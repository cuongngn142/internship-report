---

title: "Test & Validation"
date: 2026-07-09
weight: 59
chapter: false
pre: " 5.9. "
-------------

In this lab, we will perform end-to-end testing to validate the complete SOC Automation workflow. The objective is to ensure that the solution operates correctly from the moment a finding is generated in AWS Security Hub, through AWS Step Functions orchestration, AWS Lambda remediation, and finally Amazon SNS notification delivery.

---

## 1. Test Critical Response - Isolate EC2

### Scenario

This is the most aggressive response implemented by the system.

When AWS Security Hub detects an EC2 instance infected with malware or performing suspicious activities (such as Bitcoin mining, Command & Control communication, or Data Exfiltration), the workflow immediately isolates the EC2 instance to prevent lateral movement or further compromise.

---

### Step 1: Open AWS Step Functions

Navigate to:

**AWS Console → Step Functions → State machines → SecurityAutomationWorkflow**

Choose **Start execution**.

![Image](/images/5-Workshop/5.9-Test-Validation/anh1.png)

---

### Step 2: Paste the Event JSON

Use the following input:

```json
{
  "version": "0",
  "id": "12345678-1234-1234-1234-123456789012",
  "detail-type": "Security Hub Findings - Imported",
  "source": "aws.securityhub",
  "account": "629068383761",
  "time": "2026-07-09T13:35:00Z",
  "region": "ap-southeast-1",
  "resources": [],
  "detail": {
    "findings": [
      {
        "SchemaVersion": "2018-10-08",
        "Id": "arn:aws:securityhub:ap-southeast-1:<Your AWS ACCOUNT ID>:finding/critical-ec2-malware-example",
        "ProductArn": "arn:aws:securityhub:ap-southeast-1::product/aws/guardduty",
        "GeneratorId": "aws-guardduty",
        "AwsAccountId": "<Your AWS ACCOUNT ID>",
        "Types": [
          "Effects/Data Exfiltration"
        ],
        "FirstObservedAt": "2026-07-09T13:30:00.000Z",
        "LastObservedAt": "2026-07-09T13:32:00.000Z",
        "CreatedAt": "2026-07-09T13:30:00.000Z",
        "UpdatedAt": "2026-07-09T13:32:00.000Z",
        "Severity": {
          "Product": 8,
          "Normalized": 80,
          "Label": "HIGH"
        },
        "Title": "CryptoCurrency:EC2/BitcoinTool.B",
        "Description": "EC2 instance is querying malware domains associated with Bitcoin mining.",
        "Resources": [
          {
            "Type": "AwsEc2Instance",
            "Id": "<Your EC2 Instance ID>",
            "Region": "ap-southeast-1"
          }
        ],
        "WorkflowState": "NEW",
        "RecordState": "ACTIVE"
      }
    ]
  }
}
```

![Image](/images/5-Workshop/5.9-Test-Validation/anh2.png)

---

### Step 3: Monitor the Execution

Observe the workflow execution.

Expected workflow:

```
Parse Finding
        ↓
Check Severity
        ↓
Isolate EC2
        ↓
Send Notification
```

![Image](/images/5-Workshop/5.9-Test-Validation/anh3.png)

The following image shows the EC2 instance before being isolated. At this point, the instance is still attached to its original Security Group.

![Image](/images/5-Workshop/5.9-Test-Validation/anh6.png)

After the workflow completes, the instance is attached to the Isolation Security Group, which contains no inbound or outbound rules.

![Image](/images/5-Workshop/5.9-Test-Validation/anh7.png)

---

### Step 4: Verify CloudWatch Logs

Navigate to:

```
CloudWatch
→ Log Groups
→ /aws/lambda/dev-isolate-ec2
```

Verify that the Lambda function successfully isolated the EC2 instance.

![Image](/images/5-Workshop/5.9-Test-Validation/anh4.png)

---

### Step 5: Verify Email Notification

Open the email address subscribed to the SNS topic.

Verify that an email notification indicating the EC2 isolation has been received.

![Image](/images/5-Workshop/5.9-Test-Validation/anh5.png)

---

### Expected Result

