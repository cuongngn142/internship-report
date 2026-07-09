---
title: 'Tạo S3 bucket lưu log'
date: 2026-07-09
weight: 14
chapter: false
pre: ' <b> 5.4.2. </b> '
---

## Mục tiêu

Tạo S3 bucket để lưu log.

## Giải thích dịch vụ

Amazon S3 là dịch vụ lưu trữ object bền bỉ, dùng để lưu CloudTrail, Flow Logs và dữ liệu phân tích.

## Bước 1. Tạo bucket

- Mở S3 Console.
- Chọn **Create bucket**.

![S3 create](/images/5-Workshop/5.4-Data-Storage/s3.png)

## Bước 2. Điền thông tin

**General configuration**:

- **Bucket name**: Nhập `soc-platform-logs-<account-id>` (thay `<account-id>` bằng AWS Account ID của bạn)
- **AWS Region**: Chọn region phù hợp

**Block Public Access settings**:

- Giữ nguyên tất cả các checkbox được tick (block all public access)

**Bucket Versioning**: Chọn **Enable**

**Default encryption**:

- **Encryption type**: Chọn **Server-side encryption with AWS KMS keys (SSE-KMS)**
- **AWS KMS key**: Chọn `soc-platform-key`
- Tick chọn **Bucket Key**: Enable

Click **Create bucket**

![S3 form](/images/5-Workshop/5.4-Data-Storage/create-s3-log.png)

## Bước 3. Thêm bucket policy

Chọn bucket vừa tạo, tab **Permissions**, click **Bucket policy** → **Edit**

Thêm policy cho phép các services ghi logs (CloudTrail, VPC Flow Logs, Config, GuardDuty, ALB):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AWSCloudTrailAclCheck",
      "Effect": "Allow",
      "Principal": {
        "Service": "cloudtrail.amazonaws.com"
      },
      "Action": "s3:GetBucketAcl",
      "Resource": "arn:aws:s3:::soc-platform-logs-<account-id>"
    },
    {
      "Sid": "AWSCloudTrailWrite",
      "Effect": "Allow",
      "Principal": {
        "Service": "cloudtrail.amazonaws.com"
      },
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::soc-platform-logs-<account-id>/cloudtrail/*",
      "Condition": {
        "StringEquals": {
          "s3:x-amz-acl": "bucket-owner-full-control"
        }
      }
    },
    {
      "Sid": "AWSLogDeliveryAclCheck",
      "Effect": "Allow",
      "Principal": {
        "Service": "delivery.logs.amazonaws.com"
      },
      "Action": "s3:GetBucketAcl",
      "Resource": "arn:aws:s3:::soc-platform-logs-<account-id>"
    },
    {
      "Sid": "AWSLogDeliveryWrite",
      "Effect": "Allow",
      "Principal": {
        "Service": "delivery.logs.amazonaws.com"
      },
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::soc-platform-logs-<account-id>/vpc-flow-logs/*",
      "Condition": {
        "StringEquals": {
          "s3:x-amz-acl": "bucket-owner-full-control"
        }
      }
    },
    {
      "Sid": "DenyInsecureTransport",
      "Effect": "Deny",
      "Principal": "*",
      "Action": "s3:*",
      "Resource": ["arn:aws:s3:::soc-platform-logs-<account-id>", "arn:aws:s3:::soc-platform-logs-<account-id>/*"],
      "Condition": {
        "Bool": {
          "aws:SecureTransport": "false"
        }
      }
    }
  ]
}
```

Click **Save changes**

![Bucket policy](/images/5-Workshop/5.4-Data-Storage/log-policy.png)

## Bước 4. Thêm lifecycle rule

Tab **Management**, click **Create lifecycle rule**:

**Rule 1 - Transition to cheaper storage**:

- **Lifecycle rule name**: Nhập `TransitionToIA`
- **Rule scope**: Chọn **Apply to all objects in the bucket**
- **Lifecycle rule actions**: Tick các options:
  - Transition current versions of objects between storage classes
  - Expire current versions of objects
- **Transition current versions**:
  - Transition to **Standard-IA** after **30** days
  - Transition to **Glacier Instant Retrieval** after **90** days
  - Transition to **Glacier Deep Archive** after **365** days
- **Expire current versions**: After **2555** days (7 năm)
- Click **Create rule**

**Rule 2 - Cleanup incomplete uploads**:

- **Lifecycle rule name**: Nhập `CleanupIncompleteUploads`
- **Lifecycle rule actions**: Tick **Delete expired object delete markers or incomplete multipart uploads**
- **Delete incomplete multipart uploads**: After **7** days
- Click **Create rule**

![Lifecycle rule](/images/5-Workshop/5.4-Data-Storage/log-lcr.png)

## Validation

- Bucket đã tạo thành công.
- Bucket có thể lưu log và có policy/lifecycle phù hợp.

![Validation](/images/5-Workshop/5.4-Data-Storage/valid-log.png)

## Chuyển sang bước tiếp theo

Tiếp theo, bạn sẽ tạo CloudTrail.
