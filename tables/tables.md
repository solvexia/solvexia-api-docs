# Table APIs

[Get a table](#get-a-table)  
[Create a table](#create-a-table)  
[Update a table](#update-a-table)  
[Get columns of a table](#get-columns-of-a-table)  
[Create a column](#create-a-column)  
[Update a column](#update-a-column)  
[Delete a column](#delete-a-column)

---

## Get a table

Returns the table at the given table id.

```apacheconfig
GET /v1/tables/{tableId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| tableId | `string` | The table to request. |

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must be empty.

#### Response body
The successful response contains an instance of [Table](./tables_schemas.md/#table-object).

The error response contains an [Error](../response_codes.md).

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

Creates a table, returning the newly created table.

```apacheconfig
POST /v1/tables
```

#### Path parameters

The path parameters are not expected.

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must contain an instance of [Table](./tables_schemas/#table-object). The following fields will be used to create a table.

```typescript
{ 
  name: string;
  description: string
}
```

| Name | Type | Description |
| ------------- |------------- | -------------|
| name | `string` | The unique name of the table. |
| description | `string` | The description of the table. |

#### Response body
The successful response contains an instance of [Table](./tables_schemas/#table-object).

The error response contains an [Error](../response_codes.md).

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
    "description": "archive table",
    "dateCreated": "2020-06-18T00:50:09.323",
    "dateModified": "2020-06-18T00:50:09.323",
    "sizeInBytes": 0.00,
    "version": 2
}
```
---

## Update a table

Updates table parameters.

```apacheconfig
POST /v1/tables/{tableId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| tableId | `string` | The id of the table to update. |

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must contain an instance of [Table](./tables_schemas/#table-object). One or more of the following fields will be used to update the table.

```typescript
{ 
  name: string;
  description: string
}
```

| Name | Type | Description |
| ------------- |------------- | -------------|
| name | `string` | The unique name of the table. |
| description | `string` | The description of the table. |

#### Response body
The successful response contains an instance of [Table](./tables_schemas/#table-object).

The error response contains an [Error](../response_codes.md).

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

## Get columns of a table

Returns a column list of a table.

```apacheconfig
GET /v1/tables/{tableId}/columns
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| tableId | `string` | The id of a table to request columns from. |

#### Query parameters
The query parameters are not expected.

#### Request body

The request body must be empty.

#### Response body
The successful response contains an array of instances of [Column](./tables_schemas.md/#column-object).

The error response contains an [Error](../response_codes.md).

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

## Create a column

Creates a column in a table, returning the newly created column.

```apacheconfig
POST /v1/tables/{tableId}/columns/
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| tableId | `string` | The table id to of a table. |

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must contain an instance of [Column](./tables_schemas.md/#column-object). The following fields will be used to create a column.

```typescript
{ 
  name: string;
  dataType: TableColumnDataType;
  nullable: boolean;
  fieldLength: number;
  defaultValue: string | number | boolean
}
```

| Name | Type | Description |
| ------------- |------------- | -------------|
| name | `string` | REQUIRED. The unique name of the column. |
| dataType | `TableColumnDataType` |REQUIRED. [ColumnType](#table-column-type) . |
| nullable | `boolean` | OPTIONAL. Whether the column can accept null values, default is `true`. |
| fieldLength | `number` | OPTIONAL. Number of characters for 'FixedLengthText' dataType, default is `null` (which sets fixedLengthText to MAX). |
| nullable | `boolean` | OPTIONAL. Whether the column can accept `null` values, default is `true`. |
| defaultValue | `string`, `number`, `boolean` | OPTIONAL. The default value for the column, based on `dataType`. |

#### Response body
The successful response contains an instance of [Column](./tables_schemas.md/#column-object).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl "https://app.solvexia.com/api/v1/tables/mt-8239/columns" -X POST -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg" -H "Content-Type: application/json" -d '{ "name" : "col4","dataType": "number","defaultValue":5,"nullable":false}'
```

Response

```json
{ 
  "name": "col4",
  "dataType": "number",
  "defaultValue": 5,
  "fieldLength": null,
  "nullable": false
}
```
---

## Update a column

Updates table column parameters.

```apacheconfig
POST /v1/tables/{tableId}/columns/{columnName}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| tableId | `string` | The id of a table to update the column for. |
| ColumnName | `string` | The name of the column to update. You may indicate a column with spaces either by url-encoded spaces or '_' e.g. for `column space` it can be `column%20space` or `column_space`. |

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must contain an instance of [Column](./tables_schemas.md/#column-object). One or more of the following fields will be used to update the column.

```javascript
{ 
  name: string;
  dataType: TableColumnDataType;
  nullable: boolean;
  fieldLength: number;
  defaultValue: string | number | boolean
}
```

| Name | Type | Description |
| ------------- |------------- | -------------|
| name | `string` | The unique name of the column. |
| dataType | `TableColumnDataType` | [ColumnType](#table-column-type) . |
| nullable | `boolean` | Whether the column can accept null values, default is `true`. |
| fieldLength | `number` | Number of characters for 'FixedLengthText' dataType, default is `null` (which sets fixedLengthText to MAX). |
| nullable | `boolean` | Whether the column can accept `null` values, default is `true`. |
| defaultValue | `string`, `number`, `boolean` | The default value for the column, based on `dataType`. |

#### Response body
The successful response contains an instance of [Column](./tables_schemas.md/#column-object).

The error response contains an [Error](../response_codes.md).

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

Deletes a table column.

```apacheconfig
DELETE /v1/tables/{tableId}/columns/{columnName}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| tableId | `string` | The id of a table to delete the column from. |
| columnName | `string` | The name of the column to delete. You may indicate a column with spaces either by url-encoded spaces or '_' e.g. for `column space` it can be `column%20space` or `column_space`. |

#### Query parameters
The query parameters are not expected.

#### Request body

The request body must be empty.

#### Response body
The response body is empty.

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl "https://app.solvexia.com/api/v1/tables/mt-6239/columns/col1" -X DELETE -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

200 OK

---
