---
title: 'Enable GuardDuty'
date: 2026-07-09
weight: 19
chapter: false
pre: ' <b> 5.5.1. </b> '
---

## Objective

Detect suspicious activities in your AWS environment.

## Service explanation

Amazon GuardDuty uses telemetry data and machine learning to detect security threats.

## Step 1. Open GuardDuty

- Search for the `GuardDuty` service.
- Select **Get started**.

![GuardDuty console](/images/5-Workshop/5.5-Detection-Compiance/guardduty.png)

## Step 2. Enable GuardDuty

- Select **Enable GuardDuty**.

After enabling GuardDuty, select **Settings**.

- **Finding publishing frequency**: Select **15 minutes**.
- **S3 Protection**: Select **Enable**.
- **EKS Protection**: Select **Enable** (if you are using EKS).
- **Malware Protection**: Select **Enable**.
- Click **Save**.

![GuardDuty form](/images/5-Workshop/5.5-Detection-Compiance/setting-guardduty.png)

## Validation

- GuardDuty has been enabled.
- Findings are being generated.

![Validation](/images/5-Workshop/5.5-Detection-Compiance/valid-guardduty.png)

## Next step

Next, you will create an IAM Access Analyzer.
