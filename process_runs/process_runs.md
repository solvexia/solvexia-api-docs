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
    "description": "Description here",
    "lastModifiedBy": "abc.user.uservich",
    "dateModified": "11/10/2019 2:09:32 AM",
    "dateCreated": "11/10/2019 2:09:32 AM",
    "alertEmailAddress": "",
    "alertSMS": ""
}
```

## Start a process run

Request a start of a process run.

```apacheconfig
POST /v1/processRuns/{processRunId}/requests
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| processRunId | `string` | The process run id to request start run for. |

#### Query parameters
Query parameters are not expected.

#### Request body

| Name | Type | Description |
| ------------- |------------- | -------------|
| requestType | enum([ProcessRunRequestType](./process_runs_schemas.md)) | The request type `startRun` which identifies the start. |

#### Response body
Successful response contains a [Process Run Status](./process_runs_schemas.md).

```json
{
  "id": "pr-263",
  "dateFinished": null,
  "dateStarted": "",
  "runDurationInSec": 8,
  "status": "Running"
}
```

## Cancel a process run

Request to cancel a currently running process run.

```apacheconfig
POST /v1/processRuns/{processRunId}/requests
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| processRunId | `string` | The process run id to request to cancel running. |

#### Query parameters
Query parameters are not expected.

#### Request body

| Name | Type | Description |
| ------------- |------------- | -------------|
| requestType | enum([ProcessRunRequestType](./process_runs_schemas.md)) | The request type `cancelRun` which identifies cancel. |

#### Response body
Successful response contains a [Process Run Status](./process_runs_schemas.md).

```json
{
  "id": "pr-263",
  "dateFinished": null,
  "dateStarted": "",
  "runDurationInSec": 48,
  "status": "Cancelled"
}
```

## Get process run status

Request run status for a process run.

```apacheconfig
GET /v1/processRuns/{processRunId}/runStatus
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
Successful response contains a [Process Run Status](./process_runs_schemas.md).

```json
{
  "id": "pr-263",
  "dateFinished": null,
  "dateStarted": "",
  "runDurationInSec": 48,
  "status": "Cancelled"
}
```

## Get a list of steps in a process run

Request a list of steps in a process run.

```apacheconfig
GET /v1/processRuns/{processRunId}/steps
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| processRunId | `string` | The process run id to request a list of steps in a process run. |

#### Query parameters
Query parameters are not expected.

#### Request body

Request body must be empty.

#### Response body
Successful response contains a list of steps.

```json
[
  {
    "isEnabled": true,
    "id": "ds-524",
    "name": "1.1 Input parameters"
  },
  {
    "isEnabled": true,
    "id": "ds-582",
    "name": "2.1 Input parameters"
  }
]
```

## Get a step in a process run

Request an instance of a step in a process run.

```apacheconfig
GET /v1/processRuns/{processRunId}/steps/{stepId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| processRunId | `string` | The process run id to request a step in a process run. |
| stepId | `string` | The data step id to request a step in a process run. |

#### Query parameters
Query parameters are not expected.

#### Request body

Request body must be empty.

#### Response body
Successful response contains an instance of a data step.

```json
{
  "isEnabled": true,
  "id": "ds-524",
  "name": "1.1 Input parameters"
}
```

## Get data step properties

Request a list of data step properties in a step.

```apacheconfig
GET /v1/processRuns/{processRunId}/steps/{stepId}/properties
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| processRunId | `string` | The process run id to request a step from. |
| stepId | `string` | The data step id to request properties from. |

#### Query parameters
Query parameters are not expected.

#### Request body

Request body must be empty.

#### Response body
Successful response contains a list of [Data Step Properties](./process_runs_schemas.md).

```json
[
  {
    "id": "dsprop-524",
    "name": "Start date",
    "dataType": "Datepicker",
    "required": false,
    "visible": true,
    "informationFlowType": "INPUT",
    "mouseOverText": "1.2 Start date"
  }
]
```

## Get data step property

Request an instance of a data step property.

```apacheconfig
GET /v1/processRuns/{processRunId}/steps/{stepId}/properties/{propertyId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| processRunId | `string` | The process run id to request a data step property from. |
| stepId | `string` | The data step id to request a property from. |
| propertyId | `string` | The data step property id to request. |

#### Query parameters
Query parameters are not expected.

#### Request body

Request body must be empty.

#### Response body
Successful response contains an instance of a [Data Step Property](./process_runs_schemas.md).

```json
{
  "id": "dsprop-524",
  "name": "Start date",
  "dataType": "Datepicker",
  "required": false,
  "visible": true,
  "informationFlowType": "INPUT",
  "mouseOverText": "1.2 Start date",
  "value": "22-Jul-2019"
}
```

## Update data step property

Returns an instance of an updated data step property.

```apacheconfig
GET /v1/processRuns/{processRunId}/steps/{stepId}/properties/{propertyId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| processRunId | `string` | The process run id to request an update of a data step property from. |
| stepId | `string` | The data step id to request an update of a data step property from. |
| propertyId | `string` | The data step property id to request. |

#### Query parameters
Query parameters are not expected.

#### Request body

Request body must contain a valid [Data Step Property](./process_runs_schemas.md).

#### Response body
Successful response contains an id of an updated [Data Step Property](./process_runs_schemas.md) Object.

```json
{
  "id": "dsprop-456",
  "name": "Add a number",
  "dataType": "Number",
  "required": true,
  "visible": true,
  "informationFlowType": "INPUT",
  "mouseOverText": "1.2 Add a number",
  "value": "235"
}
```