# Process Runs APIs

[Get a process run](#get-a-process-run)  
[Start a process run](#start-a-process-run)  
[Cancel a process run](#Cancel-a-process-run)  
[Get process run status](#get-process-run-status)  
[Get a list of Data steps in a process run](#get-process-run-data-steps)

---

## Get a process run

Returns a [Process Run](./process_runs_schemas.md/#process-run).

```apacheconfig
GET /v1/processruns/{processRunId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| processRunId | `string` | The process run id to request. |

#### Query parameters
Query parameters are not expected.

#### Request body
Request body must be empty.

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
    "lastModifiedBy": "Not Found",
    "dateModified": "2020-06-15T02:24:14.2700000",
    "dateCreated": "2020-06-15T02:24:14.2700000"
}
```
---

## Start a process run

Start a process run.

```apacheconfig
POST /v1/requests
```

#### Path parameters
Path parameters are not expected

#### Query parameters
Query parameters are not expected.

#### Request body
Request body must contain a [Process Run Request](./process_runs_schemas.md/#process-run-request)
and 'request' property must be 'ProcessRun_CancelRq'

```json
{
  "request":"ProcessRun_StartRq",
  "processRunId":"pr-114278"
}
```

#### Response body
Successful response contains [Process Run Status](./process_runs_schemas.md/#process-run-status).

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

## Cancel a process run

Cancel a currently running process run.

```apacheconfig
POST /v1/requests
```

#### Path parameters
Path parameters are not expected

#### Query parameters
Query parameters are not expected.

#### Request body
Request body must contain a [Process Run Request](./process_runs_schemas.md/#process-run-request)
and 'request' property must be 'ProcessRun_CancelRq'

```json
{
  "request":"ProcessRun_CancelRq",
  "processRunId":"pr-114278"
}
```

#### Response body
Successful response contains a [Process Run Status](./process_runs_schemas.md/#process-run-status).

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

Get Run Status of a Process Run.

```apacheconfig
GET /v1/processRuns/{processRunId}/runstatus
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| processRunId | `string` | The process run id to request a run status for. |

#### Query parameters
Query parameters are not expected.

#### Request body

Request body must be empty.

#### Response body
Successful response contains a [Process Run Status](./process_runs_schemas.md/#process-run-status).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl -X GET "https://app.solvexia.com/api/v1/processruns/pr-114278/runstatus" -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
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

## Get Process Run Data Steps

Returns a list of all Data Steps for a specific process run.

```apacheconfig
GET /v1/processruns/{processRunId}/steps
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| processrunId | `string` | The process run id to request a list of steps in a process run. |

#### Query parameters
Query parameters are not expected.

#### Request body

Request body must be empty.

#### Response body
Successful response contains an array of [dataSteps](../steps/datastep_schemas.md/#data-step) for a process.

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