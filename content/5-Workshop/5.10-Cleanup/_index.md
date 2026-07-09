---
title: 'Cleanup resources'
date: 2026-07-09
weight: 60
chapter: false
pre: ' <b> 5.9. </b> '
---

## Objective

After completing the workshop, you will clean up the resources you created to avoid unnecessary charges, prevent dependency issues, and leave the AWS environment in a clean state.

## Service explanation

Several resources in this workshop depend on one another. For example, CloudFront must be disabled before deletion, WAF needs its associations removed before deletion, and NAT Gateway must finish deleting before the next resources can be removed. Following the correct order helps you avoid errors and save time.

## Prerequisites

- You have completed all workshop deployment steps.
- You have saved any logs, snapshots, or documents you may need.
- You agree to remove the resources created during the workshop.

![Cleanup overview](/images/5-Workshop/placeholder.svg)

## Step 1. Delete the CloudFront distribution

1. Open the Amazon CloudFront console.
2. Select the `soc-platform` distribution.
3. Click **Disable** and wait for the status to become **Disabled**.
4. After it is disabled, select the distribution and click **Delete**.

![CloudFront cleanup](/images/5-Workshop/placeholder.svg)

## Step 2. Delete the WAF Web ACL

1. Open the AWS WAF console in the **us-east-1** region.
2. Select **Web ACLs** → `soc-platform-web-acl`.
3. Open **Associated AWS resources** and remove all associations if present.
4. Open **Logging and metrics** and click **Disable logging**.
5. Return to the Web ACL list, select `soc-platform-web-acl`, and click **Delete**.

![WAF cleanup](/images/5-Workshop/placeholder.svg)

## Step 3. Delete CloudWatch resources

### 3.1 Delete CloudWatch alarms

1. Open the Amazon CloudWatch console.
2. Select **Alarms** → **All alarms**.
3. Select alarms with the prefix `soc-platform-`:
   - `soc-platform-guardduty-critical`
   - `soc-platform-lambda-errors`
   - `soc-platform-waf-high-blocks`
4. Click **Actions** → **Delete**.

### 3.2 Delete the CloudWatch dashboard

1. Select **Dashboards**.
2. Select `soc-platform-security-dashboard`.
3. Click **Delete**.

![CloudWatch cleanup](/images/5-Workshop/placeholder.svg)

## Step 4. Delete EventBridge rules

1. Open the Amazon EventBridge console.
2. Select **Rules**.
3. Delete each of the following rules:
   - `soc-platform-guardduty-findings`
   - `soc-platform-securityhub-findings`
   - `soc-platform-accessanalyzer-findings`
4. For each rule:
   - Open the rule → **Targets** tab → remove all targets
   - Return and click **Delete**

![EventBridge cleanup](/images/5-Workshop/placeholder.svg)

## Step 5. Delete the Step Functions state machine

1. Open the AWS Step Functions console.
2. Select `soc-platform-security-response`.
3. Click **Delete**.
4. Confirm the deletion.

![Step Functions cleanup](/images/5-Workshop/placeholder.svg)

## Step 6. Delete Lambda functions

1. Open the AWS Lambda console.
2. Delete each function:
   - `soc-platform-isolate-ec2`
   - `soc-platform-revoke-iam`
   - `soc-platform-send-notification`
3. For each function: click **Actions** → **Delete**.

![Lambda cleanup](/images/5-Workshop/placeholder.svg)

## Step 7. Delete SNS topics

1. Open the Amazon SNS console.
2. Select **Topics**.
3. Delete the following topics:
   - `soc-platform-critical-alerts`
   - `soc-platform-high-alerts`
4. For each topic: click **Delete** and confirm.

![SNS cleanup](/images/5-Workshop/placeholder.svg)

## Step 8. Delete security services

### 8.1 Disable Security Hub

1. Open the AWS Security Hub console.
2. Go to **Settings** → **General**.
3. Click **Disable Security Hub**.
4. Confirm.

### 8.2 Disable GuardDuty

1. Open the Amazon GuardDuty console.
2. Go to **Settings**.
3. Scroll to the bottom and click **Suspend GuardDuty** or **Disable GuardDuty**.
4. Confirm.

### 8.3 Delete the IAM Access Analyzer

1. Open the IAM console.
2. Select **Access Analyzer**.
3. Select `soc-platform-iam-analyzer`.
4. Click **Delete** and confirm.

### 8.4 Delete AWS Config

1. Open the **AWS Config** console.
2. Select **Settings**.
3. Click **Edit**.
4. Clear **Recording is on**.
5. Click **Save**.
6. Open **Rules**.
7. Delete all Config Rules created during the workshop.
8. Delete the **Configuration Recorder**.
9. Delete the **Delivery Channel**.

![Security services cleanup](/images/5-Workshop/placeholder.svg)

---

## Step 9. Delete CloudTrail

1. Open the **AWS CloudTrail** console.
2. Select **Trails**.
3. Select `soc-platform-trail`.
4. Click **Delete**.
5. Confirm the deletion.

![CloudTrail cleanup](/images/5-Workshop/placeholder.svg)

---

## Step 10. Delete VPC Flow Logs

1. Open the **Amazon VPC** console.
2. Select the VPC `soc-platform-vpc`.
3. Open the **Flow logs** tab.
4. Select the flow log.
5. Click **Actions** → **Delete flow logs**.

![Flow logs cleanup](/images/5-Workshop/placeholder.svg)

---

## Step 11. Delete Athena and Glue resources

