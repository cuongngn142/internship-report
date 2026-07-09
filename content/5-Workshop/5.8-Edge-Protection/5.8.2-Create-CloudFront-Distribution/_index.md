---
title: 'Step 2: Create a CloudFront Distribution'
date: 2026-07-09
weight: 31
chapter: false
pre: ' <b> 5.8.2. </b> '
---

## Objective

Create a CloudFront distribution to deliver content and protect the origin.

## Service explanation

Amazon CloudFront is AWS's content delivery network (CDN) that reduces latency and protects applications at the edge.

## Step 1. Create the distribution

- Open the **CloudFront Console**.
- Select **Create distribution**.

![Create distribution](/images/5-Workshop/placeholder.svg)

## Step 2. Fill in the fields

**Origin settings**:

- **Origin domain**: Enter the DNS name of the ALB (`soc-platform-alb-xxxxx.region.elb.amazonaws.com`).
- **Protocol**: Select **HTTP only**.
- **HTTP port**: `80`.
- **Add custom header**:
  - **Header name**: `X-Custom-Header`.
  - **Value**: `soc-platform-verified`.

**Default cache behavior**:

- **Viewer protocol policy**: Select **Redirect HTTP to HTTPS**.
- **Allowed HTTP methods**: Select **GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE**.
- **Cache policy**: Select **CachingDisabled**.
- **Origin request policy**: Select **AllViewer**.
- **Compress objects automatically**: Select **Yes**.

**Web Application Firewall (WAF)**:

- Select **Enable security protections**.
- **Use existing WAF configuration**: Select `soc-platform-web-acl`.

**Settings**:

- **Price class**: Select **Use all edge locations**.
- **Standard logging**: Select **On**.
- **S3 bucket**: Select `soc-platform-logs-<account-id>`.
- **Log prefix**: Enter `cloudfront-logs/`.
- **Supported HTTP versions**: Select **HTTP/2** and **HTTP/3**.

Click **Create distribution**.

![Distribution form](/images/5-Workshop/placeholder.svg)

## Validation

- The distribution has been created.
- Traffic can be routed through CloudFront.

![Validation](/images/5-Workshop/placeholder.svg)

## Next step

Next, you will configure logging for AWS WAF.
