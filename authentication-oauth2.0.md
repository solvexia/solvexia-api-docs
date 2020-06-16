# Authorizing OAuth Apps

OAuth2.0 is a protocol that allows SolveXia to communicate with third-party applications, authorise them and grant access via generation access tokens.

OAuth2.0 flow in SolveXia is implemented according to [RFC 6749](https://tools.ietf.org/html/rfc6749) 
to make the integration with SolveXia API as easy as possible.

SolveXia API provides two main methods for generating access tokens: **Client Credentials Flow**, **Authorise Code Flow**.

We strongly recommend using Authorise Code Flow for client production applications. 
The Client Credentials Flow is intended to be used by internal scripts or for testing purposes. 
Public third party applications that rely on GitHub for authentication should not ask for or collect SolveXia user credentials.
Instead, they must use the Authorise Code Flow web flow.

---

## Client Credentials Flow

Client Credentials Flow is available for limited contexts like internal scripts or testing.

The flow contains the following steps:
1. Generate access token by supplying client_id and client_secret

#### 1. Generate access token

```apacheconfig
POST https://app.solvexia.com/oauth/token 
```

##### Parameters

```json
{
    "client_id"    : "DDF-AAFBD447-55432-475B-83DB-B5AD78878821",
    "client_secret": "B5AD78878821",
    "grant_type"   : "client_credentials"
}
```


| Name | Type |Description |
| ------------- |------------- | -------------|
|client_id|`string`|REQUIRED. Client id that you received when you created an application in SolveXia.|
|client_secret|`string`|REQUIRED. Client secret that you received when you created an application in SolveXia.|
|grant_type|`string`|REQUIRED. For this flow grant type should always equal to "client_credentials".|

##### Response

```json
{
    "access_token": "syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg",
    "token_type"  : "Bearer",
    "expires_in"  : 9.8270549
}
```
| Name | Type |Description |
| ------------- |------------- | -------------|
|access_token|`string`|Access token to use for subequent API's.|
|token_type|`string`|Will always be "Bearer".|
|expires_in|`string`|Seconds in which the access token will expire, for the user application to handle.|

---

## Authorize Code Flow

Authorize Code Flow is for client public applications

The flow contains the following steps:
1. Go to authorize endpoint with client_id, code and redirect url
2. Manually login
3. Authorize application to act on your behalf
4. Generate access token & refresh token by supplying authorisation code and client id

User can refresh the access token with refresh token

#### 1. Go to authorize endpoint

```apacheconfig
GET https://app.solvexia.com/authorize?client_id=DDF-AAFBD447-55432-475B-83DB-B5AD78878821&response_type=code&redirect_uri=https://returnurl.com
```

##### Parameters

| Name | Type |Description |
| ------------- |------------- | -------------|
|client_id|`string`|REQUIRED. Client id that you received when you created an application in SolveXia.|
|response_type|`string`|REQUIRED. will always be "code".|
|redirect_uri|`string`|OPTIONAL. If not supplied it will use configured redirect url of the oauth application, if supplied it must match the oauth application redirect url|

##### Response

Will redirect to login page

#### 2. Manually login
![login](login.png)

#### 3. Authorize application to act on your behalf
![authorize](authorize.png)

You will be redirected back to the supplied (or configured) redirect uri with authorization code in query string
https://returnurl.com?code=834t0jgf03ht3h5tp03hhw3ph432trtj349t439jt034jh35ha34tj34hth34t034t3

#### 4. Generate access token

```apacheconfig
POST https://app.solvexia.com/oauth/token 
```

##### Parameters

```json
{
    "client_id":"DDF-AAFBD447-55432-475B-83DB-B5AD78878821",
    "client_secret":"B5AD78878821",
    "redirect_uri":"https://returnurl.com",
    "grant_type":"authorization_code",
    "code":"834t0jgf03ht3h5tp03hhw3ph432trtj349t439jt034jh35ha34tj34hth34t034t3"
}
```


| Name | Type |Description |
| ------------- |------------- | -------------|
|client_id|`string`|REQUIRED. Client id that you received when you created an application in SolveXia.|
|client_secret|`string`|REQUIRED. Client secret that you received when you created an application in SolveXia.|
|redirect_uri|`string`|OPTIONAL. If supplied during Step 1, it must match.|
|grant_type|`string`|REQUIRED. For this flow grant type should always equal to "authorization_code".|
|code|`string`|REQUIRED. code that was returned in query string in Step 3.|

##### Response

By default response comes in JSON.

```json
{
    "refresh_token":"430rt03erhge5heg9geiorhgeorgerguperg8h304g340gh0rhgerhgehrg349gjh3409hg3rtrt",
    "access_token":"syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg",
    "token_type":"Bearer",
    "expires_in":599.1044945
}
```
| Name | Type |Description |
| ------------- |------------- | -------------|
|access_token|`string`|Access token to use for subequent API's.|
|refresh_token|`string`|Refresh token to use for Refresh request to generate new Access Token. Has a default expiration of 6 months.|
|token_type|`string`|Will always be "Bearer".|
|expires_in|`string`|Seconds in which the access token will expire, for the user application to handle.|

#### Refresh Token
You can refresh the access token at any point prior to the refresh token expiring, if you refresh the access token it also renews the refresh token expiry as well
for another 6 months.


```apacheconfig
POST https://app.solvexia.com/oauth/token 
```

##### Parameters

```json
{
    "client_id":"DDF-AAFBD447-55432-475B-83DB-B5AD78878821",
    "client_secret":"B5AD78878821",
    "refresh_token":"430rt03erhge5heg9geiorhgeorgerguperg8h304g340gh0rhgerhgehrg349gjh3409hg3rtrt",
    "grant_type":"refresh_token"
}
```


| Name | Type |Description |
| ------------- |------------- | -------------|
|client_id|`string`|REQUIRED. Client id that was submitted during generating of access token.|
|client_secret|`string`|REQUIRED. Client secret that you received when you created an application in SolveXia.|
|redirect_uri|`string`|OPTIONAL. If supplied during generating of access token, it must match.|
|grant_type|`string`|REQUIRED. For this flow grant type should always equal to "refresh_token".|

##### Response

By default response comes in JSON.

```json
{
    "refresh_token":"gerg9erge9rg9eg9egyjkjytyju5reglemgkm5kgetremtert",
    "access_token":"eyJhbGciOiJBMjU2S1ciLCJlbmMiOiJBMTI4Q0JDLUhTMjU2Ii",
    "token_type":"Bearer",
    "expires_in":599.3086187}
```
| Name | Type |Description |
| ------------- |------------- | -------------|
|access_token|`string`|Access token to use for subequent API's.|
|refresh_token|`string`|Refresh token to use for Refresh request to generate new Access Token. Has a default expiration of 6 months.|
|token_type|`string`|Will always be "Bearer".|
|expires_in|`string`|Seconds in which the access token will expire, for the user application to handle.|


---

## Call SolveXia public API with access token

```apacheconfig
GET https://app.solvexia.com/api/v1/processes

Authorization: Bearer ACCESS_TOKEN
```

Example

```bash
curl -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg" https://app.solvexia.com/api/v1/processes
```