# AISP API Overview

## Base URL
The base URL for all AIS APIs is: `https://rs1.api.tccl.eu-hub-prod.ozoneapi.co.uk/open-banking/v4/aisp/**`.

## Account Access Consents
[Account Access Consents API](/perry/developer/documentation?resource=euhub-tccl-portal-new&document=swagger/account-info-openapi.yaml#operations-tag-Account_Access)

## Accounts
[Accounts API](/perry/developer/documentation?resource=euhub-tccl-portal-new&document=swagger/account-info-openapi.yaml#operations-tag-Accounts)

Currencycloud members will have one personal account with subaccounts for each wallet.

- Supported API: `/accounts`
- Supported fields: `AccountId`, `Status`, `Currency`, `Nickname`, `AccountCategory`, `AccountTypeCode`, `OpeningDate`, `Account[].SchemeName`, `Account[].Identification`,  `Account[].SecondaryIdentification`

## Balances
[Balances API](/perry/developer/documentation?resource=euhub-tccl-portal-new&document=swagger/account-info-openapi.yaml#operations-tag-Balances)

Balances shown in this endpoint provide the `InterimAvailable` value.

`InterimAvailable` balance is the value displayed most widely to our members within the Currencycloud apps.

Currencycloud members will have a balance for each of their wallets.

- Supported API: `/balances`
- Supported fields: `Amount.Amount`, `Amount.Currency`, `Type`, `AccountId`, `CreditDebitIndicator`, `DateTime`

## Transactions
[Transactions API](/perry/developer/documentation?resource=euhub-tccl-portal-new&document=swagger/account-info-openapi.yaml#operations-tag-Transactions)

Pagination is supported on the GET `/transactions` endpoint with a page size of 100 transactions.

- Supported API: `/transactions`
- Supported fields: `AccountId`, `TransactionId`, `CreditDebitIndicator`, `Status`, `BookingDateTime`, `ValueDateTime`, `Amount.Amount`, `Amount.Currency`

## Beneficiaries
[Beneficiaries API](/perry/developer/documentation?resource=euhub-tccl-portal-new&document=swagger/account-info-openapi.yaml#operations-tag-Beneficiaries)

- Supported API: `/beneficiaries`
- Supported fields: `AccountId`, `BeneficiaryId`, `Reference`, `CreditorAccount.SchemeName`, `CreditorAccount.Identification`, `CreditorAccount.Name`

## Direct Debits
Not supported.

## Standing Orders
Not supported.

## Products
Not supported.

## Offers
Not supported.

## Parties
[Parties API](/perry/developer/documentation?resource=euhub-tccl-portal-new&document=swagger/account-info-openapi.yaml#operations-tag-Parties)

- Supported API: `/party`
- Supported fields: `AccountRole`, `LegalStructure`, `BeneficialOwnership`, `EmailAddress`, `FullLegalName`, `Name`, `PartyId`, `Phone`, `Mobile`

## Scheduled Payments
[Scheduled Payments API](/perry/developer/documentation?resource=euhub-tccl-portal-new&document=swagger/account-info-openapi.yaml#operations-tag-Scheduled_Payments)

- Supported API: `/scheduled-payments`
- Supported fields: `AccountId`, `ScheduledPaymentId`, `ScheduledPaymentDateTime`, `ScheduledType`, `InstructedAmount.Amount`, `InstructedAmount.Currency` 

## Statements
Not supported.