* The Step Functions execution completes successfully.
* The EC2 Isolation Lambda function is invoked.
* CloudWatch Logs record the remediation process.
* An SNS email notification is delivered.
* The EC2 instance is attached to the Isolation Security Group.

---

## 2. Test Critical Response - Revoke IAM Access Key

### Scenario

When an IAM Access Key is exposed or compromised, the system immediately revokes the credential to prevent unauthorized access to AWS resources.

---

### Step 1: Open AWS Step Functions

Repeat the steps from Test Case 1.

---

### Step 2: Paste the Event JSON

```json
{
  "version": "0",
  "id": "22222222-2222-2222-2222-222222222222",
  "detail-type": "Security Hub Findings - Imported",
  "source": "aws.securityhub",
  "account": "<Your AWS Account ID>",
  "time": "2026-07-09T13:35:00Z",
  "region": "ap-southeast-1",
  "detail": {
    "findings": [
      {
        "AwsAccountId": "<Your AWS Account ID>",
        "Id": "arn:aws:securityhub:ap-southeast-1:<Your AWS Account ID>:finding/iam-revoke",
        "Severity": {
          "Product": 8
        },
        "Title": "IAM:AccessKey/Exposed",
        "Description": "IAM Access Key found on GitHub.",
        "Resources": [
          {
            "Type": "AwsIamAccessKey",
            "Id": "arn:aws:iam::<Your AWS Account ID>:access-key/<Your Access Key>",
            "Region": "ap-southeast-1"
          }
        ]
      }
    ]
  }
}
```

![Image](/images/5-Workshop/5.9-Test-Validation/anh8.png)

---

### Step 3: Monitor the Execution

Expected workflow:

```
Parse Finding
      ↓
Check Severity
      ↓
Revoke IAM
      ↓
Send Notification
```

![Image](/images/5-Workshop/5.9-Test-Validation/anh9.png)

An IAM user with an Access Key created for testing.

![Image](/images/5-Workshop/5.9-Test-Validation/anh12.png)

After the simulated compromise, the Lambda function revokes the exposed Access Key.

![Image](/images/5-Workshop/5.9-Test-Validation/anh13.png)

---

### Step 4: Verify CloudWatch Logs

```
/aws/lambda/dev_revoke_iam
```

![Image](/images/5-Workshop/5.9-Test-Validation/anh10.png)

---

### Step 5: Verify Email Notification

Verify that an email notification indicating the Access Key has been revoked is received.

![Image](/images/5-Workshop/5.9-Test-Validation/anh11.png)

---

### Expected Result

* The Revoke IAM Lambda function is executed.
* The Access Key is disabled or deleted according to the implementation.
* CloudWatch Logs record the operation.
* An SNS notification email is successfully delivered.

---

## 3. Test Critical Unsupported Resource - Skip Automated Action

### Scenario

Some AWS resources, such as Amazon S3 and Amazon CloudFront, do not currently have automated remediation workflows.

To avoid disrupting production services, the system skips automated actions and only records the finding while notifying administrators.

---

### Step 1: Open AWS Step Functions

Repeat Step 1 from the previous test.

---

### Step 2: Paste the Event JSON

```json
{
  "version": "0",
  "id": "33333333-3333-3333-3333-333333333333",
  "detail-type": "Security Hub Findings - Imported",
  "source": "aws.securityhub",
  "account": "<Your AWS Account ID>",
  "time": "2026-07-09T13:35:00Z",
  "region": "ap-southeast-1",
  "detail": {
    "findings": [
      {
        "AwsAccountId": "<Your AWS Account ID>",
        "Id": "arn:aws:securityhub:ap-southeast-1:<Your AWS Account ID>:finding/s3-unsupported",
        "Severity": {
          "Product": 9
        },
        "Title": "S3:Bucket/PublicAccess",
        "Description": "nothing",
        "Resources": [
          {
            "Type": "AwsS3Bucket",
            "Id": "<Your S3 Bucket Name>",
            "Region": "ap-southeast-1"
          }
        ]
      }
    ]
  }
}
```

![Image](/images/5-Workshop/5.9-Test-Validation/anh14.png)

---

### Step 3: Monitor the Execution

```
Parse Finding
      ↓
Check Severity
      ↓
Skip Automated Action
      ↓
Send Notification
```

