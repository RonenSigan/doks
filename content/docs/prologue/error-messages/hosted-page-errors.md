---
title: "Hosted Page Errors"
slug: "hosted-page-errors"
excerpt: "Errors can arise from the following hosted page operations:\n* [Create Checkout Page](ref:create-checkout-page) \n* [Create Card Token - Hosted Page](ref:create-card-token-hosted-page) \n* [Create Beneficiary Tokenization Page](ref:create-beneficiary-tokenization-page) \n* [Display Issued Card Details to Customer](ref:display-issued-card-details-to-customer)"
hidden: false
createdAt: "2021-01-19T16:08:18.192Z"
updatedAt: "2021-07-04T08:29:52.844Z"
---
The following error codes are relevant to hosted page operations:

**ERROR_HOSTED_PAGE_COLLECT_CARD_CUSTOMER_NOT_FOUND**
The request attempted a hosted page operation, but the customer was not found. The request was rejected. Corrective action: For 'customer', provide a valid customer ID, a string starting with 'cus_'.

**ERROR_HOSTED_PAGE_COUNTRY_CURRENCY_MISMATCH**
The request tried to create a checkout page, but there is no payment method that is supported in the country for the currency provided. The request was rejected. Corrective action: Use a different currency or country.

**ERROR_HOSTED_PAGE_INVALID_CURRENCY**
The request tried to create a checkout page, but the currency was not recognized. The request was rejected. Corrective action: For the 'currency' field, use the 3-letter ISO 4217 code in uppercase letters.

**ERROR_HOSTED_PAGE_MISSING_CUSTOMER**
The request attempted a hosted page operation, but the customer was not found. The request was rejected. Corrective action: For 'customer', provide a valid customer ID, a string starting with 'cus_'.

**ERROR_HOSTED_PAGE_NO_SUPPORTED_PAYOUT_METHOD_TYPES**
The request attempted a hosted page operation, but there are no supported payout method types for the combination of the attributes that has been specified. The request was rejected. Corrective action: Run 'List Payout Method Types'. Use only supported countries and entity types, and use only currencies that are supported for each country.

**ERROR_HOSTED_PAGE_UNREADABLE_PAYOUT_METHOD_TYPES_INCLUDE_LIST**
The request tried to create a hosted page with a list of payout method types to include, but the data was not recognized. The request was rejected. Corrective action: In 'payout_method_types_include', specify a list of strings, each of which is a payout method type.

**ERROR_HOSTED_PAGE_UNRECOGNIZED_CARD**
The request attempted a hosted page operation, but the card was not recognized or not valid. The request was rejected. Corrective action: For 'card', provide the card token or the issued card ID. The card token starts with 'card_' and the issued card ID starts with 'ci_'.

## Related Information ##
* [Error Messages](ref:error-messages)