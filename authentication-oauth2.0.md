#Authorizing OAuth Apps

OAuth2.0 is a protocol that allows SolveXia to communicate with third-party applications, authorise them and grant access.

OAuth2.0 flow in SolveXia is implemented according to [RFC 6749](https://tools.ietf.org/html/rfc6749) 
to make the integration with SolveXia API as easy as possible.

SolveXia API provides two main methods for authentication: Client Credentials Flow and Authorise Code Flow. 
We strongly recommend using Authorise Code Flow for production applications. 
The Client Credentials Flow is intended to be used for scripts or for testing purposes. 
Public third party applications that rely on GitHub for authentication should not ask for or collect SolveXia user credentials.
Instead, they must use the Authorise Code Flow web flow.

##Client Credentials Flow

Client Credentials Flow is available for limited contexts like scripts or testing.

The flow contains of the following steps:
1. Generate access token
2. Call SolveXia public API with access token
3. Refresh access token

####1. Generate access token

```apacheconfig
POST https://app.solvexia.com/oauth/token 
```

#####Parameters

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

#####Response

Be default response comes in JSON.

```json
{
    "access_token": "eyJhbGciOiJBMjU2S1ciLCJlbmMiOiJBMTI4Q0JDLUhTMjU2IiwidHlwIjoiSldUIn0.MATTGogPKhxlhgcnGEC3dM7uLjGCJR5gg1IedcXd89DrmIfcjtgySw.0wpkgniNNUknHVLEI35_Fg.uf1D7rX5guF7kR5aEmVSB-syPHeMY5H-KkCSDm7P5eJnZLbEHlUrceSoaE1_d0zgXt4D9OTW3XjzsCRbvT5ORCn1JeUirzrsCZbUNiXArh7yrt153c7_D4HledX4aQCaxv5A-kdRtfpoXTgYFF7anRTAaNt9Bj4zwy38CiVqY4q-coIhNFQJW33uJzcjCoMlPPDChvpOEMqe1cA6_79J45HgTJ_PtcUyJOxWOgqvwTo2VAgvRdy6TL-s9BG_xddMkxH25vMNgCOft-L4UdDZ9QyOYvoZHVhrVCAcwVXujDdDJeB8rkvPmIbKnFLYKgyJ5ZI_EVD8roWjptU5meetnY1uj7Jbe3HBU3kk6xbs8xrSI8O_U6skdBmRZiS8Kl3vtuHfRDDIwItGMA7i6fPtzggDqd_gttVqaLcGsmwkgMKDhwEvlf_79iZYnpmJclWrVzhG1tkQdz3OIJDQe-d4HOCRUiIyEbNP191sI-lF6-1xh1CywsTKpvzGgc38YE1wEYu9NxB1JUfBqTqLnyVkbLSt8qkUcTL3tNzaCkpa4lqWFnoUeobQeMtwHidj9-R2Q-3I9MRGFz4rf-g2TDgUEOdwlz086n4PvXHgVOhIjOQ5QglPP0dbKtQ7oftzLT6_g1e7lkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg",
    "token_type"  : "Bearer",
    "expires_in"  : 9.8270549
}
```

####2. Call SolveXia public API with access token

```apacheconfig
GET https://app.solvexia.com/api/v1/processes

Authorization: Bearer ACCESS-TOKEN
```

Example

```bash
curl -H "Authorization: Bearer ACCESS-TOKEN" https://app.solvexia.com/api/v1/processes
```