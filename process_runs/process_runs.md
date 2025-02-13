# Process Run APIs

[Get a process run](#get-a-process-run)  
[Start a process run](#start-a-process-run)  
[Cancel a process run](#cancel-a-process-run)   
[[Deprecated] Start a process run](#deprecated-start-a-process-run)  
[[Deprecated] Cancel a process run](#deprecated-cancel-a-process-run)  
[Get process run status](#get-process-run-status)  
[Get a list of data steps in a process run](#get-process-run-data-steps)  
[Get a run status of a step in a process run](#get-a-run-status-of-a-step-in-a-process-run)  
[Restart a step in a process run](#restart-a-step-in-a-process-run)  

---

## Get a process run

Returns a process run at the given id.

```apacheconfig
GET /v1/processruns/{processRunId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| processRunId | `string` | The process run id to request. |

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must be empty.

#### Response body
Successful response contains a [Process Run](./process_runs_schemas.md/#process-run).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl https://app.solvexia.com/api/v1/processruns/pr-114278 -X GET -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
{
    "id": "pr-114278",
    "name": "processapitest : run #1",
    "process": "p-114273",
    "alertEmailAddress": "",
    "alertSMS": "",
    "description": "Description here",
    "lastModifiedBy": "usa.john.adams",
    "dateModified": "2020-06-15T02:24:14.2700000",
    "dateCreated": "2020-06-15T02:24:14.2700000"
}
```
---

## Start a process run

Start a process run.

```apacheconfig
POST /v1/processruns/{processRunId}/start
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| processRunId | `string` | The process run id to start. |

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must be empty.

#### Response body
The successful response contains an instance of [Process Run Status](./process_runs_schemas.md/#process-run-status).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl -X POST "https://app.solvexia.com/api/v1/processruns/pr-114278/start" -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
{
  "id": "pr-114278",
  "dateStarted": null,
  "dateFinished": null,
  "runDurationInSeconds": null,
  "status": "Scheduled"
}
```
---

## Cancel a process run

Cancel a process run.

```apacheconfig
POST /v1/processruns/{processRunId}/cancel
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| processRunId | `string` | The process run id to cancel. |

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must be empty.

#### Response body
The successful response contains an instance of [Process Run Status](./process_runs_schemas.md/#process-run-status).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl -X POST "https://app.solvexia.com/api/v1/processruns/pr-263/cancel" -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
{
  "id": "pr-263",
  "dateFinished": null,
  "dateStarted": "",
  "runDurationInSec": 48,
  "status": "Cancelled"
}
```
---

## [Deprecated] Start a process run

Starts a process run.

```apacheconfig
POST /v1/requests
```

#### Path parameters
The path parameters are not expected.

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must contain an instance of [Process Run Request](./process_runs_schemas.md/#process-run-request). `request` property must be `ProcessRun_StartRq`.

```json
{
  "request": "ProcessRun_StartRq",
  "processRunId": "pr-114278"
}
```

#### Response body
The successful response contains an instance of [Process Run Status](./process_runs_schemas.md/#process-run-status).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl -X POST "https://app.solvexia.com/api/v1/requests" -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg" -H "Content-Type: application/json" -d '{"request":"ProcessRun_StartRq","processRunId":"pr-114278"}'
```

Response

```json
{
  "id": "pr-114278",
  "dateStarted": null,
  "dateFinished": null,
  "runDurationInSeconds": null,
  "status": "Scheduled"
}
```
---

## [Deprecated] Cancel a process run

Cancels a currently running process run.

```apacheconfig
POST /v1/requests
```

#### Path parameters
The path parameters are not expected.

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must contain an instance of [Process Run Request](./process_runs_schemas.md/#process-run-request). `request` property must be `ProcessRun_CancelRq`.

```json
{
  "request": "ProcessRun_CancelRq",
  "processRunId": "pr-114278"
}
```

#### Response body
The successful response contains an instance of [Process Run Status](./process_runs_schemas.md/#process-run-status).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl -X POST "https://app.solvexia.com/api/v1/requests" -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg" -H "Content-Type: application/json" -d '{"request":"ProcessRun_CancelRq","processRunId":"pr-114278"}'
```

Response

```json
{
  "id": "pr-263",
  "dateFinished": null,
  "dateStarted": "",
  "runDurationInSec": 48,
  "status": "Cancelled"
}
```
---

## Get process run status

Returns run status of a process run.

```apacheconfig
GET /v1/processRuns/{processRunId}/runstatus
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| processRunId | `string` | The process run id to request a run status for. |

#### Query parameters
The query parameters are not expected.

#### Request body

The request body must be empty.

#### Response body
The successful response contains an instance of [Process Run Status](./process_runs_schemas.md/#process-run-status).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl -X GET "https://app.solvexia.com/api/v1/processruns/pr-114278/runstatus" -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
{
    "id": "pr-114278",
    "dateStarted": "2025-02-05T22:40:19.923",
    "dateFinished": "2025-02-05T22:55:51.923",
    "runDurationInSeconds": 932,
    "status": "Cancelled"
}
```
---

## Get process run data steps

Returns a list of data steps for a process run.

```apacheconfig
GET /v1/processruns/{processRunId}/steps
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| processrunId | `string` | The process run id to request a list of data steps from. |

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
curl "https:/app.solvexia.com/api/v1/processruns/pr-114278/steps" -X GET -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
[
    {
        "isEnabled": true,
        "stepOrder": "1.1",
        "id": "ds-114279",
        "name": "New data step"
    },
    {
        "isEnabled": true,
        "stepOrder": "1.2",
        "id": "ds-114278",
        "name": "New data step 2"
    }
]
```
---

## Get a run status of a step in a process run

Return a run status of a step in a process run.

```apacheconfig
GET /v1/processruns/{processRunId}/steps/{stepId}/runstatus
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| processRunId | `string` | The process run id of a step. |
| stepId | `string` | The step id to request a run status for. |

#### Query parameters
The query parameters are not expected.

#### Request body

The request body must be empty.

#### Response body
The successful response contains an instances of [Step Run Status](../steps/steps_schemas.md/#step-run-status).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl -X GET "https://app.solvexia.com/api/v1/processruns/pr-114278/steps/as-20682/runstatus" -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
{
    "id": "as-20682",
    "dateFinished": null,
    "dateStarted": "2025-01-13T03:51:03.27Z",
    "runDurationInSec": 2,
    "status": "cancelled",
    "completionMessage": ""
}
```
---

## Restart a step in a process run

Restart a process run from a step.

```apacheconfig
POST /v1/processruns/{processRunId}/steps/{stepId}/restartfromhere
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| processRunId | `string` | The process run id of a step. |
| stepId | `string` | The step id to request a restart. |

#### Query parameters
The query parameters are not expected.

#### Request body

The request body must be empty.

#### Response body
The successful response contains an instances of [Step Run Status](../steps/steps_schemas.md/#step-run-status).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl -X POST "https://app.solvexia.com/api/v1/processruns/pr-114278/steps/as-20682/restartfromhere" -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
{
    "id": "as-20682",
    "dateFinished": null,
    "dateStarted": "2025-01-13T03:51:03.27Z",
    "runDurationInSec": 2,
    "status": "Running",
    "completionMessage": "step is currently running"
}
```
---