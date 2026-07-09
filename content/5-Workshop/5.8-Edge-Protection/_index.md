---
title: 'Edge Protection'
date: 2026-07-09
weight: 58
chapter: true
pre: '<b>5.8.</b>'
---

# Edge Protection

In this chapter, you will deploy the first layer of protection for the SOC Platform at the edge using Amazon CloudFront and AWS WAF. Requests from the Internet will be inspected, filtered, and protected before being forwarded to the Application Load Balancer. In addition, blocked requests will be logged for security monitoring and investigation.

After completing this chapter, the platform will be able to securely deliver content, mitigate common web-based attacks, and record security events occurring at the edge.

## Implementation steps

### Create an AWS WAF Web ACL

- Create an AWS WAF Web ACL to protect the application.
- Add AWS Managed Rule Groups and a Rate-based Rule.
- Configure the Web ACL to filter and block malicious requests before they reach the application.

### Create an Amazon CloudFront Distribution

- Create a CloudFront Distribution using the Application Load Balancer as the origin.
- Configure HTTPS, cache behavior, and content delivery settings.
- Associate CloudFront with AWS WAF to protect Internet traffic.

### Configure WAF Logging

- Enable logging for AWS WAF.
- Store WAF logs in Amazon S3.
- Collect blocked requests for monitoring, analysis, and security investigations.
