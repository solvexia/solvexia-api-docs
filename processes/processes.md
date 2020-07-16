# Process APIs

[Get a process list](#get-a-process-list)  
[Get a process](#get-a-process)  
[Create a process run](#create-a-process-run)  
[Process run list of a process](#get-a-list-of-process-runs)  
[Data steps of a process](#get-process-data-steps)  

---

## Get a process list

Lists all processes the user has access to. The caller can supply filters to adjust the results.

```apacheconfig
GET /api/v1/processes
```

#### Path parameters

This request does not have any path parameters.

#### Query parameters

| Name | Type |Description |
| ------------- |------------- | -------------|
|name|`string`|Filters the results by the process name.|
|dateCreatedStart|`string`|The filter to return processes with `dateCreated` parameter older than `dateCreatedStart`.  |
|dateCreatedEnd|`string`|The filter to return processes with `dateCreated` parameter earlier than `dateCreatedEnd`. |

#### Request body
The request body must be empty.

#### Response

The successful response contains an array of instances of [Process List Item](./schemas.md/#process-list-item).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl https://app.solvexia.com/api/v1/processes -X GET -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
[
  {
    "id": "p-1234",
    "name": "Weekly CFO Summary v2"
  },
  {
    "id": "p-234987",
    "name": "Sales reconciliation"
  }
]
```
---

## Get a process

Returns a process at a given id.

```apacheconfig
GET /v1/processes/{processId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| processId | `string` | The id of a process to request. |


#### Query parameters
The query parameters are not expected.

#### Request body
The request body must be empty.

#### Response body
The successful response contains an instance of a [Process](./schemas.md/#process).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl https://app.solvexia.com/api/v1/processes/p-114273 -X GET -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
{
    "id": "p-114273",
    "name": "processapitest",
    "alertEmailAddress": "",
    "alertSMS": "",
    "availableToSubscriber": false,
    "runsAvailableToSubscriber": false,
    "description": "Description here",
    "lastModifiedBy": "usa.john.adams",
    "dateModified": "2020-06-15T02:21:35.1500000",
    "dateCreated": "2020-06-15T02:21:32.2300000"
}
```
---

## Create a process run

Creates a process run of a process, returning the newly created process run. The process run itself is created, but not started.

```apacheconfig
POST /v1/processes/{processId}/processruns
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| processId | `string` | The process id to create a process run from. |

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must be empty.

#### Response body
The successful response contains an instance of a [Process Run](../process_runs/process_runs_schemas.md/#process-run).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl "https:///app.solvexia.com/api/v1/processes/p-114273/processruns" -X POST -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
{
  "id": "pr-114283",
  "name": "processapitest : run #2",
  "process": "p-114273",
  "alertEmailAddress": "",
  "alertSMS": "",
  "description": "Description here",
  "lastModifiedBy": "usa.john.adams",
  "dateModified": "2020-06-17T04:55:54.5430000",
  "dateCreated": "2020-06-17T04:55:54.5430000"
}
```
---

## Get a list of process runs

Returns a list of process runs for a process.

```apacheconfig
GET /v1/processes/{processId}/processruns
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| processId | `string` | The process id to get a list of process runs for a process. |

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must be empty.

#### Response body
The successful response contains an array of instances [Process Run List Item](./schemas.md/#process-list-item).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl "https:///app.solvexia.com/api/v1/processes/p-114273/processruns" -X GET -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

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
---
## Get process data steps

Returns a list of data steps of a process.

```apacheconfig
GET /v1/processes/{processId}/steps
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| processId | `string` | The process id to get a list of data steps for. |

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must be empty.

#### Response body
The successful response contains an array of instances of [Data Step](../steps/datastep_schemas.md/#data-step).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl "https:///app.solvexia.com/api/v1/processes/p-114273/steps" -X GET -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
[
    {
        "isEnabled": true,
        "stepOrder": "1.1",
        "id": "ds-114274",
        "name": "New data step"
    },
    {
        "isEnabled": true,
        "stepOrder": "1.2",
        "id": "ds-114275",
        "name": "New data step 2"
    }
]
```
---
