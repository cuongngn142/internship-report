---
title: 'Tạo WAF Web ACL'
date: 2026-07-09
weight: 30
chapter: false
pre: ' <b> 5.8.1. </b> '
---

## Mục tiêu

Tạo Web ACL để chặn request độc hại trước khi tới ứng dụng.

## Giải thích dịch vụ

AWS WAF giúp kiểm soát request tới ứng dụng bằng rule dựa trên IP, header, rate limit và pattern.

**Lưu ý**: WAF cho CloudFront phải được tạo ở region **us-east-1**

## Bước 1. Mở WAF Console

Mở **AWS WAF console** (chọn region **N. Virginia - us-east-1**), click **Create web ACL**

![Create WAF](/images/5-Workshop/placeholder.svg)

## Bước 2. Điền thông tin

**Describe web ACL and associate it to AWS resources**:

- **Resource type**: Chọn **Amazon CloudFront distributions**
- **Name**: Nhập `soc-platform-web-acl`
- **CloudWatch metric name**: Nhập `soc-platform-waf-metrics`
- Click **Next**

![WAF form](/images/5-Workshop/placeholder.svg)

## Bước 3. Thêm rule và rule groups

Click **Add rules** → **Add managed rule groups**:

| Rule Group                                       | Priority |
| ------------------------------------------------ | -------- |
| AWS managed rule groups → Core rule set          | 1        |
| AWS managed rule groups → Known bad inputs       | 2        |
| AWS managed rule groups → SQL database           | 3        |
| AWS managed rule groups → Linux operating system | 4        |
| AWS managed rule groups → Bot Control            | 6        |

Click **Add rules** → **Add my own rules and rule groups**:

- **Rule type**: Chọn **Rule builder**
- **Name**: Nhập `RateLimitRule`
- **Type**: Chọn **Rate-based rule**
- **Rate limit**: 2000
- **Action**: Block
- **Priority**: 5

**Set rule priority**: Sắp xếp theo thứ tự priority

**Default web ACL action**: Chọn **Allow**

Click **Next** → **Create web ACL**

![WAF rules](/images/5-Workshop/placeholder.svg)

## Validation

- Web ACL đã được tạo.
- Request độc hại có thể bị chặn theo rule.

![Validation](/images/5-Workshop/placeholder.svg)

## Chuyển sang bước tiếp theo

Tiếp theo, bạn sẽ tạo CloudFront distribution.
