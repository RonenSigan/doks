---
title: "General Errors"
slug: "general-errors"
hidden: false
createdAt: "2019-05-14T14:15:51.283Z"
updatedAt: "2021-05-19T07:51:36.443Z"
---
The following error messages appear in the Payment API in connection with more than one type of object.

**EMAIL_IS_VERIFIED**
The request tried to verify the email address of a white level user, but the email was already verified. The request was rejected. Corrective action: Determine why an attempt was made to verify the same email twice.

**ERROR_AMOUNT_MUST_BE_POSITIVE**
The request attempted an operation that requires an amount, but the amount was negative or zero. The request was rejected. Corrective action: Use a positive decimal number.

**ERROR_AMOUNT_NOT_VALID**
The request tried to create a transaction, but the amount was not valid. The request was rejected. Corrective action: Set the amount to a positive decimal number.

**ERROR_BANK_IDENTIFIER_MISMATCH**
The request attempted an operation that requires both an account number and a bank identifier, but the bank portion of the account number does not match the bank identifier. The request was rejected. Corrective action: Verify the account number and bank identifier and retry.

**ERROR_CARD_EXPIRED**
The request attempted an operation that requires a card, but the card expired. The request was rejected. Corrective action: Advise the cardholder to contact the issuer.

**ERROR_CARD_NOT_AUTHENTICATED**
The request tried to use a card ID, but the cardholder has not completed the 3DS verification process. The request was rejected. Corrective action: None. Create a new card ID and wait for the cardholder to complete the 3DS process. To create a new card ID, use 'Create Payment', 'Add Payment Method to Customer' or 'Create Card Token - Hosted Page'.

**ERROR_CARD_TRANSACTION_AMOUNT**
The request attempted an operation to move funds to or from a card, but the transaction amount exceeds the limits set by the card issuer. The request was rejected. Corrective action: Advise the cardholder to contact the issuer.

**ERROR_CARD_TRANSACTION_FREQUENCY**
The request attempted an operation to move funds to or from a card, but the number of times this operation has been attempted exceeds the limits set by the card issuer. The request was rejected. Corrective action: Advise the cardholder to contact the issuer.

**ERROR_CSV_FILE_NOT_VALID**
The request tried to upload a CSV file, but there was a problem with the format of the file. The request was rejected. Corrective action: Use a file that has correct CSV formatting.

**ERROR_DAYS_UNTIL_DUE_NOT_VALID**
The request tried to set or update the 'days_until_due' parameter in an invoice or subscription, but the value was not valid. The request was rejected. Corrective action: Set 'days_until_due' to a positive integer.

**ERROR_GET_CARD**
The request attempted an operation that requires a card ID, but the card was not found. The request was rejected. Corrective action: In the 'card' field, provide the ID or card number of a valid card.

**ERROR_MISSING_COUNTRY**
The request attempted an operation that requires a country, but the country was not found. The request was rejected. Corrective action: For 'country', use the 2-letter ISO 3166-1 ALPHA-2 code, in uppercase letters.

**ERROR_MISSING_EWALLET_CONTACT**
The request attempted an operation that requires an eWallet contact, but the contact was not found. The request was rejected. Corrective action: For 'ewallet_contact', use the ID of a valid eWallet contact, a string starting with 'cont_'.

**ERROR_STATEMENT_DESCRIPTOR_TOO_LONG**
The request attempted an operation that uses a statement descriptor, but it contained too many characters. The request was rejected. Corrective action: For the 'statement_descriptor' body parameter, use a string of 1-22 alphanumeric characters and spaces.

**ERROR_ZERO_AMOUNT**
The request attempted an operation that would result in a zero-amount transaction. The request was rejected. Corrective action: Adjust the split or the amount so that the final amounts are all greater than zero.

**INVALID_ADDRESS_FORMAT**
The request attempted an operation that requires an address, but the request provided an array of addresses. The request was rejected. Corrective action: Use a single 'address' object.