### 11.1 Delete the Athena Workgroup

1. Open the **Amazon Athena** console.
2. Select **Workgroups**.
3. Select `soc-platform-workgroup`.
4. Click **Delete**.

### 11.2 Delete the Glue Database

1. Open the **AWS Glue** console.
2. Select **Databases**.
3. Select `soc_platform_logs_db`.
4. Click **Delete**.

![Athena and Glue cleanup](/images/5-Workshop/placeholder.svg)

---

## Step 12. Delete the Application Load Balancer

1. Open the **Amazon EC2** console.
2. Select **Load Balancers**.
3. Select `soc-platform-alb`.
4. Click **Actions** → **Delete load balancer**.
5. Type **confirm** to confirm the deletion.

### Delete the Target Group

1. Select **Target Groups**.
2. Select `soc-platform-tg`.
3. Click **Actions** → **Delete**.

![ALB cleanup](/images/5-Workshop/placeholder.svg)

---

## Step 13. Delete the NAT Gateway and Elastic IP

### 13.1 Delete the NAT Gateway

1. Open the **Amazon VPC** console.
2. Select **NAT Gateways**.
3. Select `soc-platform-nat-gw`.
4. Click **Actions** → **Delete NAT gateway**.
5. Wait until the status changes to **Deleted**.

### 13.2 Release the Elastic IP

1. Select **Elastic IPs**.
2. Select the Elastic IP tagged `soc-platform-nat-eip`.
3. Click **Actions** → **Release Elastic IP addresses**.

![NAT cleanup](/images/5-Workshop/placeholder.svg)

---

## Step 14. Delete Security Groups

1. Open the **Amazon EC2** console.
2. Select **Security Groups**.
3. Delete the following security groups in order:

- `soc-platform-isolation-sg`
- `soc-platform-app-sg`
- `soc-platform-alb-sg`

4. For each security group:
   - Click **Actions** → **Delete security groups**.

> **Note:** You cannot delete the default security group of the VPC.

![Security group cleanup](/images/5-Workshop/placeholder.svg)

---

## Step 15. Delete VPC Components

### 15.1 Delete Route Tables

1. Open the **Amazon VPC** console.
2. Select **Route Tables**.
3. Select `soc-platform-private-rt`.
4. Open the **Subnet associations** tab.
5. Remove the subnet association.
6. Click **Delete**.
7. Repeat the same steps for `soc-platform-public-rt`.

> **Note:** The main route table cannot be deleted.

### 15.2 Delete Subnets

1. Select **Subnets**.
2. Delete:
   - `soc-platform-public-subnet`
   - `soc-platform-private-subnet`

### 15.3 Delete the Internet Gateway

1. Select **Internet Gateways**.
2. Select `soc-platform-igw`.
3. Click **Actions** → **Detach from VPC**.
4. Click **Actions** → **Delete internet gateway**.

### 15.4 Delete the VPC

1. Select **Your VPCs**.
2. Select `soc-platform-vpc`.
3. Click **Actions** → **Delete VPC**.
4. Type **delete** to confirm.

![VPC cleanup](/images/5-Workshop/placeholder.svg)

---

## Step 16. Delete the S3 Bucket

> **Note:** The bucket must be emptied before it can be deleted.

1. Open the **Amazon S3** console.
2. Select the bucket `soc-platform-logs-<account-id>`.
3. Click **Empty**.
4. Type `permanently delete` to confirm.
5. Wait until the empty operation is complete.
6. Click **Delete**.
7. Enter the bucket name to confirm.

![S3 cleanup](/images/5-Workshop/placeholder.svg)

---

## Step 17. Delete the AWS KMS Key

1. Open the **AWS KMS** console.
2. Select **Customer managed keys**.
3. Select the key with alias `soc-platform-key`.
4. Click **Key actions** → **Schedule key deletion**.
5. Choose a waiting period (at least **7 days** is recommended).
6. Click **Schedule deletion**.

> **Note:** The KMS key is not deleted immediately. It remains in a pending deletion state until the waiting period expires.

![KMS cleanup](/images/5-Workshop/placeholder.svg)

---

## Step 18. Delete IAM Roles

1. Open the **IAM** console.
2. Select **Roles**.
3. Delete the following roles:

- `soc-platform-lambda-execution-role`
- `soc-platform-stepfunctions-role`
- `soc-platform-eventbridge-role`
- `soc-platform-config-role`
- `soc-platform-vpc-flowlogs-role`

4. For each role:
   - Click **Delete**.
   - Confirm the deletion.

![IAM cleanup](/images/5-Workshop/placeholder.svg)

---

## Validation

Verify that the following resources have been removed successfully:

- CloudFront distribution has been deleted.
- AWS WAF Web ACL has been deleted.
- CloudWatch dashboards and alarms have been removed.
- EventBridge rules have been deleted.
- Step Functions state machine has been deleted.
- Lambda functions have been deleted.
- SNS topics have been deleted.
- Security Hub and GuardDuty have been disabled.
- IAM Access Analyzer, AWS Config, CloudTrail, and VPC Flow Logs have been removed.
- Athena workgroup and Glue database have been deleted.
- Application Load Balancer and Target Group have been deleted.
- NAT Gateway has been deleted and the Elastic IP has been released.
- Security groups have been removed (except the default security group).
- VPC and all associated networking resources have been deleted.
- S3 bucket has been deleted.
- AWS KMS key has been scheduled for deletion.
- IAM roles created for the workshop have been deleted.
- No `soc-platform` resources remain in your AWS account.