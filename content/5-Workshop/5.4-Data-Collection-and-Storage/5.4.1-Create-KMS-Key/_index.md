---
title: 'Create a KMS Key'
date: 2026-07-09
weight: 13
chapter: false
pre: ' <b> 5.4.1. </b> '
---

## Objective

Create an encryption key for logs.

## Service explanation

AWS KMS helps encrypt data at rest and in transit.

## Step 1. Open the KMS Console

- Search for the `KMS` service.
- Select **Create key**.

![Create key](/images/5-Workshop/placeholder.svg)

## Step 2. Fill in the fields

**Configure key**:

- **Key type**: Select **Symmetric**.
- **Key usage**: Select **Encrypt and decrypt**.
- Click **Next**.

**Add labels**:

- **Alias**: Enter `soc-platform-key`.
- **Description**: Enter `KMS key for SOC platform encryption`.
- Click **Next**.

**Define key administrative permissions**:

- Select the IAM users or roles that require key administrative permissions.
- Click **Next**.

**Define key usage permissions**:

- Add the following services: `cloudtrail.amazonaws.com`, `s3.amazonaws.com`, `delivery.logs.amazonaws.com`, `guardduty.amazonaws.com`.
- Click **Next** → **Finish**.

![KMS form](/images/5-Workshop/placeholder.svg)

## Validation

- The KMS key has been created.
- It can be used to encrypt S3 logs.

![Validation](/images/5-Workshop/placeholder.svg)

## Next step

Next, you will create an S3 bucket.