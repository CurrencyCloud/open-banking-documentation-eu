# Introduction

## Open Banking

The Currencycloud Open Banking API is based on the Open Banking Standard which allows regulated Third Party Providers (TPPs) to access Account Information Services (AIS), Payment Initiation Services (PIS), and funds confirmation requests for member accounts. Access to these services on behalf of members is controlled by strong customer authentication within Currencycloud apps as part of OpenID Connect authorisation flows.

We currently support browser-based authentication flows.

Currencycloud is an FCA-registered Account Servicing Payment Service Provider (ASPSP) who provides access to these services via the Open Banking standard.

You can find out more about Open Banking at [What is Open Banking](https://www.openbanking.org.uk/customers/what-is-open-banking/).

## API Documentation

Please see the following specifications we have aligned with:

- [Dynamic Client Registration (DCR) Specification](https://openbankinguk.github.io/dcr-docs-pub/v3.2/dynamic-client-registration.html): Use this specification to register your TPP client to use our APIs
- [Open ID Foundation's Financial Grade API (FAPI) Profile](https://openid.net/specs/openid-financial-api-part-2-1_0.html): This specification enables user authentication of consents for open banking
- [Open Banking API Specification](https://openbankinguk.github.io/read-write-api-site3/v4.0/profiles/read-write-data-api-profile.html): Based on Open Banking Read/Write API Specification v4.0.0, this specification describes the resources that are available on our service:
- [Accounts & Transaction Information API](../swagger/account-info-openapi.yaml)
- [Payments Initiation Services API](../swagger/payment-initiation-openapi.yaml)

## Getting Started

We recommend that you start off by accessing our [Sandbox](./docs/40-sandbox.md).

Our Sandbox fully reflects our production environment and provides an easy route to testing out your proposition.

To access the production environment, you must be a TPP authorised by the FCA or passported into the UK. Instructions for accessing our Production APIs are [here](./docs/30-production.md).

See our [Getting Started](./docs/20-getting-started.md) page for instructions on accessing our sandbox and production APIs

If you require test accounts then please contact support at [support@currencycloud.com](mailto:support@currencycloud.com)
