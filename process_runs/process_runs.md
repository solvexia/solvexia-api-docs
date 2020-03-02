# Process Runs

| API Endpoints                           |
| --------------------------------------- |
| 1. [Get a process run](#get-a-process-run) |
| 2. [Start a process run](#start-a-process-run) |
| 3. [Cancel a process run](#Cancel-a-process-run) |
| 4. [Get process run status](#get-process-run-status) |
| 5. [Get a list of steps in a process run](#get-a-list-of-steps-in-a-process-run) |
| 6. [Get a step in a process run](#get-a-step-in-a-process-run) |
| 7. [Get data step properties](#get-data-step-properties) |
| 8. [Get data step property](#get-data-step-property) |
| 9. [Update data step property](#update-data-step-property) |

## Get a process run

Returns an instance of a [Process Run](./process_runs_schemas.md).

```apacheconfig
GET /v1/processRuns/{processRunId}
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
Successful response contains an instance of a [Process Run](./process_runs_schemas.md).

```json
{
    "id": "pr-12484",
    "name": "Weekly CFO Summary v2: Run #32",
    "process": "p-1321",
    "alertEmailAddress": "",
    "alertSMS": "",
    "runButtonName": "Run the process",
    "description": "Description here",
    "lastModifiedBy": "abc.user.uservich",
    "dateModified": "11/10/2019 2:09:32 AM",
    "dateCreated": "11/10/2019 2:09:32 AM"
}
```
