---
title: "Idempotency"
slug: "idempotency"
hidden: false
createdAt: "2019-01-15T13:59:11.360Z"
updatedAt: "2021-06-22T10:39:24.036Z"
---
Rapyd provides an optional idempotency check for [Create Payment](ref:create-payment) requests. To activate the check, include the `idempotency` parameter in the header of the request. If the `idempotency` header is the same in another request in the next 24 hours, and if the `amount` field in the body of the request is the same, the second request is determined to be idempotent and the response to the first request is returned.
[block:callout]
{
  "type": "info",
  "title": "Note",
  "body": "The idempotency check does not examine the value of the `currency` field, so requests for 24.00 euros and 24.00 dollars are idempotent if they use the same `idempotency` header."
}
[/block]

[block:api-header]
{
  "title": "Example #1 - Not idempotent"
}
[/block]
The following example illustrates two requests that use the same `idempotency` header. They are not idempotent because they have different values for `amount`. In the responses, you can see that the `id` field is different.
[block:code]
{
  "codes": [
    {
      "code": "{\n\t\"amount\": 100,\n\t\"currency\": \"USD\",\n\t\"payment_method\": {\n\t\t\"type\": \"us_mastercard_card\",\n\t\t\"fields\": {\n\t\t\t\"number\": \"4111111111111111\",\n\t\t\t\"expiration_month\": \"12\",\n\t\t\t\"expiration_year\": \"23\",\n\t\t\t\"name\": \"John Doe\",\n\t\t\t\"cvv\": \"345\"\n\t\t},\n\t\t\"metadata\": {\n\t\t\t\"merchant_defined\": true\n\t\t}\n\t}\n}",
      "language": "json",
      "name": "Request #1"
    },
    {
      "code": "{\n    \"status\": {\n        \"error_code\": \"\",\n        \"status\": \"SUCCESS\",\n        \"message\": \"\",\n        \"response_code\": \"\",\n        \"operation_id\": \"19072d56-7834-447a-9260-7c8c8da62b06\"\n    },\n    \"data\": {\n        \"id\": \"payment_ab30fc5ed6578b415ca7ba004b34d463\",\n        \"amount\": 100,\n        \"original_amount\": 100,\n        \"is_partial\": false,\n        \"currency_code\": \"USD\",\n        \"country_code\": \"US\",\n        \"status\": \"CLO\",\n        \"description\": \"\",\n        \"merchant_reference_id\": \"\",\n        \"customer_token\": \"cus_1a4df69a959e184fd50884644f46cd73\",\n        \"payment_method\": \"card_1ccfdb70c1b34d68ea2c09a15df1310c\",\n        \"expiration\": \"0\",\n        \"captured\": true,\n        \"refunded\": false,\n        \"refunded_amount\": 0,\n        \"receipt_email\": \"\",\n        \"redirect_url\": \"\",\n        \"complete_payment_url\": \"\",\n        \"error_payment_url\": \"\",\n        \"receipt_number\": \"\",\n        \"flow_type\": \"\",\n        \"address\": null,\n        \"statement_descriptor\": \"\",\n        \"transaction_id\": \"\",\n        \"created_at\": \"1565511756\",\n        \"metadata\": {},\n        \"failure_code\": \"\",\n        \"failure_message\": \"\",\n        \"paid\": true,\n        \"paid_at\": 1565511756,\n        \"dispute\": null,\n        \"refunds\": null,\n        \"order\": null,\n        \"outcome\": null,\n        \"visual_codes\": {},\n        \"textual_codes\": {},\n        \"instructions\": [],\n        \"ewallet_id\": null,\n        \"ewallets\": [],\n        \"payment_method_options\": {},\n        \"payment_method_type\": \"us_mastercard_card\",\n        \"payment_method_type_category\": \"card\",\n        \"fx_rate\": 0,\n        \"merchant_requested_currency\": null,\n        \"merchant_requested_amount\": null,\n        \"payment_fees\": null,\n        \"invoice\": \"\",\n        \"escrow\": null\n    }\n}",
      "language": "json",
      "name": "Response #1"
    },
    {
      "code": "{\n\t\"amount\": 25,\n\t\"currency\": \"USD\",\n\t\"payment_method\": {\n\t\t\"type\": \"us_mastercard_card\",\n\t\t\"fields\": {\n\t\t\t\"number\": \"4111111111111111\",\n\t\t\t\"expiration_month\": \"12\",\n\t\t\t\"expiration_year\": \"23\",\n\t\t\t\"name\": \"John Doe\",\n\t\t\t\"cvv\": \"345\"\n\t\t},\n\t\t\"metadata\": {\n\t\t\t\"merchant_defined\": true\n\t\t}\n\t}\n}",
      "language": "json",
      "name": "Non-idempotent request #2"
    },
    {
      "code": "{\n    \"status\": {\n        \"error_code\": \"\",\n        \"status\": \"SUCCESS\",\n        \"message\": \"\",\n        \"response_code\": \"\",\n        \"operation_id\": \"68dd5bba-3358-408c-9207-5dc73935ab6d\"\n    },\n    \"data\": {\n        \"id\": \"payment_3badcd504599a0630cc4fe87cde8dfb5\",\n        \"amount\": 25,\n        \"original_amount\": 25,\n        \"is_partial\": false,\n        \"currency_code\": \"USD\",\n        \"country_code\": \"US\",\n        \"status\": \"CLO\",\n        \"description\": \"\",\n        \"merchant_reference_id\": \"\",\n        \"customer_token\": \"cus_ed007e7d1d9d2f773f89c175f6b05bfa\",\n        \"payment_method\": \"card_f23c1c0bcfd1019ee4e60e2a7f431420\",\n        \"expiration\": \"0\",\n        \"captured\": true,\n        \"refunded\": false,\n        \"refunded_amount\": 0,\n        \"receipt_email\": \"\",\n        \"redirect_url\": \"\",\n        \"complete_payment_url\": \"\",\n        \"error_payment_url\": \"\",\n        \"receipt_number\": \"\",\n        \"flow_type\": \"\",\n        \"address\": null,\n        \"statement_descriptor\": \"\",\n        \"transaction_id\": \"\",\n        \"created_at\": \"1565511799\",\n        \"metadata\": {},\n        \"failure_code\": \"\",\n        \"failure_message\": \"\",\n        \"paid\": true,\n        \"paid_at\": 1565511799,\n        \"dispute\": null,\n        \"refunds\": null,\n        \"order\": null,\n        \"outcome\": null,\n        \"visual_codes\": {},\n        \"textual_codes\": {},\n        \"instructions\": [],\n        \"ewallet_id\": null,\n        \"ewallets\": [],\n        \"payment_method_options\": {},\n        \"payment_method_type\": \"us_mastercard_card\",\n        \"payment_method_type_category\": \"card\",\n        \"fx_rate\": 0,\n        \"merchant_requested_currency\": null,\n        \"merchant_requested_amount\": null,\n        \"payment_fees\": null,\n        \"invoice\": \"\",\n        \"escrow\": null\n    }\n}",
      "language": "json",
      "name": "Response #2"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Example #2 - Idempotent"
}
[/block]
The following example illustrates two idempotent requests. They use the same `idempotency` header. Note the value of the `amount` field. In the responses, you can see that the `id` field is the same.
[block:code]
{
  "codes": [
    {
      "code": "{\n\t\"amount\": 57,\n\t\"currency\": \"USD\",\n\t\"payment_method\": {\n\t\t\"type\": \"us_mastercard_card\",\n\t\t\"fields\": {\n\t\t\t\"number\": \"4111111111111111\",\n\t\t\t\"expiration_month\": \"12\",\n\t\t\t\"expiration_year\": \"23\",\n\t\t\t\"name\": \"John Doe\",\n\t\t\t\"cvv\": \"345\"\n\t\t},\n\t\t\"metadata\": {\n\t\t\t\"merchant_defined\": true\n\t\t}\n\t}\n}",
      "language": "json",
      "name": "Request #1"
    },
    {
      "code": "{\n    \"status\": {\n        \"error_code\": \"\",\n        \"status\": \"SUCCESS\",\n        \"message\": \"\",\n        \"response_code\": \"\",\n        \"operation_id\": \"8b354b86-db72-4784-af3b-6421b89e1d12\"\n    },\n    \"data\": {\n        \"id\": \"payment_ca36b3dc4d55d46310c9e7763e12d3e2\",\n        \"amount\": 57,\n        \"original_amount\": 57,\n        \"is_partial\": false,\n        \"currency_code\": \"USD\",\n        \"country_code\": \"US\",\n        \"status\": \"CLO\",\n        \"description\": \"\",\n        \"merchant_reference_id\": \"\",\n        \"customer_token\": \"cus_21bc82061221f9f797989a977baeae67\",\n        \"payment_method\": \"card_9b04b0bb4a395ef84ffcf796972320d2\",\n        \"expiration\": \"0\",\n        \"captured\": true,\n        \"refunded\": false,\n        \"refunded_amount\": 0,\n        \"receipt_email\": \"\",\n        \"redirect_url\": \"\",\n        \"complete_payment_url\": \"\",\n        \"error_payment_url\": \"\",\n        \"receipt_number\": \"\",\n        \"flow_type\": \"\",\n        \"address\": null,\n        \"statement_descriptor\": \"\",\n        \"transaction_id\": \"\",\n        \"created_at\": \"1565511846\",\n        \"metadata\": {},\n        \"failure_code\": \"\",\n        \"failure_message\": \"\",\n        \"paid\": true,\n        \"paid_at\": 1565511847,\n        \"dispute\": null,\n        \"refunds\": null,\n        \"order\": null,\n        \"outcome\": null,\n        \"visual_codes\": {},\n        \"textual_codes\": {},\n        \"instructions\": [],\n        \"ewallet_id\": null,\n        \"ewallets\": [],\n        \"payment_method_options\": {},\n        \"payment_method_type\": \"us_mastercard_card\",\n        \"payment_method_type_category\": \"card\",\n        \"fx_rate\": 0,\n        \"merchant_requested_currency\": null,\n        \"merchant_requested_amount\": null,\n        \"payment_fees\": null,\n        \"invoice\": \"\",\n        \"escrow\": null\n    }\n}",
      "language": "json",
      "name": "Response #1"
    },
    {
      "code": "{\n\t\"amount\": 57,\n\t\"currency\": \"USD\",\n\t\"payment_method\": {\n\t\t\"type\": \"us_mastercard_card\",\n\t\t\"fields\": {\n\t\t\t\"number\": \"4111111111111111\",\n\t\t\t\"expiration_month\": \"12\",\n\t\t\t\"expiration_year\": \"23\",\n\t\t\t\"name\": \"John Doe\",\n\t\t\t\"cvv\": \"345\"\n\t\t},\n\t\t\"metadata\": {\n\t\t\t\"merchant_defined\": true\n\t\t}\n\t}\n}",
      "language": "json",
      "name": "Idempotent request #2"
    },
    {
      "code": "{\n    \"status\": {\n        \"error_code\": \"\",\n        \"status\": \"SUCCESS\",\n        \"message\": \"\",\n        \"response_code\": \"\",\n        \"operation_id\": \"8b354b86-db72-4784-af3b-6421b89e1d12\"\n    },\n    \"data\": {\n        \"id\": \"payment_ca36b3dc4d55d46310c9e7763e12d3e2\",\n        \"amount\": 57,\n        \"original_amount\": 57,\n        \"is_partial\": false,\n        \"currency_code\": \"USD\",\n        \"country_code\": \"US\",\n        \"status\": \"CLO\",\n        \"description\": \"\",\n        \"merchant_reference_id\": \"\",\n        \"customer_token\": \"cus_21bc82061221f9f797989a977baeae67\",\n        \"payment_method\": \"card_9b04b0bb4a395ef84ffcf796972320d2\",\n        \"expiration\": \"0\",\n        \"captured\": true,\n        \"refunded\": false,\n        \"refunded_amount\": 0,\n        \"receipt_email\": \"\",\n        \"redirect_url\": \"\",\n        \"complete_payment_url\": \"\",\n        \"error_payment_url\": \"\",\n        \"receipt_number\": \"\",\n        \"flow_type\": \"\",\n        \"address\": null,\n        \"statement_descriptor\": \"\",\n        \"transaction_id\": \"\",\n        \"created_at\": \"1565511846\",\n        \"metadata\": {},\n        \"failure_code\": \"\",\n        \"failure_message\": \"\",\n        \"paid\": true,\n        \"paid_at\": 1565511847,\n        \"dispute\": null,\n        \"refunds\": null,\n        \"order\": null,\n        \"outcome\": null,\n        \"visual_codes\": {},\n        \"textual_codes\": {},\n        \"instructions\": [],\n        \"ewallet_id\": null,\n        \"ewallets\": [],\n        \"payment_method_options\": {},\n        \"payment_method_type\": \"us_mastercard_card\",\n        \"payment_method_type_category\": \"card\",\n        \"fx_rate\": 0,\n        \"merchant_requested_currency\": null,\n        \"merchant_requested_amount\": null,\n        \"payment_fees\": null,\n        \"invoice\": \"\",\n        \"escrow\": null\n    }\n}",
      "language": "json",
      "name": "Response #2"
    }
  ]
}
[/block]
Note that the response to the idempotent second request is identical to the response to the first request.
[block:api-header]
{
  "title": "Example #3 - Idempotent"
}
[/block]
The following example illustrates two idempotent requests. They use the same `idempotency` header. Note that the values of the `currency` field are different, and the payment method is different. In the responses, you can see that the `id` field is the same.
[block:code]
{
  "codes": [
    {
      "code": "{\n\t\"amount\": 15.65,\n\t\"currency\": \"USD\",\n\t\"payment_method\": {\n\t\t\"type\": \"us_mastercard_card\",\n\t\t\"fields\": {\n\t\t\t\"number\": \"4111111111111111\",\n\t\t\t\"expiration_month\": \"12\",\n\t\t\t\"expiration_year\": \"23\",\n\t\t\t\"name\": \"John Doe\",\n\t\t\t\"cvv\": \"345\"\n\t\t},\n\t\t\"metadata\": {\n\t\t\t\"merchant_defined\": true\n\t\t}\n\t}\n}",
      "language": "json",
      "name": "Request #1"
    },
    {
      "code": "{\n    \"status\": {\n        \"error_code\": \"\",\n        \"status\": \"SUCCESS\",\n        \"message\": \"\",\n        \"response_code\": \"\",\n        \"operation_id\": \"0b637672-085a-45d0-9432-2072d7fb4e83\"\n    },\n    \"data\": {\n        \"id\": \"payment_11109b0c4a35741609f30e55725de43a\",\n        \"amount\": 15.65,\n        \"original_amount\": 15.65,\n        \"is_partial\": false,\n        \"currency_code\": \"USD\",\n        \"country_code\": \"US\",\n        \"status\": \"CLO\",\n        \"description\": \"\",\n        \"merchant_reference_id\": \"\",\n        \"customer_token\": \"cus_ad6f397fa6635f585471f1d74daaff74\",\n        \"payment_method\": \"card_6e1f496be2f47dc011f4412eaf1fd36f\",\n        \"expiration\": \"0\",\n        \"captured\": true,\n        \"refunded\": false,\n        \"refunded_amount\": 0,\n        \"receipt_email\": \"\",\n        \"redirect_url\": \"\",\n        \"complete_payment_url\": \"\",\n        \"error_payment_url\": \"\",\n        \"receipt_number\": \"\",\n        \"flow_type\": \"\",\n        \"address\": null,\n        \"statement_descriptor\": \"\",\n        \"transaction_id\": \"\",\n        \"created_at\": \"1565512168\",\n        \"metadata\": {},\n        \"failure_code\": \"\",\n        \"failure_message\": \"\",\n        \"paid\": true,\n        \"paid_at\": 1565512168,\n        \"dispute\": null,\n        \"refunds\": null,\n        \"order\": null,\n        \"outcome\": null,\n        \"visual_codes\": {},\n        \"textual_codes\": {},\n        \"instructions\": [],\n        \"ewallet_id\": null,\n        \"ewallets\": [],\n        \"payment_method_options\": {},\n        \"payment_method_type\": \"us_mastercard_card\",\n        \"payment_method_type_category\": \"card\",\n        \"fx_rate\": 0,\n        \"merchant_requested_currency\": null,\n        \"merchant_requested_amount\": null,\n        \"payment_fees\": null,\n        \"invoice\": \"\",\n        \"escrow\": null\n    }\n}",
      "language": "json",
      "name": "Response #1"
    },
    {
      "code": "{\n\t\"amount\": 15.65,\n\t\"currency\": \"MXN\",\n\t\"payment_method\": {\n\t\t\"type\": \"mx_santander_bank\",\n\t\t\"fields\": {}\n\t},\n\t\"metadata\": {\n\t\t\"merchant_defined\": true\n\t}\n}",
      "language": "json",
      "name": "Non-identical request #2"
    },
    {
      "code": "{\n    \"status\": {\n        \"error_code\": \"\",\n        \"status\": \"SUCCESS\",\n        \"message\": \"\",\n        \"response_code\": \"\",\n        \"operation_id\": \"0b637672-085a-45d0-9432-2072d7fb4e83\"\n    },\n    \"data\": {\n        \"id\": \"payment_11109b0c4a35741609f30e55725de43a\",\n        \"amount\": 15.65,\n        \"original_amount\": 15.65,\n        \"is_partial\": false,\n        \"currency_code\": \"USD\",\n        \"country_code\": \"US\",\n        \"status\": \"CLO\",\n        \"description\": \"\",\n        \"merchant_reference_id\": \"\",\n        \"customer_token\": \"cus_ad6f397fa6635f585471f1d74daaff74\",\n        \"payment_method\": \"card_6e1f496be2f47dc011f4412eaf1fd36f\",\n        \"expiration\": \"0\",\n        \"captured\": true,\n        \"refunded\": false,\n        \"refunded_amount\": 0,\n        \"receipt_email\": \"\",\n        \"redirect_url\": \"\",\n        \"complete_payment_url\": \"\",\n        \"error_payment_url\": \"\",\n        \"receipt_number\": \"\",\n        \"flow_type\": \"\",\n        \"address\": null,\n        \"statement_descriptor\": \"\",\n        \"transaction_id\": \"\",\n        \"created_at\": \"1565512168\",\n        \"metadata\": {},\n        \"failure_code\": \"\",\n        \"failure_message\": \"\",\n        \"paid\": true,\n        \"paid_at\": 1565512168,\n        \"dispute\": null,\n        \"refunds\": null,\n        \"order\": null,\n        \"outcome\": null,\n        \"visual_codes\": {},\n        \"textual_codes\": {},\n        \"instructions\": [],\n        \"ewallet_id\": null,\n        \"ewallets\": [],\n        \"payment_method_options\": {},\n        \"payment_method_type\": \"us_mastercard_card\",\n        \"payment_method_type_category\": \"card\",\n        \"fx_rate\": 0,\n        \"merchant_requested_currency\": null,\n        \"merchant_requested_amount\": null,\n        \"payment_fees\": null,\n        \"invoice\": \"\",\n        \"escrow\": null\n    }\n}",
      "language": "json",
      "name": "Response #2"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Note",
  "body": "If the intent is to create a different payment with a different currency and a different payment method, you cannot use the same `idempotency` header if the amount is the same."
}
[/block]