---
title: 'Enable AWS Config'
date: 2026-07-09
weight: 21
chapter: false
pre: ' <b> 5.5.3. </b> '
---

## Objective

Monitor resource configurations and evaluate compliance.

## Service explanation

AWS Config records and evaluates the configuration of AWS resources.

## Step 1. Create the IAM role for AWS Config

Open the **IAM Console**, then select **Roles** → **Create role**.

**Select trusted entity**:

- **Trusted entity type**: Select **AWS service**.
- **Use case**: Select **Config**.
- Click **Next**.

**Add permissions**:

- Attach the `AWS_ConfigRole` policy.
- Click **Next**.

**Name, review, and create**:

- **Role name**: Enter `soc-platform-config-role`.
- Click **Create role**.

Add an inline policy for S3 access:

- Select the newly created role → **Add permissions** → **Create inline policy**.
- JSON:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:PutObject", "s3:PutObjectAcl"],
      "Resource": "arn:aws:s3:::soc-platform-logs-<account-id>/config/*"
    },
    {
      "Effect": "Allow",
      "Action": "s3:GetBucketAcl",
      "Resource": "arn:aws:s3:::soc-platform-logs-<account-id>"
    }
  ]
}
```

- Click **Create policy**.

![Config role](/images/5-Workshop/5.5-Detection-Compiance/iam-create-role.png)

## Step 2. Enable AWS Config

**Settings**:

- **Recording method**: Select **All resource types with customizable overrides**.
- **Include globally recorded resource types**: Select the checkbox.
- **AWS Config role**: Select **Use an existing AWS Config service-linked role**.
- **Delivery method**: Select **Amazon S3 bucket**.
- **S3 bucket**: Select `soc-platform-logs-<account-id>`.
- **Prefix**: Enter `config`.
- Click **Next**.

**Rules**:

Select the following managed rules:

- `s3-bucket-public-read-prohibited`
- `s3-bucket-public-write-prohibited`
- `root-account-mfa-enabled`
- `iam-user-mfa-enabled`
- `vpc-flow-logs-enabled`
- `cloud-trail-enabled`
- `encrypted-volumes`
- `restricted-ssh`
- `rds-storage-encrypted`

Click **Next** → **Confirm**.

![Enable Config](/images/5-Workshop/5.5-Detection-Compiance/awsconfig.png)

## Validation

- AWS Config has been enabled.
- Resource configurations are being recorded.

![Validation](/images/5-Workshop/5.5-Detection-Compiance/valid-awsconfig.png)

## Next step

Next, you will enable Security Hub.
