---
title: 'Bước 4: Tạo EventBridge Rules'
date: 2026-07-09
weight: 27
chapter: false
pre: ' <b> 5.6.4. </b> '
---

## Mục tiêu

Tạo rule để lắng nghe event từ GuardDuty hoặc Security Hub.

## Giải thích dịch vụ

Amazon EventBridge cho phép chuyển event tới Lambda, SNS hoặc Step Functions.

## Bước 1. Tạo rule

- Mở EventBridge Console.
- Chọn **Rules** → **Create rule**.

**Define rule detail**:

- **Name**: Nhập `soc-platform-guardduty-findings`
- **Description**: Nhập `Trigger automated response for high/critical GuardDuty findings`
- **Event bus**: Chọn **default**
- Click **Next**

![Create rule](/images/5-Workshop/placeholder.svg)

## Bước 2. Điền event pattern

**Build event pattern**:

- **Event source**: Chọn **AWS events or EventBridge partner events**
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

- Click **Next**

![Event pattern](/images/5-Workshop/placeholder.svg)

## Bước 3. Chọn target

**Select target(s)**:

- **Target type**: Chọn **AWS service**
- **Select a target**: Chọn **Step Functions state machine**
- **State machine**: Chọn `soc-platform-security-response`
- Click **Next** → **Create rule**

![Target](/images/5-Workshop/placeholder.svg)

## Bước 4. Rule cho Security Hub Findings

Click **Create rule**:

- **Name**: `soc-platform-securityhub-findings`
- **Event pattern**:

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

- **Target**: SNS topic `soc-platform-critical-alerts`

## Bước 5. Rule cho IAM Access Analyzer

Click **Create rule**:

- **Name**: `soc-platform-accessanalyzer-findings`
- **Event pattern**:

```json
{
  "source": ["aws.access-analyzer"],
  "detail-type": ["Access Analyzer Finding"]
}
```

- **Target**: SNS topic `soc-platform-high-alerts`

## Validation

- Rule đã được tạo.
- Event được chuyển tới target phù hợp.

![Validation](/images/5-Workshop/placeholder.svg)

## Chuyển sang bước tiếp theo

Tiếp theo, bạn sẽ tạo dashboard và alarm trên CloudWatch.
