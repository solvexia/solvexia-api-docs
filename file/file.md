# File

| API Endpoints                           |
| --------------------------------------- |
| 1. [Get file metadata](#get-file-metadata) |
| 2. [Upload a file](#upload-a-file) |
| 3. [Download a file](#Download-a-file) |
| 4. [Update file metadata](#Update-file-metadata) |

## Get file metadata

Returns metadata information for a file.

```apacheconfig
GET /v1/files/{fileId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| fileId | `string` | The file id to request. |

#### Query parameters
Query parameters are not expected.

#### Request body
Request body must be empty.

#### Response body
Successful response contains an instance of a [File](./file_schemas.md).

```json
{
    "id": "f-732",
    "name": "Sales Q1.xlsx",
    "sizeInBytes": 55741,
    "fileExtension": "xlsx",
    "url": "https://app.solvexia.com/api/v1/files/732/download",
    "fileState": 1
}
```

## Upload a file

Upload file as a form data using streaming.

```apacheconfig
POST /v1/files/{fileId}/upload
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| fileId | `string` | The file id to upload. |

#### Query parameters
Query parameters are not expected.

#### Request body
Request body must contain form data.

#### Response body
Successful response contains an instance of a [File](./file_schemas.md) Object.

## Download a file

Returns file byte array.

```apacheconfig
GET /v1/files/{fileId}/download
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| fileId | `string` | The id of the file requested to download. |

#### Query parameters
Query parameters are not expected.

#### Request body
Request body must be empty.

#### Response body
Successful response contains file byte array.


## Update file metadata

Updates metadata information for a file.

```apacheconfig
POST /v1/files/{fileId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| fileId | `string` | The file id to request. |

#### Query parameters
Query parameters are not expected.

#### Request body
Request body must contain an instance of a [File](./file_schemas.md) Object.

```json
{
    "id": "f-732",
    "name": "Sales Q1 v2.xlsx"
}
```

#### Response body
Successful response contains an instance of a [File](./file_schemas.md) Object.

```json
{
    "id": "f-734",
    "name": "Sales Q1 v2.xlsx",
    "sizeInBytes": 74382,
    "fileExtension": "xlsx",
    "url": "https://app.solvexia.com/api/v1/files/734/download"
}
```