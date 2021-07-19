# Data Step APIs

[Get a data step](#get-a-data-step)  
[Get data step properties](#get-data-step-properties)  
[Get data step property](#get-data-step-property)  
[Update data step property](#update-data-step-property)

---

## Get a data step

Returns a data step of a process.

```apacheconfig
GET /v1/steps/{stepId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| stepId | `string` | The data step id to request. |

#### Query parameters
The query parameters are not expected.

#### Request body

The request body must be empty.

#### Response body
Successful response contains an instance of [Data Step](../steps/datastep_schemas.md/#data-step).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl "https:///app.solvexia.com/api/v1/steps/ds-114274" -X GET -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
{
    "isEnabled": true,
    "stepOrder": "1.1",
    "id": "ds-114274",
    "name": "New Step Name"
}
```
---

## Get data step properties

Returns a list of properties in a data step.

```apacheconfig
GET /v1/steps/{stepId}/properties
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| stepId | `string` | The data step id to request properties from. |

#### Query parameters
The query parameters are not expected.

#### Request body

The request body must be empty.

#### Response body
The successful response contains an array of instances of [Data Step Property](./datastep_schemas.md/#data-step-property).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl "https:///app.solvexia.com/api/v1/steps/ds-114274/properties" -X GET -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
[
    {
        "value": 324234,
        "id": "dsprop-12232",
        "name": "Untitled Number Property",
        "dataType": "Number",
        "required": false,
        "visible": true,
        "informationFlowType": "NONE",
        "mouseoverText": "mouseover"
    },
    {
        "value": 11111,
        "id": "dsprop-12233",
        "name": "Untitled Number Property",
        "dataType": "Number",
        "required": false,
        "visible": true,
        "informationFlowType": "NONE",
        "mouseoverText": "mouseover"
    }
]
```
---

## Get data step property

Returns a data step property for a data step.

```apacheconfig
GET /v1/steps/{stepId}/properties/{propertyId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| stepId | `string` | The data step id to request a property from. |
| propertyId | `string` | The data step property id to request. |

#### Query parameters
The query parameters are not expected.

#### Request body

The request body must be empty.

#### Response body
The successful response contains an instance of [Data Step Property](./datastep_schemas.md/#data-step-property).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl "https:///app.solvexia.com/api/v1/steps/ds-114274/properties/dsprop-524" -X GET -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
{
    "value": 324234,
    "id": "dsprop-524",
    "name": "Untitled Number Property",
    "dataType": "Number",
    "required": false,
    "visible": true,
    "informationFlowType": "NONE",
    "mouseoverText": "mouseover"
}
```
---

## Update data step property

Updates a data step property in a data step.

```apacheconfig
POST /v1/steps/{stepId}/properties/{propertyId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| stepId | `string` | The data step id to request an update of a data step property from. |
| propertyId | `string` | The data step property id to request. |

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must contain an instance of [Data Step Property](./datastep_schemas.md/#data-step-property).

#### Response body
The successful response contains an instance of [Data Step Property](./datastep_schemas.md/#data-step-property).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl "https:///app.solvexia.com/api/v1/steps/ds-114274/properties/dsprop-524" -X POST -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg" -H "Content-Type: application/json" -d '{"name":"Start date changed","dataType":"Number","required":false,"visible":true,"informationFlowType":"INPUT","mouseOverText":"1.3 Start date changed","value":10}'
```

Response

```json
 {
    "value": 10,
    "id": "dsprop-524",
    "name": "Start date changed",
    "dataType": "Number",
    "required": false,
    "visible": true,
    "informationFlowType": "INPUT",
    "mouseOverText": "1.3 Start date changed"
  }
```
---