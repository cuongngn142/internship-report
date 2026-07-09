---
title: 'Step 3: Create CloudTrail'
date: 2026-07-09
weight: 15
chapter: false
pre: ' <b> 5.4.3. </b> '
---

## Objective

Create CloudTrail to record management activities and API calls.

## Service explanation

CloudTrail records API activity and management events within your AWS account.

## Step 1. Create the trail

- Open the **CloudTrail Console**.
- Select **Create trail**.

![CloudTrail create](/images/5-Workshop/placeholder.svg)

## Step 2. Fill in the fields

**Choose trail attributes**:

- **Trail name**: Enter `soc-platform-trail`.
- **Storage location**: Select **Use existing S3 bucket**.
- **Trail log bucket name**: Enter `soc-platform-logs-<account-id>`.
- **Prefix**: Enter `cloudtrail`.
- **Log file SSE-KMS encryption**: Select **Enabled**.
- **AWS KMS alias**: Select `soc-platform-key`.
- **Log file validation**: Select **Enabled**.

Click **Next**.

**Choose log events**:

- **Event type**: Select **Management events**.
- **API activity**: Select both **Read** and **Write**.
- **Data events** (optional): Add S3 and Lambda if needed.
- Click **Next** → **Create trail**.

![CloudTrail form](/images/5-Workshop/placeholder.svg)

## Validation

- CloudTrail has been created.
- Logs are being delivered to the S3 bucket.

![Validation](/images/5-Workshop/placeholder.svg)

## Next step

Next, you will create VPC Flow Logs.
