# Data Step APIs

[Get a data step](#get-a-data-step)  
[Get data step properties](#get-data-step-properties)  
[Get data step property](#get-data-step-property)  
[Update data step property](#update-data-step-property)

---

## Get a data step

Get a data step

```apacheconfig
GET /v1/steps/{stepId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| stepId | `string` | The data step id to request a step in a process run. |

#### Query parameters
Query parameters are not expected.

#### Request body

Request body must be empty.

#### Response body
Successful response contains a [dataStep](../steps/datastep_schemas.md/#data-step).

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

Request a list of data step properties in a step.

```apacheconfig
GET /v1/steps/{stepId}/properties
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| stepId | `string` | The data step id to request properties from. |

#### Query parameters
Query parameters are not expected.

#### Request body

Request body must be empty.

#### Response body
Successful response contains an array of the derived [Data Step Properties](./datastep_schemas.md/#data-step-property) types.

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

Get a data step property for a data step.

```apacheconfig
GET /v1/steps/{stepId}/properties/{propertyId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| stepId | `string` | The data step id to request a property from. |
| propertyId | `string` | The data step property id to request. |

#### Query parameters
Query parameters are not expected.

#### Request body

Request body must be empty.

#### Response body
Successful response contains a derived [Data Step Property](#./datastep_schemas.md/#data-step-property) type.

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

Updates a data step property

```apacheconfig
POST /v1/steps/{stepId}/properties/{propertyId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| stepId | `string` | The data step id to request an update of a data step property from. |
| propertyId | `string` | The data step property id to request. |

#### Query parameters
Query parameters are not expected.

#### Request body
Request body must contain a valid [Data Step Property](#./datastep_schemas.md/#data-step-property) type.
Every field must be supplied except for 'id' which is unecessary (as it is in the url)

#### Response body
Successful response contains a derived [Data Step Property](#./datastep_schemas.md/#data-step-property) type.

### Example

Request

```shell
curl "https:///app.solvexia.com/api/v1/steps/ds-114274/properties/dsprop-524" -X POST -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg" -H "Content-Type: application/json" -d '{"name":"Start date changed","dataType":"Number","required":false,"visible":true,"informationFlowType":"INPUT","mouseOverText":"1.3 Start date changed","value":10}'
```

Response

```json
 {
    "value": 10,
    "name": "Start date changed",
    "dataType": "Number",
    "required": false,
    "visible": true,
    "informationFlowType": "INPUT",
    "mouseOverText": "1.3 Start date changed"
  }
```
---