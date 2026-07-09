---
title: 'Bước 1: Tạo CloudWatch Dashboard'
date: 2026-07-09
weight: 29
chapter: false
pre: ' <b> 5.7.1. </b> '
---

## Mục tiêu

Tạo dashboard để quan sát GuardDuty, Lambda, ALB và WAF.

## Giải thích dịch vụ

CloudWatch Dashboard cho phép bạn hiển thị các metrics và trạng thái quan trọng trên một màn hình duy nhất.

## Bước 1. Mở CloudWatch Console

- Tìm dịch vụ `CloudWatch`.
- Chọn **Dashboards** → **Create dashboard**.

![Search service](/images/5-Workshop/IMG_20260704_112101.jpg)

## Bước 2. Điền các field

**Dashboard name**: Nhập `soc-platform-security-dashboard`

Click **Create dashboard**

![Filled form](/images/5-Workshop/IMG_20260704_112101.jpg)

## Bước 3. Thêm widgets

Widget 1: Header

- **Widget type**: Chọn **Text**
- **Markdown**:

```
# SOC Security Dashboard - soc-platform
```

Widget 2: GuardDuty Findings

- **Widget type**: Chọn **Number**
- **Metrics**: `AWS/GuardDuty` → `FindingsCount`
- **Statistic**: Sum
- **Period**: 24 hours

Widget 3: WAF Blocked Requests

- **Widget type**: Chọn **Line**
- **Metrics**: `AWS/WAFV2` → `BlockedRequests`
- **Dimensions**: WebACL = `soc-platform-web-acl`, Rule = `ALL`

Widget 4: Security Hub Findings

- **Widget type**: Chọn **Number**
- **Metrics**: `AWS/SecurityHub` → `FindingsCount`

Widget 5: Lambda Invocations

- **Widget type**: Chọn **Stacked area**
- **Metrics**: `AWS/Lambda` → `Invocations` cho các functions:
  - `soc-platform-isolate-ec2`
  - `soc-platform-revoke-iam`
  - `soc-platform-send-notification`

  Widget 6: Lambda Errors

- **Widget type**: Chọn **Line**
- **Metrics**: `AWS/Lambda` → `Errors` cho các functions tương tự

Widget 7: ALB Request Count

- **Widget type**: Chọn **Line**
- **Metrics**: `AWS/ApplicationELB` → `RequestCount`

Widget 8: ALB Errors

- **Widget type**: Chọn **Line**
- **Metrics**: `AWS/ApplicationELB` → `HTTPCode_Target_4XX_Count`, `HTTPCode_Target_5XX_Count`

Widget 9: Step Functions Executions

- **Widget type**: Chọn **Line**
- **Metrics**: `AWS/States` → `ExecutionsStarted`, `ExecutionsFailed`

Click **Save dashboard**

![Result created](/images/5-Workshop/IMG_20260704_112101.jpg)

## Kiểm tra kết quả

- Dashboard đã được tạo.
- Metrics quan trọng có thể xem trực tiếp.

![Verification](/images/5-Workshop/IMG_20260704_112101.jpg)

## Chuyển sang bước tiếp theo

Tiếp theo, bạn sẽ tạo CloudWatch alarm.
