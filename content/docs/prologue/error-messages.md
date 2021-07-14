---
title: "Error Messages"
slug: "error-messages"
hidden: false
createdAt: "2019-08-18T15:21:04.482Z"
updatedAt: "2021-02-04T12:45:13.647Z"
---
If a REST message to the Rapyd platform contains an error that prevents the intended operation, the platform returns an error code and a message. The message explains the cause of the error and the steps that must be taken to correct it.
[block:callout]
{
  "type": "warning",
  "title": "Note",
  "body": "The sandbox simulator does a limited amount of validating the REST requests, but it does not cover every corner case for every pay method. You might experience differences between the error messages that you get in sandbox and production."
}
[/block]
The following error messages apply to two or more objects:
* [General Error Messages](ref:general-error-messages) 
* [File Errors](ref:file-errors) 
* [Foreign Exchange Errors](ref:foreign-exchange-errors) 
* [Hosted Page Errors](ref:hosted-page-errors) 

Error messages relevant to one object:
[block:api-header]
{
  "title": "Rapyd Collect"
}
[/block]
**Collection transactions**
* [Payment Errors](ref:payment-errors) 
* [Group Payment Errors](ref:group-payment-errors) 
* [Escrow Errors](ref:escrow-errors) 
* [Refund Errors](ref:refund-errors) 

**Customers**
* [Customer Errors](ref:customer-errors) 
* [Address Errors](ref:address-errors) 
* [Customer Payment Method Errors](ref:customer-payment-method-errors) 
* [Payment Method Errors](ref:payment-method-errors) 
* [Token Errors](ref:token-errors) 

**Goods and Services**
* [Product Errors](ref:product-errors) 
* [SKU Errors](ref:sku-errors) 
* [Plan Errors](ref:plan-errors)

**Subscriptions and Coupons**
* [Subscription Errors](ref:subscription-errors) 
* [Subscription Item Errors](ref:subscription-item-errors) 
* [Usage Record Errors](ref:usage-record-errors)
* [Coupon Errors](ref:coupon-errors)

**Orders and Invoices**
* [Order Errors](ref:order-errors) 
* [Return Errors](ref:return-object-errors)
* [Invoice Errors](ref:invoice-errors)

**Checkout Page**
* [Checkout Errors](ref:checkout-errors) 
[block:api-header]
{
  "title": "Rapyd Disburse"
}
[/block]
* [Payout Errors](ref:payout-errors) 
* [Service Provider Errors](ref:service-provider-errors) 
[block:api-header]
{
  "title": "Rapyd Wallet"
}
[/block]
* [Wallet Errors](ref:wallet-errors) 
* [Wallet Contact Errors](ref:wallet-contact-errors) 
* [Wallet Transaction Errors](ref:wallet-transaction-errors) 
* [Identity Verification Errors](ref:identity-verification-errors) 
[block:api-header]
{
  "title": "Rapyd Issuing"
}
[/block]
* [Issuing Platform Errors](ref:issuing-platform-errors)
* [Rapyd Authorization Errors](ref:rapyd-authorization-errors) 
* [Rapyd Protect Errors - Rapyd Authorization](ref:rapyd-protect-errors-rapyd-authorization) 
[block:api-header]
{
  "title": "Other"
}
[/block]
* [General Errors](ref:general-errors) 
* [File Errors](ref:file-errors) 
* [Foreign Exchange Errors](ref:foreign-exchange-errors) 
* [Location Errors](ref:location-errors) 
* [Metadata Errors](ref:metadata-errors) 
* [Simulated Errors](ref:simulated-errors)