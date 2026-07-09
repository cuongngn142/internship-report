---
title: 'Step 1: Create SNS Topics'
date: 2026-07-09
weight: 24
chapter: false
pre: ' <b> 5.6.1. </b> '
---

## Objective

Create SNS topics to send alerts to email or other systems.

## Service explanation

Amazon SNS is a publish/subscribe messaging service used to send notifications to multiple subscribers.

## Step 1. Create the topic

- Open the **SNS Console**.
- Select **Topics** → **Create topic**.

In the configuration page:

- **Type**: Select **Standard**.
- **Name**: Enter `soc-platform-critical-alerts`.
- **Encryption**: Select **Enable encryption** and choose the KMS key `alias/aws/sns`.
- Click **Create topic**.

![Create SNS topic](/images/5-Workshop/placeholder.svg)

## Step 2. Add a subscription

Click **Create subscription**.

- **Protocol**: Select **Email**.
- **Endpoint**: Enter the SOC team's email address.
- Click **Create subscription**.

![SNS subscription](/images/5-Workshop/placeholder.svg)

## Step 3. Confirm the email

- Confirm the subscription from the email message.

![Confirm email](/images/5-Workshop/placeholder.svg)

## Step 4. Create the High Alerts topic

Repeat the same steps using the name `soc-platform-high-alerts`.

![Confirm email](/images/5-Workshop/placeholder.svg)

## Validation

- The SNS topics have been created.
- The subscriptions are working.

![Validation](/images/5-Workshop/placeholder.svg)

## Next step

Next, you will create Lambda functions.
