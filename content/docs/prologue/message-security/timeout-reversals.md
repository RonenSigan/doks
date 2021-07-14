---
title: "Timeout Reversals"
slug: "timeout-reversals"
hidden: true
createdAt: "2020-01-14T00:48:59.214Z"
updatedAt: "2020-06-10T06:13:37.274Z"
---
The timeout reversal process relates to card issuance and card processing. 
When the issuer doesn't respond in the stipulated time (<=300 ms) and there is a general delay in the network processing, the Merchant Terminals or the Merchant's Acquirer can timeout and subsequently send us a timeout reversal (TOR) message to cancel the previous request for authorization. 
Rapyd acknowledges and responds back to all TOR messages from the network.

Rapyd will also respond with error '96' if **StandIn** is available..
[block:api-header]
{
  "title": "Code Examples"
}
[/block]

[block:api-header]
{
  "title": "Related Information"
}
[/block]
* [Webhook Signatures](ref:webhook-signatures) - Describes the formula for calculating a signature for webhooks.