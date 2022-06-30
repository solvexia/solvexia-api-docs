# User APIs

[Get a user list](#get-a-user-list)  
[Get a user](#get-a-user)\
[Get a list of user groups that a user belongs to](#get-a-list-of-user-groups-that-a-user-belongs-to)  
[Create user account](#create-user-account)  
[Disable user account](#disable-user-account)\
[Get user permissions](#get-user-permissions)  
[Add or update user permission for a given resource](#add-or-update-user-permission-for-a-given-resource)  
[Delete user permission](#delete-user-permission)

---

## Get a user list

List all the users.

```apacheconfig
GET /api/v1/users
```

#### Path parameters

This request does not have any path parameters.

#### Query parameters

The query parameters are not expected.

#### Request body
The request body must be empty.

#### Response

The successful response contains an array of instances of [User List Item](./users_schemas.md/#user-list-item).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl https://app.solvexia.com/api/v1/users -X GET -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
[
  {
    "id": "u-2345",
    "loginName": "template.mona.benson"
  },
  {
    "id": "u-23577",
    "loginName": "template.jill.watkin"
  }
]
```
---

## Get a user

Returns a user at a given id.

```apacheconfig
GET /v1/users/{userId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| userId | `string` | The id of a user to request. |


#### Query parameters
The query parameters are not expected.

#### Request body
The request body must be empty.

#### Response body
The successful response contains an instance of a [User](./users_schemas.md/#user).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl https://app.solvexia.com/api/v1/users/u-11427 -X GET -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
{
    "id": "u-11427",
    "firstName": "Mona",
    "lastName": "Benson",
    "loginName": "template.mona.benson",
    "email": "mona.benson@sample.com",
    "accountStatus": "Active",
    "city": "Sydney",
    "country": "Australia",
    "dateOfBirth": null,
    "department": null,
    "lastSignInDate": "2011-03-14T14:56:00.0000000",
    "phoneNumberLand": null,
    "phoneNumberMobile": null,
    "timezone": "(UTC+10:00) Canberra, Melbourne, Sydney",
    "userRole": "Designer"
}
```
---

## Get a list of user groups that a user belongs to

Returns a list of user groups a user belongs to.

```apacheconfig
GET /v1/users/{userId}/usergroups
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| userId | `string` | The id of a user to request a list of groups for. |


#### Query parameters
The query parameters are not expected.

#### Request body
The request body must be empty.

#### Response body
The successful response contains a list of [User Group List Item](../user_groups/user_groups_schemas.md/#user-group-list-item).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl https://app.solvexia.com/api/v1/users/u-11427/usergroups -X GET -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
[
  {
    "id": "ug-4321",
    "name": "Marketing Team"
  },
  {
    "id": "ug-234987",
    "name": "Project Team"
  }
]
```
---

## Create user account

Create a user account.

```apacheconfig
POST /v1/users
```

#### Path parameters
The path parameters are not expected.

#### Query parameters
The query parameters are not expected.

#### Request body

| Name | Type | Description | Required | Example |
| ---- | ---- | ------------| :------: | ------- |
| email | `string` | The new user’s email. | &#9745; | "email": "mona.benson<span>@sample.</span>com" |
| firstName | `string` | The new user’s first name. | &#9745; | "firstName": "Mona" |
| lastName | `string` | The new user’s last name. | &#9745; | "lastName": "Benson" |
| password | `string` | The new user’s password. Password must be at least 10 characters long and should contain at least 1 digit and 1 character in UPPERCASE. | &#9745; | "password": "Samplepassword12" |
| userRole | `enum` | The new user’s [role](./users_schemas.md/#user-roles). | &#9745; | "userRole": "Designer" |
| timezone | `enum` | The new user’s [timezone](./users_schemas.md/#time-zone). | &#9745; | "timezone": "(UTC+10:00) Canberra, Melbourne, Sydney" |

Example
```json
{
    "email": "mona.benson@sample.com",
    "firstName": "Mona",
    "lastName": "Benson",
    "password": "Samplepassword12",
    "userRole": "Designer",
    "timezone": "(UTC+10:00) Canberra, Melbourne, Sydney"
}
```

#### Response body
The successful response contains an array of instances of a [User](../users/users_schemas.md/#user).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl "https:///app.solvexia.com/api/v1/users" -X POST -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg" -H "Content-Type: application/json" -d '{"email": "mona.benson@sample.com", "firstName": "Mona", "lastName": "Benson","password": "Samplepassword12","userRole": "Designer","timezone": "(UTC+10:00) Canberra, Melbourne, Sydney"}'
```

Response

```json
{
    "id": "u-11427",
    "firstName": "Mona",
    "lastName": "Benson",
    "loginName": "template.mona.benson",
    "email": "mona.benson@sample.com",
    "accountStatus": "Active",
    "city": null,
    "country": null,
    "dateOfBirth": null,
    "department": null,
    "lastSignInDate": null,
    "phoneNumberLand": null,
    "phoneNumberMobile": null,
    "timezone": "(UTC+10:00) Canberra, Melbourne, Sydney",
    "userRole": "Designer"
}
```
---

## Disable user account

Disable a user account.

```apacheconfig
POST /v1/users/{userId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------| 
| userId | `string` | The user id to request. |

#### Query parameters
The query parameters are not expected.

#### Request body

| Name | Type | Description | Required | Example |
| ---- | ---- | ------------| :------: | ------- |
| accountStatus | `enum` | The new user’s [Account Status](./users_schemas.md/#account-status). | &#9745; | "accountStatus": "Suspended" |

Example
```json
{
    "accountStatus": "Suspended"
}
```

#### Response body
The successful response contains an array of instances of a [User](../users/users_schemas.md/#user).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl "https:///app.solvexia.com/api/v1/users/u-11427" -X POST -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg" -H "Content-Type: application/json" -d '{"accountStatus": "Suspended"}'
```

Response

```json
{
    "id": "u-11427",
    "firstName": "Mona",
    "lastName": "Benson",
    "loginName": "template.mona.benson",
    "email": "mona.benson@sample.com",
    "accountStatus": "Suspended",
    "city": "Sydney",
    "country": "Australia",
    "dateOfBirth": null,
    "department": null,
    "lastSignInDate": "2011-03-14T14:56:00.0000000",
    "phoneNumberLand": null,
    "phoneNumberMobile": null,
    "timezone": "(UTC+10:00) Canberra, Melbourne, Sydney",
    "userRole": "Designer"
}
```
---

## Get user permissions

Get a list of user permissions.

```apacheconfig
GET /v1/users/{userId}/permissions
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| userId | `string` | The user id to request. |

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must be empty.

#### Response body
The successful response contains a list of [Permission](../permissions/permissions_schemas.md/#permission).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl "https://app.solvexia.com/api/v1/users/u-11427/permisions" -X GET -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg" 
```

Response

```json
[
  {
    "resourceId": "p-2343",
    "resourceName": "Sales reconciliation",
    "role": "executor"
  },
  {
    "resourceId": "mt-4323",
    "resourceName": "Monthly Revenue",
    "role": "reader"
  }
]
```
---


## Add or update user permission for a given resource

Add or update resource permission of a user.

```apacheconfig
POST /v1/users/{userId}/permissions/{resourceId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| userId | `string` | The user id to request. |
| resourceId | `string` | The resource id to add or update. |

#### Query parameters
The query parameters are not expected.

#### Request body
```json
{
  "role": "editor"
}
```

#### Response body
The successful response contains a [Permission Role Type](../permissions/permissions_schemas.md/#permission-role-type).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl "https://app.solvexia.com/api/v1/users/u-11427/permisions/p-2343" -X POST -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg" -H "Content-Type: application/json" -d '{"role": "editor"}'
```

Response

```json
{
  "resourceId": "p-2343",
  "resourceName": "Sales reconciliation",
  "role": "editor"
}
```

---

## Delete user permission

Delete resource permission of a user.

```apacheconfig
DELETE /v1/users/{userId}/permissions/{resourceId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| userId | `string` | The user id to request. |
| resourceId | `string` | The resource id to delete. |

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must be empty.

#### Response body
The response body is empty.

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl "https://app.solvexia.com/api/v1/users/u-11427/permisions/p-2343" -X DELETE -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

200 OK

---

