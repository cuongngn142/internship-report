---
title: 'Tạo SNS Topics'
date: 2026-07-09
weight: 24
chapter: false
pre: ' <b> 5.6.1. </b> '
---

## Mục tiêu

Tạo topic để gửi cảnh báo tới email hoặc hệ thống khác.

## Giải thích dịch vụ

Amazon SNS là dịch vụ publish/subscribe dùng để gửi thông báo tới nhiều subscriber.

## Bước 1. Tạo topic

- Mở SNS Console.
- Chọn **Topics** → **Create topic**.

Trong giao diện cấu hình:

- **Type**: Chọn **Standard**
- **Name**: Nhập `soc-platform-critical-alerts`
- **Encryption**: Chọn **Enable encryption** và chọn KMS key `alias/aws/sns`
- Click **Create topic**

![Create SNS topic](/images/5-Workshop/5.6-Automated-response/sns-topic.png)
## Bước 2. Thêm subscription

Click **Create subscription**:

- **Protocol**: Chọn **Email**
- **Endpoint**: Nhập email của SOC team
- Click **Create subscription**


## Bước 3. Xác nhận email

- Xác nhận subscription trong email.

![SNS subscription](/images/5-Workshop/5.6-Automated-response/create-sub-critical.png)

## Bước 4. Tạo High Alerts Topic

Lặp lại các bước tương tự với tên `soc-platform-high-alerts`

![Confirm email](/images/5-Workshop/5.6-Automated-response/create-sns-high-alert.png)

## Validation

- SNS topic đã tạo.
- Subscription hoạt động.

![Validation](/images/5-Workshop/valid-sns-high-alert.png)

## Chuyển sang bước tiếp theo

Tiếp theo, bạn sẽ tạo Lambda functions.
