---
title: CAMARA numberVerify v1.0.0
language_tabs: []
toc_footers:
  - <a href="https://github.com/camaraproject/">Product documentation at
    Camara</a>
includes: []
search: true
highlight_theme: darkula
headingLevel: 2

---

<!-- Generator: Widdershins v4.0.1 -->

<h1 id="camara-numberverify">CAMARA numberVerify v1.0.0</h1>

> Scroll down for example requests and responses.

## Overview
Validates that the MSISDN of the mobile device connected via the cellular network is using the IP address of the connection to the server of the service that is querying the API.

## 1. Introduction

The CAMARA numberVerify API provides a service to MNO single sign-on for mobile applications (confirmation of subscriber number and IP used for application authentication without the need to use SMS or passwords).

## 2. Quick Start

- The Mobile User inform MSISDN to verification.

- BackEnd APP or Web Partner Application Server pass the IP address to TIM API GTW to validate MSISDN. 

- TIM API GTW expose a standard Openverse API CAMARA numberVerify for NumberVerification.

Before starting to use the API, the developer needs to know about the below specified details:
    
**consentGranted**

Indicates whether operator have consent from mobile phone number's owner to perform this request.
 
**device_msisdn**

Mobile phone number (MSISDN) to verify. The number must be in international format.
 
**deviceIp**

IPv4 or IPv6 address of the mobile device that will be verified with operator. 
 
**devicePort**

Port of the mobile device that will be verified with operator. Can be used only when "deviceIp" is also provided.
 
**callbackUrl**

Your URL that will be called to provide verification result when the process is complete. 
 
**returnUrl**

An URL to which the mobile device will be redirected to when verification is complete.
 
As assumption we considering to verify the phone number of the device connected to our the mobile data network 4G and 5G.

## 3. Authentication and Authorization

The numberVerify API makes use of the client credentials grant which is applicable for server to server use cases involving trusted partners or clients.
In this method the API invoker client is registered as a confidential client with an authorization grant type of client\_credentials.

Configure security access keys such as OAuth 2.0 client credentials to be used by Client applications which will invoke the numberVerify API.

## 4. API Documentation
## 4.1 Details    

### 4.1.1 User Stories
- A service provider server serving a client application (Android or IOS app, or Web app), connected through cellular network, needs to validate the MSISDN of a user. 

- To do this, it asks the user to enter their MSISDN, and then server(SP) executes the NumberVerification API, informing the MSISDN and the IP address of the cellular access of the client in question, used to inform the MSISDN to the server.

- If the informed IP address is in use by the
informed MSISDN, the API will return “OK” for the match. Otherwise, it will report “NOK”

### 4.1.2 API E2E Flows:
- Mobile phone user with a mobile device connected via the cellular network accesses a service available on the public internet. 

- This service provider asks for the MSISDN of the device and retrieves the access IP of that device.

- NumberVerification call MNO server, informing MSISDN and public IP of the access.

- API checks if there is a match between MSISDN and public IP on the operator

- API responds to the server the result of the match check = OK/NOK

Base URLs:

* <a href="https://api.timbrasil.com.br">https://api.timbrasil.com.br</a>

License: <a href="https://www.apache.org/licenses/LICENSE-2.0.html">Apache 2.0</a>

# Authentication

