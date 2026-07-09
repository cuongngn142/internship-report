---
title: 'Create a VPC'
date: 2026-07-09
weight: 5
chapter: false
pre: ' <b> 5.3.1. </b> '
---

## Objective

Create a dedicated VPC for the workshop.

## Service explanation

Amazon VPC allows you to create a private virtual network that is isolated from other AWS resources.

## Step 1. Open the VPC console

1. Open the **Amazon VPC Console**.
2. In the navigation pane on the left, select **Your VPCs**, then click **Create VPC**.

![Search VPC](/images/5-Workshop/5.3-Vpc/vpc-console.png)

## Step 2. Click Create VPC

- Select **VPC only**.
- **Name tag**: Enter `soc-platform-vpc`.
- **IPv4 CIDR block**: Enter `10.0.0.0/16`.
- **IPv6 CIDR block**: Select **No IPv6 CIDR block**.
- **Tenancy**: Select **Default**.
- Leave all other settings as their default values, then click **Create VPC**.

![Create button](/images/5-Workshop/5.3-Vpc/create-vpc.PNG)

## Step 3. Fill in the fields

After the VPC has been created, select the newly created VPC and choose **Actions** → **Edit VPC settings**.

- Check **Enable DNS hostnames**.
- Check **Enable DNS resolution**.
- Click **Save**.

![Advanced settings](/images/5-Workshop/5.3-Vpc/vpc-setting1.png)

## Step 4. Configure advanced settings

- The VPC `soc-platform-vpc` has been created.
- Its status is **Available**.

![Validation](/images/5-Workshop/5.3-Vpc/vpc-setting2.png)

## Validation

Next, you will create an Internet Gateway.
