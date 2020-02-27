# Processes

1. [List users processes](#list-users-processes)
2. [Get a process](#get-a-process)

## List users processes

List all processes available to the user.

```apacheconfig
GET /api/v1/processes
```

#### Path parameters

This request does not have any path parameters.

#### Query parameters

| Name | Type |Description |
| ------------- |------------- | -------------|
|name|`string`|Filters the results by the process name. When it is not present, returns all the processes that user has access to. |

#### Request body
Request body must be empty.

#### Response

Successful response contains a list of [Process List Item](./schemas.md/#process-list-item)s.

```json
[
  {
    "id": "p-1234",
    "name": "Weekly CFO Summary v2"
  },
  {
    "id": "p-2347",
    "name": "Sales reconciliation"
  }
]
```

## Get a process

Returns an instance of a [Process](./schemas.md/#process).

```apacheconfig
GET /v1/processes/{processId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| processId | `string` | The process id to request. |


#### Query parameters
Query parameters are not expected.

#### Request body
Request body must be empty.

#### Response body
Successful response contains an instance of a [Process](./schemas.md/#process).

```json
{
    "id": "p-12484",
    "name": "testp04",
    "alertEmailAddress": "",
    "alertSMS": "",
    "availableToSubscriber": false,
    "runsAvailableToSubscriber": false,
    "description": "Description here",
    "lastModifiedBy": "abc.user.uservich",
    "dateModified": "11/10/2019 2:09:32 AM",
    "dateCreated": "11/10/2019 2:09:32 AM"
}
```