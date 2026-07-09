---
title: 'Create EventBridge Rules'
date: 2026-07-09
weight: 27
chapter: false
pre: ' <b> 5.6.4. </b> '
---

## Objective

Create rules to listen for events from GuardDuty or Security Hub.

## Service explanation

Amazon EventBridge routes events to services such as Lambda, SNS, or Step Functions.

## Step 1. Create the GuardDuty rule

- Open the **EventBridge Console**.
- Select **Rules** → **Create rule**.

**Define rule detail**:

- **Name**: Enter `soc-platform-guardduty-findings`.
- **Description**: Enter `Trigger automated response for high/critical GuardDuty findings`.
- **Event bus**: Select **default**.
- Click **Next**.

![Create rule](/images/5-Workshop/placeholder.svg)

## Step 2. Fill in the GuardDuty event pattern

**Build event pattern**:

- **Event source**: Select **AWS events or EventBridge partner events**.
- **Event pattern**:

```json
{
  "source": ["aws.guardduty"],
  "detail-type": ["GuardDuty Finding"],
  "detail": {
    "severity": [
      {
        "numeric": [">=", 4]
      }
    ]
  }
}
```

- Click **Next**.

![Event pattern](/images/5-Workshop/placeholder.svg)

## Step 3. Select the target

**Select target(s)**:

- **Target type**: Select **AWS service**.
- **Select a target**: Select **Step Functions state machine**.
- **State machine**: Select `soc-platform-security-response`.
- Click **Next** → **Create rule**.

![Target](/images/5-Workshop/placeholder.svg)

## Step 4. Create the Security Hub findings rule

Click **Create rule**.

- **Name**: Enter `soc-platform-securityhub-findings`.

**Event pattern**:

```json
{
  "source": ["aws.securityhub"],
  "detail-type": ["Security Hub Findings - Imported"],
  "detail": {
    "findings": {
      "Severity": {
        "Label": ["CRITICAL", "HIGH"]
      }
    }
  }
}
```

- **Target**: Select the SNS topic `soc-platform-critical-alerts`.

## Step 5. Create the IAM Access Analyzer rule

Click **Create rule**.

- **Name**: Enter `soc-platform-accessanalyzer-findings`.

**Event pattern**:

```json
{
  "source": ["aws.access-analyzer"],
  "detail-type": ["Access Analyzer Finding"]
}
```

- **Target**: Select the SNS topic `soc-platform-high-alerts`.

## Validation

- The rules have been created.
- Events are routed to the appropriate targets.

![Validation](/images/5-Workshop/placeholder.svg)

## Next step

Next, you will create a CloudWatch dashboard and alarms.
