---
title: "Webhooks"
slug: "webhooks"
hidden: false
createdAt: "2018-07-25T12:02:24.386Z"
updatedAt: "2021-02-23T11:49:05.088Z"
---
A **webhook** is a callback that is triggered by an event in the Payments platform. It contains all relevant information about that trigger event. To receive webhooks, you must configure your account with the URL you want the webhooks to go to. See [Defining a Webhook Endpoint] (https://docs.rapyd.net/client-portal/docs/defining-a-webhook-endpoint). Use the 'type' field in the webhooks to filter them or route them for further processing.
[block:api-header]
{
  "title": "Trigger Events"
}
[/block]
A **synchronous trigger event** occurs at the same time as the HTTP request and response. The synchronous webhook contains exactly the same information as the response. You can use synchronous webhooks to confirm the content of the response.

An **asynchronous trigger event** occurs after the request-response cycle is complete. For example, payment by cash requires the end-user customer to physically transfer cash into the Rapyd system at a point-of-sale ([*POS*](ref:glossary)) location. The payment object is created in the system and the response is sent, but the payment is not complete until the cash is received and registered. That trigger event causes Rapyd to send a webhook with the appropriate notification.
[block:api-header]
{
  "title": "Uses of Webhooks"
}
[/block]
The merchant can use the webhook notifications for any purpose, including the following:
* Finalizing a transaction.
* An audit trail.
* A secondary method for tracking or synchronizing transactions.
* Fraud detection and prevention.

[block:api-header]
{
  "title": ""
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Note",
  "body": "In this reference document, individual asynchronous webhooks appear together with the features they relate to. Synchronous webhooks are not documented because they contain the same information as the responses."
}
[/block]