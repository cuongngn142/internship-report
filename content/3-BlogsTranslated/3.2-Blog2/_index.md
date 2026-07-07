---
title: "Blog 2"
date: 2024-07-07
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# Adding a Voice Layer to WhatsApp Conversations with AWS End User Messaging

Businesses around the world use WhatsApp as one of the primary channels to communicate with customers. It is a familiar, trusted, and efficient platform for many scenarios, including appointment confirmations, customer support, notifications, and business interactions. However, most conversations today still rely entirely on text messages.

Although text messaging is convenient, there are situations where typing is slow, inconvenient, or unable to clearly express a user's intent. In these cases, voice messages provide a more natural and efficient communication method.

This blog introduces how **AWS End User Messaging** enables businesses to receive and respond to WhatsApp voice messages. By combining AWS services such as AWS Lambda, Amazon Transcribe, Amazon Polly, and Amazon SNS, organizations can build voice-to-voice messaging solutions without implementing real-time voice calls.

---

## Why Voice Messages Matter

Text messaging remains an essential communication method, but voice notes offer several unique advantages.

Some of the main benefits include:

- Richer communication through tone, emotion, and emphasis.
- Faster communication, as speaking is generally much quicker than typing on a mobile device.
- Improved accessibility for elderly users or users with visual impairments.
- Greater flexibility by allowing customers to choose between voice and text depending on the situation.

Rather than replacing text messaging, voice messages complement existing conversations and improve the overall customer experience.

---

## Common Use Cases

Voice messaging is particularly valuable in situations where speaking is more convenient than typing.

Typical use cases include:

- Elderly users who prefer listening and speaking.
- Field workers and delivery drivers who cannot easily type while working.
- Healthcare applications where patients describe symptoms more naturally through speech.
- Restaurants and travel services where customers can quickly make reservations.
- Customer support scenarios involving complex issues that are easier to explain verbally.

These scenarios demonstrate how voice messaging can improve both communication efficiency and customer satisfaction.

---

## AWS End User Messaging and WhatsApp

AWS End User Messaging is a fully managed AWS service that enables businesses to send and receive messages across multiple communication channels, including:

- WhatsApp
- SMS
- MMS (United States only)
- Outbound Voice
- Push Notifications

For WhatsApp messaging, incoming messages are automatically delivered to an Amazon SNS topic, allowing seamless integration with other AWS services such as:

- Amazon SNS
- Amazon SQS
- AWS Lambda
- Amazon Bedrock

This event-driven architecture makes it easy to process both text and voice messages using serverless services.

For voice messaging, developers can combine several AWS AI services:

- Amazon Transcribe for Speech-to-Text conversion.
- Amazon Polly for Text-to-Speech synthesis.
- Third-party speech recognition models such as Whisper through the Amazon Bedrock Marketplace.

---

## Voice-to-Voice Messaging Architecture

The flexibility of AWS End User Messaging enables businesses to build complete voice-to-voice messaging workflows.

The process consists of the following steps:

1. A customer sends a voice message through WhatsApp.
2. AWS End User Messaging receives the message.
3. Amazon SNS publishes the inbound event.
4. AWS Lambda downloads and processes the audio.
5. Amazon Transcribe (or Whisper) converts speech into text.
6. The chatbot or conversational application processes the request.
7. Amazon Polly converts the response into natural speech.
8. AWS End User Messaging sends the generated voice message back to the customer through WhatsApp.

Because this solution processes recorded audio asynchronously, it is different from real-time voice calling.

---

## Sample Solution

AWS provides an open-source AWS CDK project that demonstrates this architecture.

The sample project performs the following tasks:

- Receive WhatsApp voice messages.
- Convert speech into text.
- Process the request using chatbot logic.
- Generate a natural voice response.
- Send the audio response back through WhatsApp.

The solution supports multiple deployment modes:

- Inbound-only messaging
- Outbound-only messaging
- Complete voice-to-voice messaging

Current features include:

- End-to-end encryption using AWS KMS.
- Configurable Amazon SNS topics.
- Choice between Amazon Transcribe and Whisper for speech recognition.
- Optional text-to-speech generation with Amazon Polly.
- Support for both voice and text conversations.

---

## Getting Started

The complete solution is available as an open-source AWS CDK project.

Before deployment, you need:

- An AWS account with appropriate permissions.
- Node.js version 18 or later.
- AWS CDK CLI installed.
- A WhatsApp Business Account registered with AWS End User Messaging.

When registering the WhatsApp Business Account, a Meta Business account must be created. The phone number used for registration must not have been previously associated with a personal WhatsApp account. After registration, the WhatsApp Business application should be activated using the same phone number.

---

## Deployment

To deploy the solution, first clone the sample repository and install the required dependencies.

```
npm install
```

Next, configure your WhatsApp Phone Number ID in the `config.params.json` file. If it has not been configured, AWS CDK will prompt you during deployment.

Build the project:

```
npm run build
```

Deploy the infrastructure:

```
cdk deploy
```

The CDK stack automatically provisions all required AWS resources, including:

- AWS Lambda functions
- Amazon SNS topics
- Amazon S3 buckets
- IAM roles

For detailed configuration instructions, refer to the GitHub repository provided by AWS.

When the solution is no longer needed, remove all deployed resources to avoid unnecessary charges:

```
cdk destroy
```

---

## Conclusion

Voice messaging has become a common communication method for personal conversations on WhatsApp. Bringing the same capability into business messaging allows organizations to provide interactions that are more natural, accessible, and engaging.

By combining AWS End User Messaging with services such as AWS Lambda, Amazon Transcribe, Amazon Polly, and Amazon SNS, developers can build scalable voice-enabled customer communication solutions without changing the way customers interact with their business.

The AWS CDK sample project provides an excellent starting point for experimenting with voice-to-voice messaging and extending the solution to meet real business requirements.

---

## Original Article

https://aws.amazon.com/blogs/messaging-and-targeting/adding-a-voice-layer-to-whatsapp-conversations-with-aws-end-user-messaging/