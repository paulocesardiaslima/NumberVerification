# Number Verify API documentation

## Overview

### Introduction

CAMARA Number Verify API aims to deliver proof of device possession, that is attached to SIM card and MSISDN, using mobile network authentication.

CAMARA community agreed to enable Number Verify API in two complementary flavours:

1. Based on CAMARA standardization guidelines, that enables API service on a dedicated endpoint and follows CAMARA AuthN/AuthZ concept. [More details available here](#details)
2. Based on GSMA Mobile Connect standardized family of Identity APIs, that delivers Verified MSISDN service. [More details available here](#details)

### Quick start

1. Download one of yaml files.
2. Contact CAMARA API maintainers to get guidance on the onboarding process:

   * [Deutsche Telekom - Dawid Wróblewski](https://github.com/DT-DawidWroblewski)
   * [Telefonica - Mona Mokhber](https://github.com/monamok)
   * [Orange - Ludovic Robert](https://github.com/bigludo7)

### Onboarding process for Mobile Connect

1. Describe your Use case within *Use Case Declaration Form* - provided by MNO employee that guides you through the whole process. MNOs require you to provide data like (it is a subject to local market/MNO conditions what is required):

* Name/Address/Website/Contact
* Business Type
* Mobile Connect product that is required for a use case
* Use case description, from the consumer point of view (preferably with screenshots, sequence diagrams, and information about where Mobile Connect product shall be used)
* Purpose - the reason for using Mobile Connect
* Privacy Policy details
* Consent Policy details, including the process of consent acquisition

2. Register *redirect_uri*
3. Register MSISDNs you would like to test Number Verify API
4. Register MSISDN to pass secrets (e.g. client_secret or API-key)

Upon successful onboarding following details are shared:

1. **client_id** - used for requesting Mobile Connect services
2. **client_secret** - passed in a secured way, e.g. by SMS to MSISDN provided during onboarding

## Authentication and/or Authorization

* [Camara AuthN/AuthZ Concept]()
* [Mobile Connect AuthN/AuthZ Concept covered within MC Verified MSISDN specification](https://www.gsma.com/identity/wp-content/uploads/2022/12/IDY.54-Mobile-Connect-Verified-MSISDN-Definition-and-Technical-Requirements-1.0.pdf)

## Documentation

### Details

|Flavour|Details Page|
|---|---|
|CAMARA|[DetailsPage](../../code/API_definitions/CAMARA/NUMBER_VERIFICATION_API.md)|
|Mobile Connect|[DetailsPage](../../code/API_definitions/MobileConnect/MC_VERIFIED_MSISDN.md)|

### Endpoint definitions

|Flavour|Endpoint type|Endpoint path|
|---|---|---|
|CAMARA|AuthN/AuthZ||
||resource|/verify|
|Mobile Connect|AuthN|/authorize<br>/token|
||resource|/userinfo|

>Please note that Mobile Connect **/authorize** covers mobile network authentication step that requirements are subject of a particuler MNO and might require, but not limited to, e.g. additional request headers, request in HTTP, follow redirect to additional ID services (like token servers).

### Errors

Described inside yaml files.

### Release Notes

|No|Version|Changelog|
|:---:|---:|:---|
|1|0.5.0|Camara & Mobile Connect flavours available|

## API Spec

|Flavour|yaml|
|---|---|
|CAMARA Number Verification|[yaml](../../code/API_definitions/CAMARA/number_verification.yaml)|
|Mobile Connect Verified MSISDN|[yaml](../../code/API_definitions/MobileConnect/numberVerify.yaml)|