**INVALID_AMOUNT**
The request attempted an operation that requires an amount, but the amount was not found, was not a valid number or was out of bounds. The request was rejected. Corrective action: Use the correct amount.

**INVALID_COUNTRY**
The request attempted an operation that requires a country, but the value was missing or not recognized. The request was rejected. Corrective action: Use the correct 2-letter ISO 3166-1 ALPHA-2 code for the country, in uppercase letters.

**INVALID_COUNTRY_CODE**
The request attempted an operation that requires a country code, but the country code was missing or not recognized. The request was rejected. Corrective action: Use the 2-letter ISO 3166-1 ALPHA-2 country code in uppercase letters.

**INVALID_CURRENCY**
The request attempted an operation that requires a currency, but the value was missing or not recognized. The request was rejected. Corrective action: Use the correct 3-letter ISO 4217 code for the currency in uppercase letters.

**INVALID_CUSTOMER_EMAIL**
The request attempted an operation that requires a valid email address, but the information was not in proper email address format. The request was rejected. Corrective action: Use the correct format for an email address.

**INVALID_DESCRIPTION**
The request attempted an operation that requires a description, but the description was not found. The request was rejected. Corrective action: In the 'description' field, provide a description of the operation.

**INVALID_FIELDS**
The request attempted an operation, but one of the fields contained a value that is not valid. The request was rejected. Corrective action: The name of the field appears at the end of the response code. Use a valid value.

**INVALID_FIRST_NAME**
The request tried to perform an operation that requires the first name of an individual, but the 'first_name' field was blank or invalid. The request was rejected. Corrective action: Provide a valid first name.

**INVALID_LIMIT**
The request tried to retrieve a list of objects, but the 'limit' query parameter was not set to a valid value. The request was rejected. Corrective action: Set 'limit' to an integer between 1 and 100.

**INVALID_NAME**
The request attempted an operation that requires a name, but the 'name' field was missing, empty or not recognized. The request was rejected. Corrective action: Use a valid string.

**INVALID_PAGE_NUMBER**
The request attempted a GET operation that requires a page number, but the value was not recognized. The request was rejected. Corrective action: For 'page_number', use a positive integer.

**INVALID_PHONE_NUMBER**
The request attempted an operation that requires a phone number, but the phone number was missing or not recognized. The request was rejected. Corrective action: Use the correct number in E.164 format.

**INVALID_REGEX_FIELDS**
The request attempted an operation, but one or more of the required fields did not match the expected regular expression pattern. The request was rejected. Corrective action: Use the correct regular expression pattern for all of the fields that are listed at the end of the response code.

**INVALID_ROUTING_NUMBER**
The request attempted an operation that requires a bank routing number, but the number was not recognized. The request was rejected. Corrective action: Use a valid bank routing number.

**INVALID_TOKEN**
The request tried to perform an operation that requires the ID of an object, but the object was not found. The request was rejected. Corrective action: Use a valid 'id' for this operation.

**MISSING_CURRENCIES**
The request attempted an operation that requires a currency, but the currency was not found. The request was rejected. Corrective action: Use the three-letter ISO 4217 code, in uppercase letters.

**MISSING_FIELDS**
The request attempted an operation, but one or more required fields were missing. The request was rejected. Corrective action: Provide all of the fields that are listed at the end of the error code. For more information, see the API Reference.

**MISSING_INVALID_PARAMETERS**
A parameter is missing or contains an invalid value. The request was rejected. Corrective action: Check all input parameters.

**REQUEST_DECLINED**
Your request was declined. For more information, please contact Rapyd Customer Service.

**REQUEST_UNDER_REVIEW**
Your request is under review by Rapyd's operations department. For more information, please contact Rapyd Customer Service.

**SERVICE_TEMPORARILY_UNAVAILABLE**
The request attempted an operation, but the service is temporarily unavailable. The request was rejected. Corrective action: Retry in a few minutes. If the problem persists, contact Rapyd Client Support.