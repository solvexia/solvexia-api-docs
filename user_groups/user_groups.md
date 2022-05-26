# User Group APIs

[Get a user group list](#get-a-user-group-list)  
[Get a user group](#get-a-user-group)  
[Get members for a user group](#get-members-for-a-user-group) <br />
[Add member to a user group](#add-member-to-a-user-group) <br />
[Remove member from a user group](#remove-member-from-a-user-group) <br />
[Get user group permissions](#get-user-group-permissions) 
[Add or update user group permission for a given resource](#add-or-update-user-group-permission-for-a-given-resource)  
[Delete or update user group permission](#delete-user-group-permission)

---

## Get a user group list

List all the user groups.

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

Get a list of members for a user group.

```apacheconfig
GET /v1/userGroups/{userGroupId}/members
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| userGroupId | `string` | The user group id to request. |

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must be empty.

#### Response body
The successful response contains an array of instances of a [Member](./user_groups_schemas.md/#member).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl "https://app.solvexia.com/api/v1/userGroups/ug-114273/members" -X GET -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
[
  {
    "id": "u-1233",
    "loginName": "template.tom.jordan"
  },
  {
    "id": "u-1463",
    "loginName": "template.jack.mayer"
  }
]
```
---

## Add member to a user group

Add a member to a user group.

```apacheconfig
POST /v1/userGroups/{userGroupId}/members/{userId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| userGroupId | `string` | The user group id to request. |
| userId | `string` | The user id to add. |

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must be empty.

#### Response body
The successful response contains a [Member](./user_groups_schemas.md/#member).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl "https://app.solvexia.com/api/v1/userGroups/ug-114273/members/u-1233" -X POST -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
{
  "id": "u-1233",
  "loginName": "template.tom.jordan"
}
```

---

## Remove member from a user group

Remove a member from a user group.

```apacheconfig
DELETE /v1/userGroups/{userGroupId}/members/{userId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| userGroupId | `string` | The user group id to request. |
| userId | `string` | The user id to remove. |

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
curl "https://app.solvexia.com/api/v1/userGroups/ug-114273/members/u-1233" -X DELETE -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

200 OK

---

## Get user group permissions

Get a list of user group permissions.

```apacheconfig
GET /v1/userGroups/{userGroupId}/permissions
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| userGroupId | `string` | The user group id to request. |

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
curl "https://app.solvexia.com/api/v1/userGroups/ug-114273/permisions" -X GET -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
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

## Add or update user group permission for a given resource

Add or update resource permission of a user group.

```apacheconfig
POST /v1/userGroups/{userGroupId}/permissions/{resourceId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| userGroupId | `string` | The user group id to request. |
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
curl "https://app.solvexia.com/api/v1/userGroups/ug-114273/permisions/p-2343" -X POST -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg" -H "Content-Type: application/json" -d '{"role": "editor"}'
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

## Delete user group permission

Delete resource permission of a user group.

```apacheconfig
DELETE /v1/userGroups/{userGroupId}/permissions/{resourceId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| userGroupId | `string` | The user group id to request. |
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
curl "https://app.solvexia.com/api/v1/userGroups/ug-114273/permisions/p-2343" -X DELETE -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

200 OK

---

