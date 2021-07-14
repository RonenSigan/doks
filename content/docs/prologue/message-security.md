---
title: "Message Security"
slug: "message-security"
hidden: false
createdAt: "2018-09-05T12:42:51.244Z"
updatedAt: "2021-05-26T23:19:37.534Z"
---
The REST messages to the Rapyd platform have the following layers of protection against interception and tampering: 
* **Secure transfer protocol** - REST requests and responses are sent with the HTTPS protocol.
* **IP whitelist** - All requests to the production platforms are screened against a list of IP addresses  provided by the client.
* **Message Headers** - All requests require message headers. These headers are documented for each method.
* **Access Keys** - All requests require an access key.
* **Timestamp** - All requests to the Rapyd platform are timestamped with the actual current time. If the timestamp is in the future, or is older than 60 seconds, the request is rejected.
* **Signature** - All requests to the Payment platform are signed. Your unique access key and secret key are used in the calculation of the signature. See [Request Signatures](ref:request-signatures). Webhooks are also signed.
* **Idempotency** - [Create Payment](ref:create-payment) requests are tested for idempotency when they have an `idempotency` header. If communications failures or tampering cause a request to be received twice, the second request is ignored. This protects against double-charging a customer for the same charge. See [Idempotency](ref:idempotency).
[block:api-header]
{
  "title": "Additional Information"
}
[/block]
* [Accounts and Credentials](/client-portal/docs/accounts-and-credentials) - Information about access keys and secret keys.
* [Webhook Security](ref:webhook-security)- Security features in webhooks from Rapyd to the client.