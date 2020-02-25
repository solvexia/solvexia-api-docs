# Authorizing OAuth Apps

OAuth2.0 is a protocol that allows SolveXia to communicate with third-party applications, authorise them and grant access.

OAuth2.0 flow in SolveXia is implemented according to [RFC 6749](https://tools.ietf.org/html/rfc6749) 
to make the integration with SolveXia API as easy as possible.

SolveXia API provides two main methods for authentication: Client Credentials Flow and Authorise Code Flow. 
We strongly recommend using Authorise Code Flow for production applications. 
The Client Credentials Flow is intended to be used for scripts or for testing purposes. 
Public third party applications that rely on GitHub for authentication should not ask for or collect SolveXia user credentials.
Instead, they must use the Authorise Code Flow web flow.

## Client Credentials Flow

Client Credentials Flow is available for limited contexts like scripts or testing.

The flow contains of the following steps:
1. Generate access token
2. Call SolveXia public API with access token
3. Refresh access token

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

Here is the description for each parameter

| Name | Type |Description |
| ------------- |------------- | -------------|
|client_id|`string`|Client id that you received when you created an application in SolveXia.|
|client_secret|`string`|Client secret that you received when you created an application in SolveXia.|
|grant_type|`string`|For this flow grant type should always equal to "client_credentials".|

##### Response

Be default response comes in JSON.

```json
{
    "access_token": "syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg",
    "token_type"  : "Bearer",
    "expires_in"  : 9.8270549
}
```

#### 2. Call SolveXia public API with access token

```apacheconfig
GET https://app.solvexia.com/api/v1/processes

Authorization: Bearer ACCESS-TOKEN
```

Example

```bash
curl -H "Authorization: Bearer ACCESS-TOKEN" https://app.solvexia.com/api/v1/processes
```