---
title: 'Step 2: Create an S3 bucket for log storage'
date: 2026-07-09
weight: 14
chapter: false
pre: ' <b> 5.4.2. </b> '
---

## Objective

Create an S3 bucket to store logs.

## Service explanation

Amazon S3 is a durable object storage service used to store CloudTrail logs, VPC Flow Logs, and analytics data.

## Step 1. Create the bucket

- Open the **S3 Console**.
- Select **Create bucket**.

![S3 create](/images/5-Workshop/placeholder.svg)

## Step 2. Fill in the fields

**General configuration**:

- **Bucket name**: Enter `soc-platform-logs-<account-id>` (replace `<account-id>` with your AWS Account ID).
- **AWS Region**: Select the appropriate Region.

**Block Public Access settings**:

- Keep all checkboxes selected (Block all public access).

**Bucket Versioning**:

- Select **Enable**.

**Default encryption**:

- **Encryption type**: Select **Server-side encryption with AWS KMS keys (SSE-KMS)**.
- **AWS KMS key**: Select `soc-platform-key`.
- Enable **Bucket Key**.

Click **Create bucket**.

![S3 form](/images/5-Workshop/placeholder.svg)

## Step 3. Add the bucket policy

Select the newly created bucket, open the **Permissions** tab, then select **Bucket policy** → **Edit**.

Add the following policy to allow services to write logs (CloudTrail, VPC Flow Logs, Config, GuardDuty, and ALB):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AWSCloudTrailAclCheck",
      "Effect": "Allow",
      "Principal": {
        "Service": "cloudtrail.amazonaws.com"
      },
      "Action": "s3:GetBucketAcl",
      "Resource": "arn:aws:s3:::soc-platform-logs-<account-id>"
    },
    {
      "Sid": "AWSCloudTrailWrite",
      "Effect": "Allow",
      "Principal": {
        "Service": "cloudtrail.amazonaws.com"
      },
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::soc-platform-logs-<account-id>/cloudtrail/*",
      "Condition": {
        "StringEquals": {
          "s3:x-amz-acl": "bucket-owner-full-control"
        }
      }
    },
    {
      "Sid": "AWSLogDeliveryAclCheck",
      "Effect": "Allow",
      "Principal": {
        "Service": "delivery.logs.amazonaws.com"
      },
      "Action": "s3:GetBucketAcl",
      "Resource": "arn:aws:s3:::soc-platform-logs-<account-id>"
    },
    {
      "Sid": "AWSLogDeliveryWrite",
      "Effect": "Allow",
      "Principal": {
        "Service": "delivery.logs.amazonaws.com"
      },
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::soc-platform-logs-<account-id>/vpc-flow-logs/*",
      "Condition": {
        "StringEquals": {
          "s3:x-amz-acl": "bucket-owner-full-control"
        }
      }
    },
    {
      "Sid": "DenyInsecureTransport",
      "Effect": "Deny",
      "Principal": "*",
      "Action": "s3:*",
      "Resource": [
        "arn:aws:s3:::soc-platform-logs-<account-id>",
        "arn:aws:s3:::soc-platform-logs-<account-id>/*"
      ],
      "Condition": {
        "Bool": {
          "aws:SecureTransport": "false"
        }
      }
    }
  ]
}
```

Click **Save changes**.

![Bucket policy](/images/5-Workshop/placeholder.svg)

## Step 4. Add lifecycle rules

Open the **Management** tab, then click **Create lifecycle rule**.

**Rule 1 - Transition to cheaper storage**:

- **Lifecycle rule name**: Enter `TransitionToIA`.
- **Rule scope**: Select **Apply to all objects in the bucket**.
- Under **Lifecycle rule actions**, select:
  - Transition current versions of objects between storage classes.
  - Expire current versions of objects.
- Under **Transition current versions**:
  - Transition to **Standard-IA** after **30** days.
  - Transition to **Glacier Instant Retrieval** after **90** days.
  - Transition to **Glacier Deep Archive** after **365** days.
- Under **Expire current versions**, set **2555** days (7 years).
- Click **Create rule**.

**Rule 2 - Cleanup incomplete uploads**:

- **Lifecycle rule name**: Enter `CleanupIncompleteUploads`.
- Under **Lifecycle rule actions**, select **Delete expired object delete markers or incomplete multipart uploads**.
- Set **Delete incomplete multipart uploads** to **7** days.
- Click **Create rule**.

![Lifecycle rule](/images/5-Workshop/placeholder.svg)

## Validation

- The bucket has been created successfully.
- The bucket can store logs and has the appropriate bucket policy and lifecycle rules configured.

![Validation](/images/5-Workshop/placeholder.svg)

## Next step

Next, you will create CloudTrail.