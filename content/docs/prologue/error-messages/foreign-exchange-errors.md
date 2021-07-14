---
title: "Foreign Exchange Errors"
slug: "foreign-exchange-errors"
excerpt: "Foreign exchange errors can arise in Rapyd Wallet currency conversion operations, in payments and in payouts."
hidden: false
createdAt: "2019-08-14T14:39:40.645Z"
updatedAt: "2021-01-20T15:27:46.650Z"
---
The following error messages relate to foreign exchange:

**ERROR_DIFFERENT_CURRENCY_REQUIRED**
The request tried to request the daily rate for a currency exchange, but the buy currency and the sell currency were the same. The request was rejected. Corrective action: Set ‘buy_currency’ to a different value from ‘sell_currency’.

**ERROR_CURRENCY_PAIR_NOT_VALID**
The request tried to request the daily rate for a currency exchange, but the buy currency cannot be converted into the selected sell currency. The request was rejected. Corrective action: Contact customer support.

**ERROR_GET_DAILY_RATE_CURRENCY_PAIR_NOT_VALID**
The request tried to request the daily rate for a currency exchange, but the buy currency cannot be converted into the selected sell currency. The request was rejected. Corrective action: Contact customer support.

**ERROR_GET_DAILY_RATE_DIFFERENT_CURRENCY_REQUIRED**
The request tried to request the daily rate for a currency exchange, but the buy currency and the sell currency were the same. The request was rejected. Corrective action: Set ‘buy_currency’ to a different value from ‘sell_currency’.

**ERROR_GET_RATE**
The request attempted an operation that requires currency exchange, but the rate for one or both of the currencies could not be found. The request was rejected. Corrective action: Try the request at a later time.

**ERROR_HOSTED_PAGE_FX_FEE_ONLY_ALLOWED_FOR_FX_TRANSACTIONS**
The request tried to set a foreign exchange fee but the requested payment was not a foreign exchange transaction. The request was rejected. Corrective action: For a payment that does not require foreign exchange, leave 'fx_fee' unset.

**INVALID_EXPIRATION**
The request attempted an operation that requires a forward date, but the date was not found or was not valid. The request was rejected. Corrective action: Provide a forward date that is a valid Unix time, not past, and not more than 1 year in the future.

**INVALID_SOURCE_CURRENCY**
The request attempted an operation that requires a currency code for the result of an FX operation, but the sell currency was not recognized. The request was rejected. Corrective action: Use the correct 3-letter ISO 4217 code for the currency in uppercase letters.