- oAuth2 authentication. This API uses OAuth 2 [More info](https://api.example.com/docs/auth)

    - Flow: clientCredentials

    - Token URL = [https://example.com/oauth/token](https://example.com/oauth/token)

|Scope|Scope Description|
|---|---|
|authorize:read|Grant read-only authorize data|

<h1 id="camara-numberverify-verified-msisdn">Verified MSISDN</h1>

## get__authorize

> Code samples

`GET /authorize`

*Authorize*

Authorize authenticated via oAuth2

<h3 id="get__authorize-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|response_type|query|string|false|none|
|scope|query|string|false|none|
|version|query|string|false|none|
|redirect_uri|query|string|false|none|
|nonce|query|integer|false|none|
|prompt|query|string|false|none|
|state|query|string|false|none|
|correlation_id|query|string|false|none|
|acr_values|query|integer|false|none|
|client_id|query|string|false|client_id provided by MNO for mc vm match api consumption|

> Example responses

<h3 id="get__authorize-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful response|None|

<h3 id="get__authorize-responseschema">Response Schema</h3>

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
oAuth2 ( Scopes: authorize:read )
</aside>

## post__token

> Code samples

`POST /token`

*Token*

> Body parameter

<h3 id="post__token-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Content-Type|header|string|false|none|
|Authorization|header|string|false|base64(client_id:client_secret)|
|grant_type|query|string|false|none|
|code|query|string|false|none|
|correlation_id|query|string|false|none|
|redirect_uri|query|string|false|none|

> Example responses

> 200 Response

```json
{
  "access_token": "hIiC6ksKeD7olGcdW7-KcsKrX0kMEEm_NEtRdE2Le9k",
  "id_token": "{id_token}",
  "correlation_id": "vm_match",
  "token_type": "Bearer",
  "expires_in": "500"
}
```

<h3 id="post__token-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|Inline|

<h3 id="post__token-responseschema">Response Schema</h3>

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Date|string||none|
|200|Content-Type|string||none|
|200|Transfer-Encoding|string||none|
|200|Connection|string||none|
|200|Strict-Transport-Security|string||none|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
oAuth2 ( Scopes: authorize:read )
</aside>

## post__openid_userinfo

> Code samples

`POST /openid/userinfo`

*User Info*

> Body parameter

```json
{
  "correlation_id": "vm_match",
  "received_correlation_id": "true",
  "mc_claims": {
    "device_msisdn": "+5511985231234"
  }
}
```

<h3 id="post__openid_userinfo-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Content-Type|header|string|false|none|
|Authorization|header|string|false|access_token|
|X-Request-consentGranted|header|boolean|false|none|
|X-Request-deviceIp|header|string(ip)|false|none|
|X-Request-devicePort|header|integer(int32)|false|none|
|X-Request-callbackUrl|header|string|false|none|
|X-Request-returnUrl|header|string|false|none|
|body|body|object|false|none|

> Example responses

> OK

```json
{
  "sub": "c1be197e-4314-4dd9-bd3e-26002004b468b5a9dc43",
  "correlation_id": "vm_match",
  "device_msisdn_verified": true
}
```

```json
{
  "sub": "c1be197e-4314-4dd9-bd3e-26002004b468b5a9dc43",
  "correlation_id": "vm_match",
  "device_msisdn_verified": false
}
```

> 401 Response

```json
{
  "code": "UNAUTHORIZED",
  "message": "Authorization failed: ..."
}
```

> 403 Response

```json
{
  "code": "FORBIDDEN",
  "message": "Operation not allowed: ..."
}
```

> 404 Response

```json
{
  "status": "ERROR",
  "message": "Resource not found"
}
```

> 500 Response

```json
{
  "status": "ERROR",
  "message": "Generic error"
}
```

> 503 Response

```json
{
  "code": "SERVICE_UNAVALIBLE",
  "message": "Service unavailable"
}
```

> 504 Response

```json
{
  "status": "ERROR",
  "message": "Backend connection timeout"
}
```

<h3 id="post__openid_userinfo-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|Inline|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|[ErrorInfo](#schemaerrorinfo)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Forbidden|[ErrorInfo](#schemaerrorinfo)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The specified resource was not found|[ErrResponse](#schemaerrresponse)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|An unknow error has occurred|[ErrResponse](#schemaerrresponse)|
|503|[Service Unavailable](https://tools.ietf.org/html/rfc7231#section-6.6.4)|Service unavailable|[ErrorInfo](#schemaerrorinfo)|
|504|[Gateway Time-out](https://tools.ietf.org/html/rfc7231#section-6.6.5)|Connection timeout towards backend service has occurred|[ErrResponse](#schemaerrresponse)|

<h3 id="post__openid_userinfo-responseschema">Response Schema</h3>

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Date|string||none|
|200|Content-Type|string||none|
|200|Transfer-Encoding|string||none|
|200|Connection|string||none|
|200|X-Content-Type-Options|string||none|
|200|X-XSS-Protection|string||none|
|200|Cache-Control|string||none|
|200|Pragma|string||none|
|200|Expires|integer||none|
|200|X-Frame-Options|string||none|
|200|Strict-Transport-Security|string||none|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
oAuth2 ( Scopes: authorize:read )
</aside>

# Schemas

<h2 id="tocS_ErrResponse">ErrResponse</h2>
<!-- backwards compatibility -->
<a id="schemaerrresponse"></a>
<a id="schema_ErrResponse"></a>
<a id="tocSerrresponse"></a>
<a id="tocserrresponse"></a>

```json
{
  "status": "OK",
  "message": "OK"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|status|string|false|none|none|
|message|string|false|none|none|

<h2 id="tocS_ErrorInfo">ErrorInfo</h2>
<!-- backwards compatibility -->
<a id="schemaerrorinfo"></a>
<a id="schema_ErrorInfo"></a>
<a id="tocSerrorinfo"></a>
<a id="tocserrorinfo"></a>

```json
{
  "code": "string",
  "message": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|code|string|true|none|Code given to this error|
|message|string|true|none|Detailed error description|

