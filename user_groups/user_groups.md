# User Group APIs

[Get a user group list](#get-a-user-group-list)  
[Get a user group](#get-a-user-group)  
[Get members for a user group](#get-members-for-a-user-group)  
[Create a process run](#create-a-process-run)  
[Process run list of a process](#get-a-list-of-process-runs)  
[Data steps of a process](#get-process-data-steps)  

---

## Get a user group list

Lists all the user groups.

```apacheconfig
GET /api/v1/userGroups
```

#### Path parameters

This request does not have any path parameters.

#### Query parameters

The query parameters are not expected.

#### Request body
The request body must be empty.

#### Response

The successful response contains an array of instances of [User Group List Item](./user_groups_schemas.md/#user-group-list-item).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl https://app.solvexia.com/api/v1/userGroups -X GET -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

With query parameters

```shell
curl https://app.solvexia.com/api/v1/userGroups -X GET -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
[
  {
    "id": "ug-1234",
    "name": "Sales Team"
  },
  {
    "id": "ug-234987",
    "name": "Project Team"
  }
]
```
---

## Get a user group

Returns a user group at a given id.

```apacheconfig
GET /v1/userGroups/{userGroupId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| userGroupId | `string` | The id of a user group to request. |


#### Query parameters
The query parameters are not expected.

#### Request body
The request body must be empty.

#### Response body
The successful response contains an instance of a [UserGroup](./user_groups_schemas.md/#user-group).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl https://app.solvexia.com/api/v1/userGroups/ug-114273 -X GET -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
{
    "id": "ug-114273",
    "name": "Sales Team",
    "description": "Description for a user group"
}
```
---

## Get members for a user group

Get list of members for a user group.

```apacheconfig
POST /v1/userGroups/{userGroupId}/members
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| userGroupId | `string` | The user group id to get the members. |

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must be empty.

#### Response body
The successful response contains an array of instances of a [User](../users/users_schemas.md/#user).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl "https:///app.solvexia.com/api/v1/userGroups/ug-114273/members" -X POST -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
{
  "id": "pr-114283",
  "accountActive": false,
  "city": null,
  "country": null,
  "dateOfBirth": null,
  "department": null,
  "email": "tom.jordan@example.com",
  "firstName": "Tom",
  "lastName": "Jordan",
  "lastSignInDate": "2011-03-14T14:56:00.0000000",
  "loginName": "template.tom.jordan",
  "phoneNumberLand": null,
  "phoneNumberMobile": null,
  "timeZoneHasDaylightSavings": true,
  "timezone": "(UTC+10:00) Canberra, Melbourne, Sydney",
  "userRole": "Designer"
}
```
---
