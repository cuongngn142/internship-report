---
title: 'Tạo VPC Flow Logs'
date: 2026-07-09
weight: 16
chapter: false
pre: ' <b> 5.4.4. </b> '
---

## Mục tiêu

Ghi lại traffic mạng trong VPC.

## Giải thích dịch vụ

VPC Flow Logs ghi lại thông tin traffic cho phân tích sự cố và phát hiện bất thường.

## Bước 1. Tạo flow log

- Mở VPC Console.
- Chọn VPC `soc-platform-vpc`.
- Chọn **Flow logs** → **Create flow log**.

![Flow logs create](/images/5-Workshop/5.4-Data-Storage/flow-log.png)

## Bước 2. Điền thông tin

Trong giao diện cấu hình:

- **Name**: Nhập `soc-platform-vpc-flowlog`
- **Filter**: Chọn **Reject** (chỉ ghi log traffic bị reject)
- **Maximum aggregation interval**: Chọn **10 minutes**
- **Destination**: Chọn **Send to an Amazon S3 bucket**
- **S3 bucket ARN**: Nhập `arn:aws:s3:::soc-platform-logs-<account-id>/vpc-flow-logs/`
- **Log record format**: Chọn **Custom format** và thêm:
  ```
  ${version} ${account-id} ${interface-id} ${srcaddr} ${dstaddr} ${srcport} ${dstport} ${protocol} ${packets} ${bytes} ${start} ${end} ${action} ${log-status}
  ```
- Click **Create flow log**

![Flow logs form](/images/5-Workshop/5.4-Data-Storage/create-fl.png)

## Validation

- Flow log đã được tạo.
- Traffic được ghi lại.

![Validation](/images/5-Workshop/5.4-Data-Storage/valid-fl.png)

## Chuyển sang bước tiếp theo

Tiếp theo, bạn sẽ tạo Athena Workgroup và Glue Database.
