---
title: 'Create a WAF Web ACL'
date: 2026-07-09
weight: 30
chapter: false
pre: ' <b> 5.8.1. </b> '
---

## Objective

Create a Web ACL to block malicious requests before they reach the application.

## Service explanation

AWS WAF helps control requests to your application using rules based on IP addresses, headers, rate limits, and request patterns.

**Note:** A WAF Web ACL for CloudFront must be created in the **US East (N. Virginia) (`us-east-1`)** Region.

## Step 1. Open the WAF Console

Open the **AWS WAF Console** (switch to the **N. Virginia (`us-east-1`)** Region), then click **Create web ACL**.

![Create WAF](/images/5-Workshop/placeholder.svg)

## Step 2. Fill in the fields

**Describe web ACL and associate it to AWS resources**:

- **Resource type**: Select **Amazon CloudFront distributions**.
- **Name**: Enter `soc-platform-web-acl`.
- **CloudWatch metric name**: Enter `soc-platform-waf-metrics`.
- Click **Next**.

![WAF form](/images/5-Workshop/placeholder.svg)

## Step 3. Add rules and rule groups

Click **Add rules** → **Add managed rule groups**.

| Rule Group                                       | Priority |
| ------------------------------------------------ | -------: |
| AWS managed rule groups → Core rule set          |        1 |
| AWS managed rule groups → Known bad inputs       |        2 |
| AWS managed rule groups → SQL database           |        3 |
| AWS managed rule groups → Linux operating system |        4 |
| AWS managed rule groups → Bot Control            |        6 |

Click **Add rules** → **Add my own rules and rule groups**.

- **Rule type**: Select **Rule builder**.
- **Name**: Enter `RateLimitRule`.
- **Type**: Select **Rate-based rule**.
- **Rate limit**: `2000`.
- **Action**: **Block**.
- **Priority**: `5`.

**Set rule priority**:

- Arrange the rules according to the priority order.

**Default web ACL action**:

- Select **Allow**.

Click **Next** → **Create web ACL**.

![WAF rules](/images/5-Workshop/placeholder.svg)

## Validation

- The Web ACL has been created.
- Malicious requests can be blocked according to the configured rules.

![Validation](/images/5-Workshop/placeholder.svg)

## Next step

Next, you will create a CloudFront distribution.
