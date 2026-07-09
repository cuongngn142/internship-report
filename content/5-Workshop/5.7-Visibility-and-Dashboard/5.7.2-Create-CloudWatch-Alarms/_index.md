---
title: 'Create CloudWatch Alarms'
date: 2026-07-09
weight: 30
chapter: false
pre: ' <b> 5.7.2. </b> '
---

## Objective

Create alarms to notify you when metrics exceed defined thresholds.

## Service explanation

CloudWatch Alarms send notifications when metrics exceed configured thresholds, allowing the SOC team to respond quickly.

## Step 1. Create the GuardDuty Critical Alarm

Open the **CloudWatch Console**.

- Select **Alarms**.
- Click **Create alarm**.
![create alarm](/images/5-Workshop/5.7-Visibility-Dashboard/cloudwatch-create-alarm.png)
## Step 2. Fill in the fields

**Select metric**:

- **Namespace**: `AWS/GuardDuty`.
- **Metric**: `FindingsCount`.

**Specify metric and conditions**:

- **Statistic**: **Sum**.
- **Period**: **5 minutes**.
- **Threshold type**: **Static**.
- **Condition**: **Greater than or equal to 1**.

**Configure actions**:

- **Alarm state trigger**: **In alarm**.
- **SNS topic**: Select `soc-platform-critical-alerts`.

**Alarm name**:

- Enter `soc-platform-guardduty-critical`.

Click **Create alarm**.


## Step 3. Create the Lambda Error Alarm

Repeat the same steps with the following settings:

- **Metric**: `AWS/Lambda` → `Errors` → **FunctionName** = `soc-platform-isolate-ec2`.
- **Alarm name**: `soc-platform-lambda-errors`.
![Validation](/images/5-Workshop/5.7-Visibility-Dashboard/lambda-error-alarm.png)
## Step 4. Create the WAF High Block Rate Alarm

Repeat the same steps with the following settings:

- **Metric**: `AWS/WAFV2` → `BlockedRequests`.
- **Threshold**: `1000`.
- **Evaluation Periods**: `2`.
- **Alarm name**: `soc-platform-waf-high-blocks`.

## Validation

- The alarms have been created.
- Notifications will be sent when the configured thresholds are exceeded.


## Next step

Next, you will create the edge protection layer using WAF and CloudFront.
