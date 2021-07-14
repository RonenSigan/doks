---
title: "Webhook Security"
slug: "webhook-security"
hidden: false
createdAt: "2019-12-10T23:57:55.315Z"
updatedAt: "2020-08-27T14:37:26.149Z"
---
Webhooks from the Rapyd platform have the following layers of protection against interception and tampering:
* **Secure transfer protocol** - Webhooks are sent with the HTTPS protocol.
* **Signature** - All webhooks are signed. Your unique access key and secret key are used in the calculation of the signature. See [Webhook Signatures](ref:webhook-signatures).
* **Timestamp** - All webhooks are timestamped with the actual current time.
* **IP whitelist** - You can add Rapyd's IP to your whitelist.
[block:api-header]
{
  "title": "Additional Information"
}
[/block]
For more information about access keys and secret keys, see [Access Keys](doc:access-keys).