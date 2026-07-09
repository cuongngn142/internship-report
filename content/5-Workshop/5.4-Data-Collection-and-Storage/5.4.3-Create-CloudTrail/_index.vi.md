---
title: 'Bước 3: Tạo CloudTrail'
date: 2026-07-09
weight: 15
chapter: false
pre: ' <b> 5.4.3. </b> '
---

## Mục tiêu

Tạo CloudTrail để ghi nhận hoạt động quản trị và API.

## Giải thích dịch vụ

CloudTrail ghi lại hoạt động API và quản trị trên AWS account.

## Bước 1. Tạo trail

- Mở CloudTrail Console.
- Chọn **Create trail**.

![CloudTrail create](/images/5-Workshop/placeholder.svg)

## Bước 2. Điền thông tin

**Choose trail attributes**:

- **Trail name**: Nhập `soc-platform-trail`
- **Storage location**: Chọn **Use existing S3 bucket**
- **Trail log bucket name**: Nhập `soc-platform-logs-<account-id>`
- **Prefix**: Nhập `cloudtrail`
- **Log file SSE-KMS encryption**: Chọn **Enabled**
- **AWS KMS alias**: Chọn `soc-platform-key`
- **Log file validation**: Chọn **Enabled**

Click **Next**

**Choose log events**:

- **Event type**: Tick **Management events**
- **API activity**: Chọn **Read** và **Write**
- **Data events** (optional): Thêm S3 và Lambda nếu cần
- Click **Next** → **Create trail**

![CloudTrail form](/images/5-Workshop/placeholder.svg)

## Validation

- CloudTrail đã được tạo.
- Log bắt đầu được gửi tới bucket.

![Validation](/images/5-Workshop/placeholder.svg)

## Chuyển sang bước tiếp theo

Tiếp theo, bạn sẽ tạo VPC Flow Logs.
