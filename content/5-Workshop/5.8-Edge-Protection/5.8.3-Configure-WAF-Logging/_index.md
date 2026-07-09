---
title: 'Configure WAF Logging'
date: 2026-07-09
weight: 32
chapter: false
pre: ' <b> 5.8.3. </b> '
---

## Objective

Enable WAF logging to store allowed and blocked requests.

## Service explanation

WAF logging helps you analyze attacks and optimize your WAF rules.

## Step 1. Enable logging

- Select the Web ACL `soc-platform-web-acl` that you created.
- Go to the **Logging and metrics** tab, then click **Enable logging**.

**Logging destination**:

- **Amazon S3 bucket**: Select `soc-platform-logs-<account-id>`

**Filter logs**:

- **Default behavior**: Select **Drop**
- **Filters**: Add a filter to keep only **BLOCK** actions

Click **Save**.

![WAF logging](/images/5-Workshop/placeholder.svg)

## Validation

- Logging has been enabled.
- Requests can be stored for later analysis.

![Validation](/images/5-Workshop/placeholder.svg)

## Next step

Next, you will proceed to the Testing and Validation section.