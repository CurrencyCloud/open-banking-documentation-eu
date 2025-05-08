# PISP API Overview

## Base URL
The base URL for all PIS APIs is: `https://rs1.api.tccl.eu-hub-prod.ozoneapi.co.uk/open-banking/v4/pisp/**`

## Supported Payment Types
The Currencycloud API currently supports the following:
- Domestic Payments
  - `POST /domestic-payments`
  - `GET /domestic-payments/{DomesticPaymentId}`
- Domestic Scheduled Payments
  - `POST /domestic-scheduled-payments`
  - `GET /domestic-scheduled-payments/{DomesticScheduledPaymentId}`
- International Payments
  - `POST /international-payments`
  - `GET /international-payments/{InternationalPaymentId}`
- International Scheduled Payments
  - `POST /international-scheduled-payments`
  - `GET /international-scheduled-payments/{InternationalScheduledPaymentId}`

The Currencycloud API **does not** support the following:
- Domestic Standing Orders
- International Standing Orders
- `/payment-details` end-points
- File Payments

## Overview

The header `x-idempotency-key` is required when creating payment consents and making payments.

We only support the mandatory fields, unless otherwise stated.

### The following rules apply to all domestic payment consents:

Use domestic payments for FPS payments, GBP to GBP.

### `LocalInstrument`
- Required: Only the Faster Payments Service (FPS) is supported.

### `InstructedAmount/Currency`
- Required: Must be `GBP`

### `RemittanceInformation/Structured[]`
- Required: Must contain a single object
- The object must have a name of `CreditorReferenceInformation` and contain a nested object with a key of `Reference` and the value being the provided reference

For example
```json
{
  "CreditorReferenceInformation": {
      "Reference": "{{reference value}}"
  }
}
```

### `RemittanceInformation/Unstructured[]`
- Optional: If provided, the value should represent the reason for the payment

### `Risk/BeneficiaryAccountType`
- Required:
  - Must be `Personal` when making payments to personal bank accounts
  - Must be `Business` when making payments to business bank accounts

### `CreditorAccount/SchemeName`
- Required: Only `UK.OBIE.SortCodeAccountNumber` is supported

### `CreditorPostalAddress/Country`
- Required: Must contain the two-letter combination (ISO alpha-2) representing the country where the beneficiary is located.

### The following apply to all domestic scheduled payment consents:
These follow the same rules as domestic payments with the addition of the following fields:

### `RequestedExecutionDateTime`
* Required: Must be a date in the future
* See https://support.currencycloud.com/hc/en-gb/articles/360018923079-Holiday-Calendar for more information about the allowed dates

#### Example payment consent
```json
{
    "Data": {
        "Initiation": {
            "InstructionIdentification": "ACME412",
            "EndToEndIdentification": "FRESCO.21302.GFX.20",
            "LocalInstrument": "UK.OBIE.FPS",
            "InstructedAmount": {
                "Amount": "24.99",
                "Currency": "GBP"
            },
            "CreditorAccount": {
                "SchemeName": "UK.OBIE.SortCodeAccountNumber",
                "Identification": "00000012345678",
                "Name": "Bob Davis"
            },
            "CreditorPostalAddress": {
                "Country": "UK"
            },
            "RemittanceInformation": {
                "Structured": [
                    {
                        "CreditorReferenceInformation": {
                            "Reference": "FRESCO-101"
                        }
                    }
                ],
                "Unstructured": [
                    "Internal ops code 5120101"
                ]
            }
        }
    },
    "Risk": {
        "BeneficiaryAccountType": "Personal"
    }
}
```

### The following apply to all international payment consents:

Use international payments for international SWIFT payments in all currencies supported by Currencycloud.

Payments are sent via the SWIFT network, and intermediary bank charges may apply. The payer decides if they want these charges to be deducted from the payment amount or not.
This is configured with the settings belonging to the account owner. See [SWIFT Payment Fees](https://support.currencycloud.com/hc/en-gb/articles/4415919510418-Swift-Payment-Fees) for more information about SWIFT payment fees.

> **_NOTE:_** Only payments with `InstructedAmount` in the same currency as `CurrencyOfTransfer` are supported.

### `CurrencyOfTransfer`
- Required: Must be the same currency as the `InstructedAmount/Currency`

### `CreditorAgent/SchemeName`
- Required: Must be `UK.OBIE.BICFI` and the `CreditorAgent/Identification` must also be set to be the bank's BIC.

### `CreditorAgent/Identification`
- Required: This is the bank's BIC

### `CreditorAgent/PostalAddress/Country`
- Required: Must contain the two digit letter combination (ISO alpha-2) where representing the country where the bank is located

### `Creditor/PostalAddress/TownName`
- Required: Must be the Town/City where the beneficiary is located

### `Creditor/PostalAddress/Country`
- Required: Must contain the two digit letter combination (ISO alpha-2) where representing the country where the beneficiary is located

### `CreditorAccount/SchemeName`
- Required: Must be UK.OBIE.IBAN

### `CreditorAccount/Identification`
- Required: The creditor's IBAN

### `CreditorAccount/Name`
- Required: The name of the beneficiary.
- Beneficiary names cannot contain numbers for an individual

### `RemittanceInformation/Structured[]`
- Required: Must contain a single object
- The object must have a name of `CreditorReferenceInformation` and contain a nested object with a key of `Reference` and the value being the provided reference

For example
```json
{
  "CreditorReferenceInformation": {
      "Reference": "{{reference value}}"
  }
}
```

### `RemittanceInformation/Unstructured[]`
- Optional: If provided the value should represent the reason for the payment

### `Risk/BeneficiaryAccountType`
- Required:
  - Must be `Personal` when making payments to personal bank accounts
  - Must be `Business` when making payments to business bank accounts

### The following apply to all international scheduled payment consents:
These follow the same rules as international payments with the addition of the following fields:

### `RequestedExecutionDateTime`
- Required: Must be a date in the future.
- See [Holiday Calendar](https://support.currencycloud.com/hc/en-gb/articles/360018923079-Holiday-Calendar) for more information about the allowed dates.

#### Example payment consent
```json
{
    "Data": {
        "Initiation": {
            "InstructionIdentification": "ACME412",
            "EndToEndIdentification": "FRESCO.21302.GFX.20",
            "CurrencyOfTransfer": "EUR",
            "InstructedAmount": {
                "Amount": "49.99",
                "Currency": "EUR"
            },
            "CreditorAgent": {
                "SchemeName": "UK.OBIE.BICFI",
                "Identification": "ABC123",
                "PostalAddress": {
                    "Country": "FR"
                }
            },
            "Creditor": {
                "PostalAddress": {
                    "TownName": "Paris",
                    "Country": "FR"
                }
            },
            "CreditorAccount": {
                "SchemeName": "UK.OBIE.IBAN",
                "Identification": "FR123",
                "Name": "Bob Davis"
            },
            "RemittanceInformation": {
                "Structured": [
                    {
                        "CreditorReferenceInformation": {
                            "Reference": "FRESCO-101"
                        }
                    }
                ],
                "Unstructured": [
                    "Internal ops code 5120101"
                ]
            }
        }
    },
    "Risk": {
        "BeneficiaryAccountType": "Personal"
    }
}
```