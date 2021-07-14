---
title: "Webhook Signatures"
slug: "webhook-signatures"
excerpt: "When Rapyd sends you a webhook, the webhook includes a signature. You can verify the integrity of the message by calculating the signature yourself and comparing it with the value you received in the webhook. If the values do not match, contact **[Rapyd Client Support](https://support.rapyd.net)**."
hidden: false
createdAt: "2019-12-08T15:04:42.734Z"
updatedAt: "2021-04-22T06:47:45.611Z"
---
[block:api-header]
{
  "title": "Calculation of Signature"
}
[/block]
The signature is calculated as a hash of a concatenation of specific strings, according to the following formula:

 ** *signature* = BASE64 ( HASH ( *url_path* + *salt* + *timestamp* + *access_key* + *secret_key* + *body_string* ) )**

where:
* ***BASE64*** is a Base-64 encoding algorithm.
* ***HASH*** is HMAC-SHA256.

* ***url_path*** is the entire URL that was configured for your company to receive webhooks. See [Defining a Webhook Endpoint](/client-portal/docs/defining-a-webhook-endpoint).
* ***salt*** is a random numeric string for each request. Length: 8-16 digits.
* ***timestamp*** is the time the webhook was sent, in [*Unix time*](ref:glossary). The Rapyd platform is synchronized to the actual current time, as defined by public NTP servers. See [*NTP*](ref:glossary).
* ***access_key*** is the access key for your organization, assigned by Rapyd.
* ***secret_key*** is the secret key for your organization, assigned by Rapyd. The secret key is like a password, and is transmitted only as part of the calculated signature. Do not share it with your customers or partners, and do not transmit it in plaintext.
* ***body_string*** is a valid JSON string.
[block:callout]
{
  "type": "warning",
  "title": "Note",
  "body": "Different languages handle Base-64 encoding differently. You must adequately test your code so that you are using all the correct Base-64 options to validate the signatures that Rapyd sends."
}
[/block]

[block:api-header]
{
  "title": "Related Information"
}
[/block]
* [Request Signatures](ref:request-signatures) - Describes the formula for calculating signatures for requests to the Rapyd platform. Provides code examples.