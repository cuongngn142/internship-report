---
title: 'Blog 1'
date: 2024-07-07
weight: 1
chapter: false
pre: ' <b> 3.1. </b> '
---

# Customize Federated Sign-In with the Inbound Federation Lambda Trigger in Amazon Cognito

When building applications that use Federated Sign-In with Amazon Cognito, developers commonly integrate authentication through Google, Microsoft Entra ID (Azure AD), Facebook, or other external Identity Providers (IdPs). However, once an IdP successfully authenticates a user, Amazon Cognito processes and stores the user information almost immediately. As a result, tasks such as normalizing user attributes, filtering groups, or automatically linking accounts often require additional backend logic or the use of other Lambda triggers that are not specifically designed for this purpose.

In this blog, AWS introduces the **Inbound Federation Lambda Trigger**, a new Amazon Cognito Lambda Trigger that allows developers to intercept and modify user data received from an Identity Provider before Cognito creates or updates the user profile in the User Pool. This feature simplifies integration with external identity systems, reduces backend processing logic, and provides greater flexibility over the Federated Sign-In workflow.

---

## Overview of the Inbound Federation Lambda Trigger

The Inbound Federation Lambda Trigger is invoked after a user successfully authenticates with an Identity Provider and before Amazon Cognito writes the user information into the User Pool.

At this stage, the Lambda function has access to information such as:

- User Pool ID
- App Client ID
- Identity Provider being used
- Authentication protocol (SAML, OIDC, Login with Amazon, etc.)
- All user attributes returned by the Identity Provider

Based on this information, developers can:

- Normalize user attributes
- Add or remove attributes
- Filter group memberships
- Call external APIs
- Automatically link user accounts

After the Lambda function completes its processing, Amazon Cognito continues by creating or updating the user profile and issuing the Access Token, ID Token, and Refresh Token to the application.

---

## Authentication Workflow

Compared with the traditional Federated Sign-In process, the authentication workflow remains almost unchanged. Users are still redirected to the Identity Provider for authentication.

The main difference is that after the Identity Provider returns the authenticated user information, Amazon Cognito invokes the Inbound Federation Lambda Trigger before storing the data in the User Pool.

The workflow consists of the following steps:

1. The user signs in through an Identity Provider.
2. Amazon Cognito redirects the user to the IdP.
3. The Identity Provider authenticates the user and returns the user information.
4. Amazon Cognito invokes the Inbound Federation Lambda Trigger.
5. The Lambda function validates, transforms, or enriches the user data.
6. Amazon Cognito updates the User Pool.
7. Amazon Cognito issues authentication tokens to the application.

This extension point allows all user information to be processed before it is stored in Amazon Cognito.

---

## Common Use Cases

### Filtering Large Group Attributes

In many B2B and SaaS environments, an Identity Provider may return hundreds of group memberships for a single user.

If all of these groups are stored in Amazon Cognito, the attribute size may exceed the User Pool limits, causing the authentication process to fail.

For example, an Active Directory environment may return more than 200 groups, while the application only requires two groups for authorization. The Lambda Trigger can remove unnecessary groups before Cognito stores the user profile, reducing redundant data and ensuring a successful authentication process.

---

### Automatic Account Linking

In B2C applications, users may initially register using an email address and password, then later choose to sign in with Google or Facebook.

Without account linking, Amazon Cognito creates multiple user profiles for the same individual.

The Inbound Federation Lambda Trigger can identify an existing account based on the user's email address or other unique attributes and automatically link the external Identity Provider to that account.

As a result, users maintain a single profile in the Cognito User Pool, and all application data remains consistent across authentication methods.

---

### User Attribute Normalization and Data Enrichment

Different Identity Providers may use different attribute names, such as:

- given_name
- first_name
- displayName

The Lambda Trigger can normalize these attributes into a consistent format before they are stored in the User Pool.

Additionally, the Lambda function can retrieve extra information from external systems, including:

- Roles
- Permissions
- Departments
- Tenants
- Subscription details

This additional information can be added to the user profile before Amazon Cognito issues authentication tokens.

---

## Implementation Best Practices

When implementing the Inbound Federation Lambda Trigger, AWS recommends following several best practices:

- Design Lambda functions to execute quickly and minimize authentication latency.
- Use caching when external API calls are required.
- Monitor performance using Amazon CloudWatch.
- Configure alarms for Lambda exceptions and timeout events.
- Be aware that Apple Sign In may use private relay email addresses, making automatic account linking difficult. In such cases, a manual account-linking workflow should be provided.

---

## Conclusion

The Inbound Federation Lambda Trigger is a new Amazon Cognito feature that extends the Federated Sign-In workflow by allowing developers to process user data before it is stored in the User Pool. Instead of implementing additional backend logic, developers can normalize user attributes, filter group memberships, enrich user information from external systems, and automatically link accounts directly within the authentication flow.

For B2B, SaaS, and B2C applications that rely on Federated Authentication, this feature provides a flexible and efficient way to integrate external Identity Providers, simplify identity management, and improve the overall user authentication experience.

---

## Original Article

https://aws.amazon.com/blogs/security/customize-federated-sign-in-with-new-amazon-cognito-lambda-trigger/
