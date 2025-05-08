# MCI Fallback

A Modified Customer Interface (MCI) fallback mechanism, also known as a contingency mechanism. An MCI provides a backup plan that allows third-party payment providers (TPPs) to access Currencycloud customer data through Currencycloud Direct if our Open Banking APIs are not working.

## Service flow

1. The TPP initiates a request to the MCI interface, embedding its QWAC certificate within the request.
2. The MCI service verifies the TPP’s certificate against the OBIE Directory. If the certificate is valid, the TPP is granted access to proceed.
3. The TPP then conducts the PSU (Payment Service User) authentication and, upon successful authentication, gains access to the required services.
4. If the QWAC certificate is found to be invalid, the MCI service blocks the TPP request, ensuring secure and compliant access.

![mcifallback](/assets/mci-fallback.png)

## Configuration

* TPP Facing URL: https://tccl-eu.mci.uk-hub-prod.ozoneapi.co.uk
* Currencycloud Direct Base URL: https://direct.currencycloud.com

As a TTP, you'll then make requests via https://tccl-eu.mci.uk-hub-prod.ozoneapi.co.uk/ ensuring you include your QWAC certificate in the request.