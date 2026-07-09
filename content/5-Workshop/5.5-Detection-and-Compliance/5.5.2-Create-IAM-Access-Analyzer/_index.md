---
title: 'Create an IAM Access Analyzer'
date: 2026-07-09
weight: 20
chapter: false
pre: ' <b> 5.5.2. </b> '
---

## Objective

Detect unintended access permissions.

## Service explanation

IAM Access Analyzer helps identify resources that are shared unintentionally.

## Step 1. Create the analyzer

- Open the **IAM Console**.
- Select **Access Analyzer** → **Create analyzer**.

![Access Analyzer](/images/5-Workshop/5.5-Detection-Compiance/iam-analyzer.png)

## Step 2. Fill in the fields

In the configuration page:

- **Analyzer name**: Enter `soc-platform-iam-analyzer`.
- **Zone of trust**: Select **Current account**.
- Click **Create analyzer**.

![Create analyzer form](/images/5-Workshop/5.5-Detection-Compiance/config-iam-analyzer.png)

## Validation

- The analyzer has been created.
- Access analysis has started.

![Validation](/images/5-Workshop/5.5-Detection-Compiance/valid-analyzer.png)

## Next step

Next, you will enable AWS Config.
