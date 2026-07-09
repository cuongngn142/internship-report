---
title: 'Tạo CloudFront Distribution'
date: 2026-07-09
weight: 31
chapter: false
pre: ' <b> 5.8.2. </b> '
---

## Mục tiêu

Tạo CloudFront distribution để phân phối nội dung và bảo vệ origin.

## Giải thích dịch vụ

CloudFront là CDN của AWS giúp giảm độ trễ và bảo vệ ứng dụng ở lớp biên.

## Bước 1. Tạo distribution

- Mở CloudFront Console.
- Chọn **Create distribution**.

![Create distribution](/images/5-Workshop/placeholder.svg)

## Bước 2. Điền thông tin

**Origin settings**:

- **Origin domain**: Nhập DNS name của ALB (`soc-platform-alb-xxxxx.region.elb.amazonaws.com`)
- **Protocol**: Chọn **HTTP only**
- **HTTP port**: 80
- **Add custom header**:
  - **Header name**: `X-Custom-Header`
  - **Value**: `soc-platform-verified`

**Default cache behavior**:

- **Viewer protocol policy**: Chọn **Redirect HTTP to HTTPS**
- **Allowed HTTP methods**: Chọn **GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE**
- **Cache policy**: Chọn **CachingDisabled**
- **Origin request policy**: Chọn **AllViewer**
- **Compress objects automatically**: Chọn **Yes**

**Web Application Firewall (WAF)**:

- Chọn **Enable security protections**
- **Use existing WAF configuration**: Chọn `soc-platform-web-acl`

**Settings**:

- **Price class**: Chọn **Use all edge locations**
- **Standard logging**: Chọn **On**
- **S3 bucket**: Chọn `soc-platform-logs-<account-id>`
- **Log prefix**: Nhập `cloudfront-logs/`
- **Supported HTTP versions**: Chọn **HTTP/2** và **HTTP/3**

Click **Create distribution**

![Distribution form](/images/5-Workshop/placeholder.svg)

## Validation

- Distribution đã được tạo.
- Traffic có thể đi qua CloudFront.

![Validation](/images/5-Workshop/placeholder.svg)

## Chuyển sang bước tiếp theo

Tiếp theo, bạn sẽ cấu hình logging cho WAF.
