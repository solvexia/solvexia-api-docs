# Processes

1. [List users processes](#list-users-processes)
2. [Get a process](#get-a-process)
3. [Create a process run](#create-a-process-run)
4. [Get a list of process runs](#get-a-list-of-process-runs)

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

## Create a process run

Returns an id of a newly created process run. The run itself is created, but not started.

```apacheconfig
POST /v1/processes/{processId}/processRuns
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| processId | `string` | The process id to create a process run from. |

#### Query parameters
Query parameters are not expected.

#### Request body
Request body must be empty.

#### Response body
Successful response contains an id of a newly created process run.

```json
{
  "id": "pr-12484"
}
```

## Get a list of process runs

Returns a list of all created runs of a specified process.

```apacheconfig
GET /v1/processes/{processId}/processRuns
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| processId | `string` | The process id to get a list of runs for. |

#### Query parameters
Query parameters are not expected.

#### Request body
Request body must be empty.

#### Response body
Successful response contains a list of all runs created from a process. Schema [Process List Item](./schemas.md/#process-list-item).

```json

[
  {
      "id": "pr-1234"
    , "name": "Weekly CFO Summary v2: Run #32"
  }
  , {
      "id": "pr-1235"
    , "name": "Weekly CFO Summary v2: Run #33"
  }
]
```