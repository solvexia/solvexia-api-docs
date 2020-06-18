# Table APIs

[Get a table](#get-a-table)  
[Create a table](#create-a-table)  
[Update a table](#update-a-table)  
[Get Columns of a table](#get-columns-of-a-table)  
[Create a Column](#create-a-column)  
[Update a Column](#update-a-column)  
[Delete a column](#delete-a-column)

---

## Get a table

Get a Table

```apacheconfig
GET /v1/tables/{tableId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| tableId | `string` | The table id to of a table. |

#### Query parameters
Query parameters are not expected.

#### Request body

Request body must be empty.

#### Response body
Successful response contains a [table](./tables_schemas.md/#table-object) json.

### Example

Request

```shell
curl "https://app.solvexia.com/api/v1/tables/mt-6239" -X GET -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
{
    "id": "mt-6239",
    "name": "publicapitable2",
    "description": "hurhurt",
    "dateCreated": "2020-06-04T07:48:12.707",
    "dateModified": "2020-06-04T07:48:12.707",
    "sizeInBytes": 16384.00,
    "version": 9
}
```
---

## Create a table

Creates a table

```apacheconfig
POST /v1/tables
```

#### Path parameters

Path parameters are not expected.

#### Query parameters
Query parameters are not expected.

#### Request body
Request body must contain a valid [Table object](./tables_schemas/#table-object) json.
with the following fields
```javascript
{ 
  "name" : string,
  "description": string
}
```

| Name | Type | Description |
| ------------- |------------- | -------------|
| name | `string` | Name of the table, must be unique. |
| description | `string` | description of the table. |

#### Response body
Successful response contains a [Table object](./tables_schemas/#table-object) json.

### Example

Request

```shell
curl "https://app.solvexia.com/api/v1/tables" -X POST -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg" -H "Content-Type: application/json" -d '{"name": "publicapitable3","description": "hurhurt2"}'
```

Response

```json
{
    "id": "mt-8239",
    "name": "publicapitable3",
    "description": "hurhurt2",
    "dateCreated": "2020-06-18T00:50:09.323",
    "dateModified": "2020-06-18T00:50:09.323",
    "sizeInBytes": 0.00,
    "version": 2
}
```
---

## Update a table

Updates a table

```apacheconfig
POST /v1/tables/{tableId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| tableId | `string` | The table id to of a table. |

#### Query parameters
Query parameters are not expected.

#### Request body
Request body must contain a valid [Table object](./tables_schemas/#table-object) json.
with one or more of the following fields
```javascript
{ 
  "name" : string,
  "description": string
}
```

| Name | Type | Description |
| ------------- |------------- | -------------|
| name | `string` | Name of the table, must be unique. |
| description | `string` | description of the table. |

#### Response body
Successful response contains a [Table object](./tables_schemas/#table-object) json.

### Example

Request

```shell
curl "https://app.solvexia.com/api/v1/tables/mt-8239" -X POST -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg" -H "Content-Type: application/json" -d '{"name": "publicapitable5","description": "hurhurt5"}'
```

Response

```json
{
    "id": "mt-8239",
    "name": "publicapitable5",
    "description": "hurhurt5",
    "dateCreated": "2020-06-18T00:50:09.323",
    "dateModified": "2020-06-18T00:50:09.323",
    "sizeInBytes": 0.00,
    "version": 2
}
```
---

## Get Columns of a table

Gets the columns of a table

```apacheconfig
GET /v1/tables/{tableId}/columns
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| tableId | `string` | The table id to of a table. |

#### Query parameters
Query parameters are not expected.

#### Request body

Request body must be empty.

#### Response body
Successful response contains an array of [column](./tables_schemas.md/#column-object) json.

### Example

Request

```shell
curl "https://app.solvexia.com/api/v1/tables/mt-6239/columns" -X GET -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
[
    {
        "name": "_Record_ID",
        "dataType": "Number",
        "defaultValue": null,
        "fieldLength": null,
        "nullable": false
    },
    {
        "name": "colfixed",
        "dataType": "FixedLengthText",
        "defaultValue": null,
        "fieldLength": 255,
        "nullable": true
    },
    {
        "name": "colcreate",
        "dataType": "FixedLengthText",
        "defaultValue": null,
        "fieldLength": 252,
        "nullable": true
    }
]
```
---

## Create a Column

Creates a column for a table

```apacheconfig
POST /v1/tables/{tableId}/columns/
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| tableId | `string` | The table id to of a table. |

#### Query parameters
Query parameters are not expected.

#### Request body
Request body must contain a valid [column](./tables_schemas.md/#column-object) json.
'name' and 'dataType' are required.
```javascript
{ 
  "name" : string,
  "dataType": TableColumnDataType,
  "nullable": boolean,
  "fieldLength": number,
  "defaultValue": string/number/boolean
}
```

| Name | Type | Description |
| ------------- |------------- | -------------|
| name | `string` | REQUIRED. Name of the table, must be unique. |
| dataType | `TableColumnDataType` |REQUIRED. [ColumnType](#table-column-type) . |
| nullable | `boolean` | OPTIONAL. Whether a column can accept null values, default true |
| fieldLength | `number` | OPTIONAL. Number of characters for 'FixedLengthText' dataType, default null  (which sets fixedLengthText to MAX) |
| nullable | `boolean` | OPTIONAL. Whether a column can accept null values, default true |
| defaultValue | `string/number/boolean` | OPTIONAL. The default value for the column, based on dataType |

#### Response body
Successful response contains a [column](./tables_schemas.md/#column-object) json.

### Example

Request

```shell
curl "https://app.solvexia.com/api/v1/tables/mt-8239/columns" -X POST -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg" -H "Content-Type: application/json" -d '{ "name" : "col4","dataType": "number","defaultValue":5,"nullable":false}'
```

Response

```json
{ 
  "name" : "col4",
  "dataType": "number",
  "defaultValue":5,
  "fieldLength": null,
  "nullable":false
}
```
---

## Update a Column

Updates a column for a table

```apacheconfig
POST /v1/tables/{tableId}/columns/{columnName}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| tableId | `string` | The table id to of a table. |
| ColumnName | `string` | The name of a column, you may indicate a column with spaces either by url-encoded spaces or '_' e.g. for 'column space' it can be 'column%20space' or 'column_space' . |

#### Query parameters
Query parameters are not expected.

#### Request body
Request body must contain a valid [column](./tables_schemas.md/#column-object) json.
one or more of the following is required.
```javascript
{ 
  "name" : string,
  "dataType": TableColumnDataType,
  "nullable": boolean,
  "fieldLength": number,
  "defaultValue": string/number/boolean
}
```

| Name | Type | Description |
| ------------- |------------- | -------------|
| name | `string` | Name of the table, must be unique. |
| dataType | `TableColumnDataType` | [ColumnType](#table-column-type) . |
| nullable | `boolean` | Whether a column can accept null values, default true |
| fieldLength | `number` | Number of characters for 'FixedLengthText' dataType, default (max) |
| nullable | `boolean` | Whether a column can accept null values, default true |
| defaultValue | `string/number/boolean` | The default value for the column, based on dataType |

#### Response body
Successful response contains a [column](./tables_schemas.md/#column-object) json.

### Example

Request

```shell
curl "https://app.solvexia.com/api/v1/tables/mt-8239/columns" -X POST -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg" -H "Content-Type: application/json" -d '{ "name" : "col4","dataType": "number","defaultValue":5,"nullable":false}'
```

Response

```json
{
    "name": "col4",
    "dataType": "TrueFalse",
    "defaultValue": 5,
    "fieldLength": null,
    "nullable": false
}
```
---

## Delete a column

Delete a column

```apacheconfig
DELETE /v1/tables/{tableId}/columns/{columnName}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| tableId | `string` | The table id to of a table. |
| ColumnName | `string` | The name of a column, you may indicate a column with spaces either by url-encoded spaces or '_' e.g. for 'column space' it can be 'column%20space' or 'column_space' . |

#### Query parameters
Query parameters are not expected.

#### Request body

Request body must be empty.

#### Response body
There is no Response Body

### Example

Request

```shell
curl "https://app.solvexia.com/api/v1/tables/mt-6239/columns/col1" -X DELETE -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

200 OK

---