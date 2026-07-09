---
title: 'Tạo IAM Access Analyzer'
date: 2026-07-09
weight: 20
chapter: false
pre: ' <b> 5.5.2. </b> '
---

## Mục tiêu

Phát hiện quyền truy cập không mong muốn.

## Giải thích dịch vụ

IAM Access Analyzer giúp xác định tài nguyên bị chia sẻ sai cách.

## Bước 1. Tạo analyzer

- Mở IAM Console.
- Chọn **Access Analyzer** → **Create analyzer**.

![Access Analyzer](/images/5-Workshop/placeholder.svg)

## Bước 2. Điền thông tin

Trong giao diện cấu hình:

- **Analyzer name**: Nhập `soc-platform-iam-analyzer`
- **Zone of trust**: Chọn **Current account**
- Click **Create analyzer**

![Create analyzer form](/images/5-Workshop/placeholder.svg)

## Validation

- Analyzer đã được tạo.
- Quá trình phân tích quyền truy cập bắt đầu.

![Validation](/images/5-Workshop/placeholder.svg)

## Chuyển sang bước tiếp theo

Tiếp theo, bạn sẽ bật AWS Config.
