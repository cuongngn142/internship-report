---
title: 'Step 1: Create a CloudWatch Dashboard'
date: 2026-07-09
weight: 29
chapter: false
pre: ' <b> 5.7.1. </b> '
---

## Objective

Create a dashboard to monitor GuardDuty, Lambda, ALB, and WAF.

## Service explanation

CloudWatch Dashboards allow you to display important metrics and resource status on a single screen.

## Step 1. Open the CloudWatch Console

- Search for the `CloudWatch` service.
- Select **Dashboards** → **Create dashboard**.

![Search service](/images/5-Workshop/IMG_20260704_112101.jpg)

## Step 2. Fill in the fields

**Dashboard name**:

- Enter `soc-platform-security-dashboard`.

Click **Create dashboard**.

![Filled form](/images/5-Workshop/IMG_20260704_112101.jpg)

## Step 3. Add widgets

**Widget 1: Header**

- **Widget type**: Select **Text**.
- **Markdown**:

```
# SOC Security Dashboard - soc-platform
```

**Widget 2: GuardDuty Findings**

- **Widget type**: Select **Number**.
- **Metrics**: `AWS/GuardDuty` → `FindingsCount`.
- **Statistic**: **Sum**.
- **Period**: **24 hours**.

**Widget 3: WAF Blocked Requests**

- **Widget type**: Select **Line**.
- **Metrics**: `AWS/WAFV2` → `BlockedRequests`.
- **Dimensions**: **WebACL** = `soc-platform-web-acl`, **Rule** = `ALL`.

**Widget 4: Security Hub Findings**

- **Widget type**: Select **Number**.
- **Metrics**: `AWS/SecurityHub` → `FindingsCount`.

**Widget 5: Lambda Invocations**

- **Widget type**: Select **Stacked area**.
- **Metrics**: `AWS/Lambda` → `Invocations` for the following functions:
  - `soc-platform-isolate-ec2`
  - `soc-platform-revoke-iam`
  - `soc-platform-send-notification`

**Widget 6: Lambda Errors**

- **Widget type**: Select **Line**.
- **Metrics**: `AWS/Lambda` → `Errors` for the same Lambda functions.

**Widget 7: ALB Request Count**

- **Widget type**: Select **Line**.
- **Metrics**: `AWS/ApplicationELB` → `RequestCount`.

**Widget 8: ALB Errors**

- **Widget type**: Select **Line**.
- **Metrics**: `AWS/ApplicationELB` → `HTTPCode_Target_4XX_Count`, `HTTPCode_Target_5XX_Count`.

**Widget 9: Step Functions Executions**

- **Widget type**: Select **Line**.
- **Metrics**: `AWS/States` → `ExecutionsStarted`, `ExecutionsFailed`.

Click **Save dashboard**.

![Result created](/images/5-Workshop/IMG_20260704_112101.jpg)

## Validation

- The dashboard has been created.
- Key metrics can be viewed directly from the dashboard.

![Verification](/images/5-Workshop/IMG_20260704_112101.jpg)

## Next step

Next, you will create CloudWatch alarms.