![Image](/images/5-Workshop/5.9-Test-Validation/anh15.png)

---

### Step 4: Verify CloudWatch Logs

Verify the Skip Action Lambda logs.

![Image](/images/5-Workshop/5.9-Test-Validation/anh16.png)

---

### Step 5: Verify Email Notification

![Image](/images/5-Workshop/5.9-Test-Validation/anh17.png)

---

### Expected Result

* No changes are made to the AWS resource.
* The finding is logged.
* An email notification is sent.
* The workflow completes successfully.

---

## 4. Test High Severity (Human in the Loop)

### Scenario

For findings with High severity (between 4 and 6.9), the system does not perform automatic remediation. Instead, it logs the event and forwards it to the SOC analyst for manual review and decision-making.

---

### Step 1: Open AWS Step Functions

Repeat the steps from Test Case 1.

---

### Step 2: Paste the Event JSON

```json
{
  "version": "0",
  "id": "44444444-4444-4444-4444-444444444444",
  "detail-type": "Security Hub Findings - Imported",
  "source": "aws.securityhub",
  "account": "<Your AWS Account ID>",
  "time": "2026-07-09T13:35:00Z",
  "region": "ap-southeast-1",
  "detail": {
    "findings": [
      {
        "AwsAccountId": "<Your AWS Account ID>",
        "Id": "arn:aws:securityhub:ap-southeast-1:<Your AWS Account ID>:finding/high-severity",
        "Severity": {
          "Product": 5
        },
        "Title": "IAM:User/PasswordPolicy",
        "Description": "Weak password policy detected.",
        "Resources": [
          {
            "Type": "AwsIamUser",
            "Id": "admin",
            "Region": "ap-southeast-1"
          }
        ]
      }
    ]
  }
}
```

![Image](/images/5-Workshop/5.9-Test-Validation/anh18.png)

---

### Step 3: Monitor the Execution

```
Parse Finding
      ↓
Check Severity
      ↓
Human Review
      ↓
Send Notification
```

![Image](/images/5-Workshop/5.9-Test-Validation/anh19.png)

---

### Step 4: Verify CloudWatch Logs

![Image](/images/5-Workshop/5.9-Test-Validation/anh20.png)

---

### Step 5: Verify Email Notification

![Image](/images/5-Workshop/5.9-Test-Validation/anh21.png)

---

### Expected Result

* No automated remediation is performed.
* CloudWatch Logs record the event.
* An email notification is sent.
* The finding is forwarded for manual investigation.

---

## 5. Test Low Severity (Log and Monitor)

### Scenario

Low-severity findings are primarily used for observability purposes.

The workflow simply records the event in CloudWatch Logs without performing any remediation actions.

---

### Step 1: Open AWS Step Functions

Repeat the steps from Test Case 1.

---

### Step 2: Paste the Event JSON

```json
{
  "version": "0",
  "id": "55555555-5555-5555-5555-555555555555",
  "detail-type": "Security Hub Findings - Imported",
  "source": "aws.securityhub",
  "account": "<Your AWS Account ID>",
  "time": "2026-07-09T13:35:00Z",
  "region": "ap-southeast-1",
  "detail": {
    "findings": [
      {
        "AwsAccountId": "<Your AWS Account ID>",
        "Id": "arn:aws:securityhub:ap-southeast-1:<Your AWS Account ID>:finding/low-severity-info",
        "Severity": {
          "Product": 2
        },
        "Title": "CloudTrail:Event/Disabled",
        "Description": "CloudTrail logging is disabled.",
        "Resources": [
          {
            "Type": "AwsCloudTrailTrail",
            "Id": "default-trail",
            "Region": "ap-southeast-1"
          }
        ]
      }
    ]
  }
}
```

![Image](/images/5-Workshop/5.9-Test-Validation/anh22.png)

---

### Step 3: Monitor the Execution

```
Parse Finding
      ↓
Check Severity
      ↓
Log and Monitor
```

![Image](/images/5-Workshop/5.9-Test-Validation/anh23.png)

---

### Expected Result

* The Step Functions execution completes successfully.
* No remediation action is performed.
* The finding is recorded in CloudWatch Logs.
* No AWS resources are modified.
