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
|grant_type|`string`|For this flow grant type should always be equal to "client_credentials".|

##### Response

Schema

```dtd
{
	access_token  string
	token_type    string
	expires_in    float32
}
```

Example

```json
{
    "access_token": "syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg",
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

## Authorise Code Flow

Authorise Code Flow must be used in all third-party applications that intended to go public.

The authorization session contains of the following steps:
1. Authorise request with user redirection to prove their SolveXia identity
2. Users are redirected back to your app web page with a code
3. Call SolveXia public API with access token


### 1. Authorise request with user redirection to prove their SolveXia identity

Call this url and it will redirect to the page which will request user to login and approve access to your application.

```apacheconfig
GET http://app.solvexia.com/oauth/authorize
```

##### Parameters

```bash
client_id=DDF-AAFBD447-55432-475B-83DB-B5AD78878821&response_type=code&redirect_uri=https://myapp.com/
```

Explained

| Name | Type |Description |
| ------------- |------------- | -------------|
|client_id|`string`|Client id that you received when you created an application in SolveXia.|
|response_type|`string`|For this step response type should always be equal to "code".|
|redirect_uri|`string`|The URL of your application where users will be sent after authorization.|

### 2. Users are redirected back to your app web page with a code

If the authorization was successful, user is redirected back to your application page specified in `redirect_uri` with a temporary 
authorization code in a query string that you can exchange for the access token.

```apacheconfig
https://myapp.com/?code=158dgfa4678vsdfgshdflgsdfgsd9fgsd7fg-dfg7632
```

Retrieve the code and make a call to get an access token.

```apacheconfig
POST https://app.solvexia.com/oauth/token 
```

##### Parameters

Schema

```dtd
{
	client_id     string
	client_secret string
	redirect_uri  string
	grant_type    string
	code          string
}
```

Note that `redirect_uri` must stay the same through all the steps of the authorization session.

```json
{
    "client_id"    : "DDF-AAFBD447-55432-475B-83DB-B5AD78878821",
    "client_secret": "B5AD78878821",
    "redirect_uri" : "https://myapp.com/",
    "grant_type"   : "authorization_code",
    "code"         : "158dgfa4678vsdfgshdflgsdfgsd9fgsd7fg-dfg7632"
}
```

Explained

| Name | Type |Description |
| ------------- |------------- | -------------|
|client_id|`string`|Client id that you received when you created an application in SolveXia.|
|response_type|`string`|For this step response type should always be equal to "code".|
|redirect_uri|`string`|The URL of your application where users will be sent after authorization.|
|grant_type|`string`|For this flow grant type should always be equal to "authorization_code".|
|code|`string`|The authorization code that was provided to your app after successful user redirect.|

##### Response

Schema

```dtd
{
	refresh_token string
	access_token  string
	token_type    string
	expires_in    float32
}
```

Example

```json
{
    "access_token" : "syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg",
    "refresh_token": "sdfgd453SDFJHS8-kdRtfpoXTgYFF7LHgVOhIjOQSD68VZvc2_uAew.P07tE_54654w45654",
    "token_type"   : "Bearer",
    "expires_in"   : 9.8270549
}
```

Save the refresh token and expiry date. If the access token is expired, you need to refresh it using a refresh token.

### 3. Call SolveXia public API with access token

```apacheconfig
GET https://app.solvexia.com/api/v1/processes

Authorization: Bearer ACCESS-TOKEN
```

Example

```bash
curl -H "Authorization: Bearer ACCESS-TOKEN" https://app.solvexia.com/api/v1/processes
```

## Refresh access tokens

SolveXia access token live span is short, so we require you to refresh tokens in order to access SolveXia public API. Here is how.

```apacheconfig
GET https://au.qa.solvexia.com/oauth/token
```

##### Parameters

Schema

```dtd
{
	client_id     string
	client_secret string
	refresh_token string
	grant_type    string
}
```

Note that `redirect_uri` must stay the same through all the steps of the authorization session.

```json
{
    "client_id"    : "DDF-AAFBD447-55432-475B-83DB-B5AD78878821",
    "client_secret": "B5AD78878821",
    "refresh_token": "sdfgd453SDFJHS8-kdRtfpoXTgYFF7LHgVOhIjOQSD68VZvc2_uAew.P07tE_54654w45654",
    "grant_type"   : "refresh_token"
}
```

Explained

| Name | Type |Description |
| ------------- |------------- | -------------|
|client_id|`string`|Client id that you received when you created an application in SolveXia.|
|response_type|`string`|For this step response type should always be equal to "code".|
|refresh_token|`string`|The refresh token you received along with the access token.|
|grant_type|`string`|For this flow grant type should always be equal to "refresh_token".|

##### Response

Schema

```dtd
{
	refresh_token string
	access_token  string
	token_type    string
	expires_in    float32
}
```

Example

```json
{
    "access_token" : "syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg",
    "refresh_token": "sdfgd453SDFJHS8-kdRtfpoXTgYFF7LHgVOhIjOQSD68VZvc2_uAew.P07tE_54654w45654",
    "token_type"   : "Bearer",
    "expires_in"   : 9.8270549
}
```