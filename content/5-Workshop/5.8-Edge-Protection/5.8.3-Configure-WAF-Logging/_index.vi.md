---
title: 'Cấu hình WAF Logging'
date: 2026-07-09
weight: 32
chapter: false
pre: ' <b> 5.8.3. </b> '
---

## Mục tiêu

Bật logging cho WAF để lưu request bị chặn hoặc cho phép.

## Giải thích dịch vụ

WAF logging giúp bạn phân tích tấn công và tối ưu rule.

## Bước 1. Bật logging

- Chọn Web ACL vừa tạo Web ACL `soc-platform-web-acl`.
- Vào tab **Logging and metrics**, click **Enable logging**.

**Logging destination**:

- **Amazon S3 bucket**: Chọn `soc-platform-logs-<account-id>`

**Filter logs**:

- **Default behavior**: Chọn **Drop**
- **Filters**: Thêm filter để chỉ giữ lại BLOCK actions

Click **Save**



## Validation

- Logging đã được bật.
- Request có thể được lưu để phân tích sau này.

![Validation](/images/5-Workshop/5.8-Edge-Protection/config-loggin-wacl.png)

## Chuyển sang bước tiếp theo

Tiếp theo, bạn sẽ tới phần test và vadilation .
