---
title: 'Tạo KMS Key'
date: 2026-07-09
weight: 13
chapter: false
pre: ' <b> 5.4.1. </b> '
---

## Mục tiêu

Tạo khóa mã hóa cho logs.

## Giải thích dịch vụ

AWS KMS giúp mã hóa dữ liệu ở rest và transit.

## Bước 1. Mở KMS Console

- Tìm dịch vụ `KMS`.
- Chọn **Create key**.

![Create key](/images/5-Workshop/5.4-Data-Storage/kms.png)

## Bước 2. Điền thông tin

**Configure key**:

- **Key type**: Chọn **Symmetric**
- **Key usage**: Chọn **Encrypt and decrypt**
- Click **Next**

**Add labels**:

- **Alias**: Nhập `soc-platform-key`
- **Description**: Nhập `KMS key for SOC platform encryption`
- Click **Next**

**Define key administrative permissions**:

- Chọn các IAM users/roles cần quyền quản trị key
- Click **Next**

**Define key usage permissions**:

- Thêm các services: `cloudtrail.amazonaws.com`, `s3.amazonaws.com`, `delivery.logs.amazonaws.com`, `guardduty.amazonaws.com`
- Click **Next** → **Finish**

![KMS form](/images/5-Workshop/5.4-Data-Storage/kms-configure-key.png)

## Validation

- KMS key đã được tạo.
- Có thể dùng để mã hóa S3 logs.

![Validation](/images/5-Workshop/5.4-Data-Storage/created-key.png)

## Chuyển sang bước tiếp theo

Tiếp theo, bạn sẽ tạo S3 bucket.
