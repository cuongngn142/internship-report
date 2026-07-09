---
title: 'Tạo Athena Workgroup và Glue Database'
date: 2026-07-09
weight: 17
chapter: false
pre: ' <b> 5.4.5. </b> '
---

## Mục tiêu

Tạo Athena Workgroup và Glue Database để query log.

## Giải thích dịch vụ

Athena cho phép query dữ liệu trực tiếp trên S3 bằng SQL; Glue Database làm schema cho bảng log.

## Bước 1. Tạo Athena Workgroup

- Mở Athena Console.
- Chọn **Workgroups** → **Create workgroup**.

![Athena workgroup](/images/5-Workshop/5.4-Data-Storage/athena-g.png)

## Bước 2. Điền thông tin

Trong giao diện cấu hình:

- **Workgroup name**: Nhập `soc-platform-workgroup`
- **Query result location**: Nhập `s3://soc-platform-logs-<account-id>/athena-results/`
- **Encrypt query results**: Chọn **SSE-KMS** và chọn key `soc-platform-key`
- **Publish query metrics to CloudWatch**: Chọn **Enable**
- Click **Create workgroup**

![Athena form](/images/5-Workshop/5.4-Data-Storage/create-groupwork.png)

## Bước 3. Tạo Glue Database

- Mở Glue Console.
- Chọn **Databases** → **Add database**.

Trong giao diện cấu hình:

- **Database name**: Nhập `soc_platform_logs_db`
- **Description**: Nhập `SOC Platform logs database for Athena queries`
- Click **Create database**

![Glue DB](/images/5-Workshop/5.4-Data-Storage/glue-database.png)

## Validation

- Athena Workgroup đã sẵn sàng.
- Glue Database có thể dùng cho query log.

![Validation](/images/5-Workshop/5.4-Data-Storage/valid-glue-database)

## Chuyển sang bước tiếp theo

Tiếp theo, bạn sẽ bật các dịch vụ phát hiện và tuân thủ.
