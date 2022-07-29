# Authorizing OAuth Apps

OAuth2.0 is a protocol that allows SolveXia to communicate with third-party applications, authorize them and grant access via a generated access token.

OAuth2.0 flow in SolveXia is implemented according to [RFC 6749](https://tools.ietf.org/html/rfc6749) 
to make the integration with SolveXia API as easy as possible.

SolveXia API provides two main methods for generating access tokens: **Client Credentials Flow**, **Authorize Code Flow**.

We strongly recommend using authorize Code Flow for client production applications. 
The [Client Credentials Flow](#client-credentials-flow) is intended to be used by internal scripts or for testing purposes. 
Public third party applications that rely on SolveXia for authentication should not ask for or collect SolveXia user credentials.
Instead, they must use the [Authorization Code Flow](#authorize-code-flow).


### Index
[Client Credentials Flow](#client-credentials-flow)  
[Authorization Code Flow](#authorize-code-flow)
[Refresh Token](#refresh-token)  
[API Request with Token](#call-solveXia-public-api-with-access-token)

## Client Credentials Flow

Client Credentials Flow is available for limited contexts like internal scripts or testing. 
The flow contains just one step which generates an access token by supplying client_id and client_secret.

#### Generate access token

```apacheconfig
POST 
https://[env].solvexia.com/oauth/token 
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
|scope|`string`|OPTIONAL. A whitespace-separated list of [scopes](./oauth-scopes.md) your application requires to work.|

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
|access_token|`string`|Access token to use for subsequent API's.|
|token_type|`string`|Will always be "Bearer".|
|expires_in|`number`|Seconds in which the access token will expire, for the user application to handle.|

##### Example

```bash
curl -X POST "https://app.solvexia.com/oauth/token" \
     -H "Content-Type: application/json" \
     -d '{"client_id":"DDF-AAFBD447-55432-475B-83DB-B5AD78878821","client_secret":"B5AD78878821","grant_type":"client_credentials"}'
```

## Authorize Code Flow

Authorize Code Flow is for the client public applications.

The flow contains the following steps:
1. Redirect to SolveXia authorization endpoint
2. SolveXia prompts user to login and consent
3. Generate access token & refresh token by supplying authorization code and client id

User can refresh the access token with refresh token

#### 1. Redirect to SolveXia authorization endpoint

```http
GET
https://[env].solvexia.com/oauth/authorize?client_id=your_client_id&response_type=code&redirect_uri=your_return_url
```

##### Parameters

| Name | Type |Description |
| ------------- |------------- | -------------|
|client_id|`string`|REQUIRED. Client id that you received when you created an application in SolveXia.|
|response_type|`string`|REQUIRED. will always be "code".|
|redirect_uri|`string`|OPTIONAL. If not supplied it will use configured redirect url of the oauth application, if supplied it must match the oauth application redirect url.|
|state|`string`|OPTIONAL. Specifies any string value that your application uses to maintain state between your authorization request and the authorization server's response.|
|scope|`string`|OPTIONAL. A whitespace-separated list of [scopes](./oauth-scopes.md) your application requires to work.|

After the SolveXia authorization server successfully verifies your parameters, it will redirect the user to the login page and, as a next step, to the authorization form.

#### 2. SolveXia prompts user to login and consent
![login](login.png)

In this step, the user logs in and considers whether to grant your application the requested access. At this stage, SolveXia displays a consent form that shows the name of your application.
The user can then authorize access to their SolveXia resources requested by your application or refuse the request.

![authorize](authorize.png)

If the user authorizes access, you will be redirected back to the supplied (or configured) redirect uri with the authorization code in the query string.
If you supplied an optional state parameter in the first step, SolveXia will return that as well.

```http
GET
https://example.return_url.com?code=authorization_code
```

#### 3. Exchange authorization code for access and refresh tokens

Finally, you can exchange the authorization code for an access token. Note, that authorization code has a short life span of 5 seconds.

```http
POST
https://[env].solvexia.com/oauth/token 
```

##### Parameters


| Name | Type |Description |
| ------------- |------------- | -------------|
|client_id|`string`|REQUIRED. Client id that you received when you created an application in SolveXia.|
|client_secret|`string`|REQUIRED. Client secret that you received when you created an application in SolveXia.|
|redirect_uri|`string`|OPTIONAL. If supplied during Step 1, it must match.|
|grant_type|`string`|REQUIRED. For this flow grant type should always equal to "authorization_code".|
|code|`string`|REQUIRED. code that was returned in query string in Step 3.|

```json
{
    "client_id"    : "DDF-AAFBD447-55432-475B-83DB-B5AD78878821",
    "client_secret": "B5AD78878821",
    "redirect_uri" : "https://example.return_url.com",
    "grant_type"   : "authorization_code",
    "code"         : "834t0jgf03ht3h5tp03hhw3ph432trtj349t439jt034jh35ha34tj34hth34t034t3"
}
```

##### Response

By default, response comes in JSON.

| Name | Type |Description |
| ------------- |------------- | -------------|
|access_token|`string`|Access token to use for subsequent API's.|
|refresh_token|`string`|Refresh token to use for Refresh request to generate new Access Token. Has a default expiration of 6 months.|
|token_type|`string`|Will always be "Bearer".|
|expires_in|`number`|Seconds in which the access token will expire, for the user application to handle.|
|scope|`string`|OPTIONAL. A whitespace-separated list of [scopes](./oauth-scopes.md) your application requires to work.|

```json
{
    "refresh_token": "430rt03erhge5heg9geiorhgeorgerguperg8h304g340gh0rhgerhgehrg349gjh3409hg3rtrt",
    "access_token" : "syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg",
    "token_type"   : "Bearer",
    "expires_in"   : 599.1044945,
    "scope"        : "user_read usergroup_read process"
}
```

##### Example

```cURL
curl -X POST "https://app.solvexia.com/oauth/token" \
     -H "Content-Type: application/json" \
     -d '{"client_id":"DDF-AAFBD447-55432-475B-83DB-B5AD78878821","client_secret":"B5AD78878821","grant_type":"authorization_code","code":"430rt03erhgehrg349gjh3409hg3rtrt"}'
```

## Refresh Token

You can refresh the access token at any point prior to the refresh token expiring, if you refresh the access token it also renews the refresh token expiry as well for another 6 months.

```http
POST
https://[env].solvexia.com/oauth/token 
```

##### Parameters

```json
{
    "client_id"    : "DDF-AAFBD447-55432-475B-83DB-B5AD78878821",
    "client_secret": "B5AD78878821",
    "refresh_token": "430rt03erhge5heg9geiorhgeorgerguperg8h304g340gh0rhgerhgehrg349gjh3409hg3rtrt",
    "grant_type"   : "refresh_token"
}
```


| Name | Type |Description |
| ------------- |------------- | -------------|
|client_id|`string`|REQUIRED. Client id that was submitted during generating of access token.|
|client_secret|`string`|REQUIRED. Client secret that you received when you created an application in SolveXia.|
|redirect_uri|`string`|OPTIONAL. If supplied during generating of access token, it must match.|
|grant_type|`string`|REQUIRED. For this flow grant type should always equal to "refresh_token".|

##### Response

By default, response comes in JSON.

```json
{
    "refresh_token": "gerg9erge9rg9eg9egyjkjytyju5reglemgkm5kgetremtert",
    "access_token" : "eyJhbGciOiJBMjU2S1ciLCJlbmMiOiJBMTI4Q0JDLUhTMjU2Ii",
    "token_type"   : "Bearer",
    "expires_in"   : 599.3086187
}
```
| Name | Type |Description |
| ------------- |------------- | -------------|
|access_token|`string`|Access token to use for subsequent API's.|
|refresh_token|`string`|Refresh token to use for Refresh request to generate new Access Token. Has a default expiration of 6 months.|
|token_type|`string`|Will always be "Bearer".|
|expires_in|`number`|Seconds in which the access token will expire, for the user application to handle.|
|scope|`string`|OPTIONAL. A whitespace-separated list of [scopes](./oauth-scopes.md) your application requires to work.|


##### Example

```cURL
curl -X POST "https://app.solvexia.com/oauth/token" \
     -H "Content-Type: application/json" \
     -d '{"client_id":"DDF-AAFBD447-55432-475B-83DB-B5AD78878821","client_secret":"B5AD78878821","grant_type":"refresh_token","refresh_token":"430rt03erhgehrg349gjh3409hg3rtrt"}'
```

## Call SolveXia public API with access token

```http
GET https://[env].solvexia.com/api/v1/processes

Authorization: Bearer ACCESS_TOKEN
```

##### Example

```cURL
curl -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg" \
     https://app.solvexia.com/api/v1/processes
```
