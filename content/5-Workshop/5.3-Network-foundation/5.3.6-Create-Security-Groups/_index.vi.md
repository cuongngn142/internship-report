---
title: 'Tạo Security Group'
date: 2026-07-09
weight: 10
chapter: false
pre: ' <b> 5.3.6. </b> '
---

## Mục tiêu

Tạo các security group để kiểm soát lưu lượng vào/ra.

## Giải thích dịch vụ

Security group là firewall ở cấp instance. Bạn cần thêm rule phù hợp cho ALB và application tier.

## Bước 1. Tạo security group cho ALB

Mở **EC2 console**, trên thanh điều hướng bên trái, chọn **Security Groups**, click **Create security group**

Trong giao diện cấu hình:

- **Security group name**: Nhập `soc-platform-alb-sg`
- **Description**: Nhập `Security group for Application Load Balancer`
- **VPC**: Chọn `soc-platform-vpc`

![ALB SG](/images/5-Workshop/placeholder.svg)

## Bước 2. Thêm rule cho ALB SG

**Inbound rules**, click **Add rule**:
| Type | Protocol | Port Range | Source | Description |
|------|----------|------------|--------|-------------|
| HTTPS | TCP | 443 | 0.0.0.0/0 | HTTPS from CloudFront |
| HTTP | TCP | 80 | 0.0.0.0/0 | HTTP redirect |

Click **Create security group**

![ALB SG rules](/images/5-Workshop/placeholder.svg)

## Bước 3. Tạo security group cho ứng dụng

Click **Create security group**:

- **Security group name**: Nhập `soc-platform-app-sg`
- **Description**: Nhập `Security group for SOC Application Server`
- **VPC**: Chọn `soc-platform-vpc`

**Inbound rules**, click **Add rule**:
| Type | Protocol | Port Range | Source | Description |
|------|----------|------------|--------|-------------|
| Custom TCP | TCP | 8080 | soc-platform-alb-sg | Application port from ALB |

**Outbound rules**, xóa rule mặc định và thêm:
| Type | Protocol | Port Range | Destination | Description |
|------|----------|------------|-------------|-------------|
| HTTPS | TCP | 443 | 0.0.0.0/0 | HTTPS to AWS APIs |

Click **Create security group**

![App SG](/images/5-Workshop/placeholder.svg)

## Bước 4. Tạo Isolation Security Group

Click **Create security group**:

- **Security group name**: Nhập `soc-platform-isolation-sg`
- **Description**: Nhập `Isolation security group - no traffic allowed`
- **VPC**: Chọn `soc-platform-vpc`

**Xóa tất cả Inbound rules và Outbound rules** (để hoàn toàn cô lập)

Click **Create security group**

![App SG](/images/5-Workshop/placeholder.svg)

## Validation

- ALB SG cho phép traffic từ Internet.
- App SG chỉ cho phép traffic từ ALB.
- Security Group `soc-platform-isolation-sg` đã được tạo thành công.
- `soc-platform-alb-sg` cho phép HTTP (80) và HTTPS (443) từ `0.0.0.0/0`.
- `soc-platform-app-sg` chỉ cho phép HTTP (80) từ `soc-platform-alb-sg`.
- `soc-platform-isolation-sg` không có Inbound rules và không có Outbound rules.
- Cả ba Security Group đều thuộc VPC `soc-platform-vpc`.

![Validation](/images/5-Workshop/placeholder.svg)

## Chuyển sang bước tiếp theo

Tiếp theo, bạn sẽ tạo Application Load Balancer.
