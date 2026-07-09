---
title: 'Tạo CloudWatch Alarms'
date: 2026-07-09
weight: 30
chapter: false
pre: ' <b> 5.7.2. </b> '
---

## Mục tiêu

Tạo alarm để cảnh báo khi metric vượt ngưỡng.

## Giải thích dịch vụ

CloudWatch Alarm gửi cảnh báo khi metric vượt ngưỡng, giúp SOC team phản ứng nhanh.

## Bước 1. Tạo GuardDuty Critical Alarm

Mở **CloudWatch console**

- Chọn **Alarms**.
- Nhấn **Create alarm**.

![Search service](/images/5-Workshop/IMG_20260704_112101.jpg)

## Bước 2. Điền các field

**Select metric**:

- **Namespace**: `AWS/GuardDuty`
- **Metric**: `FindingsCount`

**Specify metric and conditions**:

- **Statistic**: Sum
- **Period**: 5 minutes
- **Threshold type**: Static
- **Condition**: Greater/Equal than 1

**Configure actions**:

- **Alarm state trigger**: In alarm
- **SNS topic**: Chọn `soc-platform-critical-alerts`

**Alarm name**: Nhập `soc-platform-guardduty-critical`

Click **Create alarm**

![Filled form](/images/5-Workshop/IMG_20260704_112101.jpg)

## Bước 3. Tạo Lambda Error Alarm

Lặp lại tương tự với:

- **Metric**: `AWS/Lambda` → `Errors` → FunctionName = `soc-platform-isolate-ec2`
- **Alarm name**: `soc-platform-lambda-errors`

## Bước 4. Tạo WAF High Block Rate Alarm

Lặp lại tương tự với:

- **Metric**: `AWS/WAFV2` → `BlockedRequests`
- **Threshold**: 1000
- **Evaluation Periods**: 2
- **Alarm name**: `soc-platform-waf-high-blocks`

## Kiểm tra kết quả

- Alarm đã được tạo.
- Cảnh báo sẽ được gửi khi metric vượt ngưỡng.

![Verification](/images/5-Workshop/IMG_20260704_112101.jpg)

## Chuyển sang bước tiếp theo

Tiếp theo, bạn sẽ tạo lớp bảo vệ ở biên bằng WAF và CloudFront.
