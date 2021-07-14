---
title: "Rapyd API Reference Guide"
slug: "rapyd-api-reference-guide"
excerpt: "The API Reference Guide provides technical descriptions of the Rapyd Payments API and Point of Sale API. All methods are fully documented, including working examples. Also describes webhooks and error messages."
hidden: false
createdAt: "2018-09-06T07:16:14.874Z"
updatedAt: "2021-06-27T13:12:03.519Z"
---
[block:callout]
{
  "type": "success",
  "body": "The Payments API is relevant to Rapyd clients.\n\nThe POS API is relevant to point-of-sale locations, such as ATMs and retail stores that handle cash transactions for  Rapyd Wallets.",
  "title": "Audience"
}
[/block]
Reference topics in this document:
[block:api-header]
{
  "title": "General Topics"
}
[/block]
* [Rapyd Platform](ref:rapyd-platform) - Rapyd provides a production platform and a sandbox environment.
* [Information Security](ref:information-security) - Rapyd is certified as a Level 1 service provider by the Payment Card Industry (PCI) Data Security Standard. Rapyd is also certified as complaint with the ISO/IEC 27001 standard.
* [Message Security](ref:message-security) - Rapyd uses several methods to ensure that communications with the platform are protected from interception and tampering.
* [Webhooks](ref:webhooks) - The Rapyd platform generates messages in response to asynchronous events, such as a consumer completing a payment at a later time.
* [Error Messages](ref:error-messages) - The structure and content of the API's built-in context-sensitive help. General errors, file errors and FX errors are discussed here. Error messages that are specific to a single group of methods appear at the end of the group.
[block:api-header]
{
  "title": "Rapyd Collect"
}
[/block]
Collecting funds from many different payment sources and transferring it to Rapyd Wallets.

* [Rapyd Collect Overview](ref:rapyd-collect-overview) - Payments, group payments, escrows and refunds.
[block:api-header]
{
  "title": "Rapyd Disburse"
}
[/block]
Paying funds out of a Rapyd Wallet to various types of beneficiaries.

* [Rapyd Disburse Overview](ref:rapyd-disburse-overview) - Payouts to configured payout methods and payouts to service providers.
[block:api-header]
{
  "title": "Rapyd Wallet"
}
[/block]
The source of payouts and where payments are deposited.

* [Rapyd Wallet Overview](ref:rapyd-wallet-overview) - Rapyd wallets, contacts, transfer transactions, transaction reports, currency exchange, virtual bank accounts and identity verification.
[block:api-header]
{
  "title": "Rapyd Issuing"
}
[/block]
Interfacing Rapyd Wallets with traditional banking services.

* [Rapyd Issuing Overview](ref:rapyd-issuing-overview) - Issuing cards to Rapyd wallets.
[block:api-header]
{
  "title": "Testing Methods"
}
[/block]
Special topics of interest to client developers.

* [Testing for Payments API](ref:testing-for-payments-api) - Error simulation, adding and withdrawing funds.
[block:api-header]
{
  "title": "Point-of-Sale API"
}
[/block]
An API for physical locations that handle cash for Rapyd wallets, such as ATMs and retail stores. 

* [Point-of-Sale API Overview](ref:point-of-sale-api-overview) - Methods for accepting and disbursing cash.
[block:api-header]
{
  "title": "Glossary"
}
[/block]
* [Glossary](ref:glossary) - Terms used in this reference guide.