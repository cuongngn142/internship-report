---
title: 'Create Lambda Functions'
date: 2026-07-09
weight: 25
chapter: false
pre: ' <b> 5.6.2. </b> '
---

## Objective

Create three Lambda functions for automated response.

## Service explanation

AWS Lambda allows you to run code without managing servers.

## Step 1. Create the IAM role for Lambda

Open the **IAM Console**, then select **Roles** → **Create role**.

**Select trusted entity**:

- **Trusted entity type**: Select **AWS service**.
- **Use case**: Select **Lambda**.
- Click **Next**.

**Add permissions**:

- Attach the `AWSLambdaBasicExecutionRole` policy.
- Click **Next**.

**Name, review, and create**:

- **Role name**: Enter `soc-platform-lambda-execution-role`.
- Click **Create role**.
![Create IAM role](/images/5-Workshop/5.6-Automated-response/iam-role.png)
Add an inline policy for SOC operations:

- Select the newly created role → **Add permissions** → **Create inline policy**.
- JSON:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:DescribeInstances",
        "ec2:DescribeSecurityGroups",
        "ec2:ModifyInstanceAttribute",
        "ec2:CreateSnapshot",
        "ec2:CreateTags"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "iam:ListAccessKeys",
        "iam:UpdateAccessKey",
        "iam:DeleteLoginProfile",
        "iam:PutUserPolicy",
        "iam:ListUserPolicies",
        "iam:GetUser"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::soc-platform-logs-<account-id>/incident-logs/*"
    },
    {
      "Effect": "Allow",
      "Action": "sns:Publish",
      "Resource": [
        "arn:aws:sns:<region>:<account-id>:soc-platform-critical-alerts",
        "arn:aws:sns:<region>:<account-id>:soc-platform-high-alerts"
      ]
    }
  ]
}
```

- Click **Create policy**.

![Lambda role](/images/5-Workshop/5.6-Automated-response/created-lambda-ex-role.png)

## Step 2. Create the `soc-platform-isolate-ec2` Lambda function

Open the **AWS Lambda Console**, then click **Create function**.

**Basic information**:

- **Function name**: Enter `soc-platform-isolate-ec2`.
- **Runtime**: Select **Python 3.11**.
- **Execution role**: Select **Use an existing role** → `soc-platform-lambda-execution-role`.
- Click **Create function**.

**Code source**:

- Paste the code from the `automated-response.yaml` file (the **IsolateEC2Function** section).

**Configuration** → **Environment variables**:

- `ISOLATION_SG_ID`: The ID of `soc-platform-isolation-sg`.
- `LOG_BUCKET`: `soc-platform-logs-<account-id>`.

**Configuration** → **General configuration**:

- **Timeout**: 5 minutes.

Click **Deploy**.

![Lambda isolate](/images/5-Workshop/5.6-Automated-response/created-lambda-isolate-ec2.png)

## Step 3. Create the `soc-platform-revoke-iam` Lambda function

Repeat the same steps:

- **Function name**: `soc-platform-revoke-iam`.
- **Environment variables**: `LOG_BUCKET`.
- Paste the code from the **RevokeIAMFunction** section.

![Lambda revoke IAM](/images/5-Workshop/5.6-Automated-response/created-lambda-revoke.png)

## Step 4. Create the `soc-platform-send-notification` Lambda function

Repeat the same steps:

- **Function name**: `soc-platform-send-notification`.
- **Environment variables**:
  - `CRITICAL_TOPIC_ARN`: ARN of the critical alerts topic.
  - `HIGH_TOPIC_ARN`: ARN of the high alerts topic.
- Paste the code from the **SendNotificationFunction** section.

![Lambda notify](/images/5-Workshop/5.6-Automated-response/created-lambda-send-noti.png)

## Validation

- All three Lambda functions have been created.
- The functions can be invoked by the automated response workflow.

![Validation](/images/5-Workshop/5.6-Automated-response/valid-lambda.png)

## Next step

Next, you will create a Step Functions state machine.
