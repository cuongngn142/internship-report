---
title: 'Bước 3: Bật AWS Config'
date: 2026-07-09
weight: 21
chapter: false
pre: ' <b> 5.5.3. </b> '
---

## Mục tiêu

Theo dõi cấu hình tài nguyên và đánh giá tuân thủ.

## Giải thích dịch vụ

AWS Config ghi nhận và đánh giá cấu hình tài nguyên.

## Bước 1. Tạo IAM role cho Config

Mở **IAM console**, chọn **Roles** → **Create role**

**Select trusted entity**:

- **Trusted entity type**: Chọn **AWS service**
- **Use case**: Chọn **Config**
- Click **Next**

**Add permissions**:

- Attach policy: `AWS_ConfigRole`
- Click **Next**

**Name, review, and create**:

- **Role name**: Nhập `soc-platform-config-role`
- Click **Create role**

Thêm inline policy cho S3 access:

- Chọn role vừa tạo → **Add permissions** → **Create inline policy**
- JSON:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:PutObject", "s3:PutObjectAcl"],
      "Resource": "arn:aws:s3:::soc-platform-logs-<account-id>/config/*"
    },
    {
      "Effect": "Allow",
      "Action": "s3:GetBucketAcl",
      "Resource": "arn:aws:s3:::soc-platform-logs-<account-id>"
    }
  ]
}
```

- Click **Create policy**

![Config role](/images/5-Workshop/placeholder.svg)

## Bước 2. Bật AWS Config

**Settings**:

- **Recording method**: Chọn **All resource types with customizable overrides**
- **Include globally recorded resource types**: Tick chọn
- **AWS Config role**: Chọn **Use an existing AWS Config service-linked role**
- **Delivery method**: Chọn **Amazon S3 bucket**
- **S3 bucket**: Chọn `soc-platform-logs-<account-id>`
- **Prefix**: Nhập `config`
- Click **Next**

**Rules**: Chọn các managed rules sau:

- `s3-bucket-public-read-prohibited`
- `s3-bucket-public-write-prohibited`
- `root-account-mfa-enabled`
- `iam-user-mfa-enabled`
- `vpc-flow-logs-enabled`
- `cloud-trail-enabled`
- `encrypted-volumes`
- `restricted-ssh`
- `rds-storage-encrypted`

Click **Next** → **Confirm**

![Enable Config](/images/5-Workshop/placeholder.svg)

## Validation

- AWS Config đã hoạt động.
- Tài nguyên bắt đầu được ghi nhận.

![Validation](/images/5-Workshop/placeholder.svg)

## Chuyển sang bước tiếp theo

Tiếp theo, bạn sẽ bật Security Hub.
