---
title: "Rapyd Platform"
slug: "rapyd-platform"
excerpt: "Rapyd provides the following platforms for fintech-as-a-service:\n* **Payments** - Moving money to and from Rapyd wallets.\n* **Point of Sale** - Handling cash at retail locations.\n\nEach platform has a production environment and also a sandbox for testing purposes. The sandbox is a simulator that approximates the behavior of the production environment."
hidden: false
createdAt: "2018-09-02T12:27:09.447Z"
updatedAt: "2021-04-14T10:03:11.296Z"
---
[block:callout]
{
  "type": "danger",
  "title": "Important",
  "body": "The production environment provides only the features and pay methods that are specified in your contract with Rapyd.\n\nThe sandbox enables you to test all features and pay methods.\n\nWhen you are ready to add more pay methods, use the Client Portal. Note that some pay methods require extra steps."
}
[/block]

[block:api-header]
{
  "title": "Payment Platform"
}
[/block]
**Production**

The production platform for payments is a commercial platform that processes actual monetary transactions. Use this environment after testing is complete. Relevant to clients.

* Base URL: **https:/&#47;api.rapyd.net**

**Sandbox**

The sandbox is a test environment for use by the client. Use this environment for all testing and demonstrations. You can set up one sandbox per email address. Data produced in a sandbox can be used only in that specific sandbox.

There are limitations to the ability of the sandbox simulator to mimic the behavior of the production environment. For example, a card issuer might have a limit on the number of times a card can be used in any one 24-hour period. A card transaction that violates that limit might succeed in the sandbox but fail in the real world. 

Similarly, if there are problems with the API request, there might be differences between the error codes in the sandbox and the error codes for various actual pay methods.

* Base URL: **https:/&#47;sandboxapi.rapyd.net**

[block:api-header]
{
  "title": "Point of Sale Platform"
}
[/block]
**Production**

The production platform for POS is a commercial platform for ATMs and other retail locations that handle cash transactions. Relevant to Rapyd partners.

* Base URL: **https:/&#47;pos.rapyd.net**

**Sandbox**

The sandbox is a test environment for ATMs and other retail locations that handle cash transactions. Data produced in a sandbox can be used only in that specific sandbox. Relevant to Rapyd partners.

* Base URL: **https:/&#47;sandboxpos.rapyd.net**

To set up a production environment and sandbox for the Point-of-Sale API, contact **[Rapyd Client Support](https://support.rapyd.net)**.