# File APIs
[Get file metadata](#get-file-metadata)  
[Update file metadata](#Update-file-metadata)  
[Upload a file](#upload-a-file)  
[Download a file](#Download-a-file)  
[Start upload chunks session](#start-upload-chunk-session)  
[Upload chunk](#upload-chunk)  
[Commit upload chunk session](#commit-upload-session)  

---

## Get file metadata

Returns metadata information for a file.

```apacheconfig
GET /v1/files/{fileId}/metadata
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| fileId | `string` | The file id to request metadata for. |

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must be empty.

#### Response body
The successful response contains an instance of a [File](./file_schemas.md/#file).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl "https://app.solvexia.com/api/v1/files/f-45678/metadata" -X GET -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
{
    "id": "f-732",
    "name": "Sales Q1.xlsx",
    "sizeInBytes": 55741,
    "fileExtension": "xlsx",
    "url": "https://app.solvexia.com/api/v1/files/f-732"
}
```
---

## Update file metadata

Updates metadata information for a file.

```apacheconfig
POST /v1/files/{fileId}/metadata
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| fileId | `string` | The id of the file to update metadata for. |

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must contain an instance of [File](./file_schemas.md/#file). Note that only the `name` field may be changed.

```json
{
    "name": "Sales Q1 v2 changed.xlsx"
}
```

#### Response body
The successful response contains an instance of a [File](./file_schemas.md/#file).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl "https://app.solvexia.com/api/v1/files/f-45678/metadata" -X POST -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg" -H "Content-Type: application/json" -d '{"name":"Sales Q1 v2 changed.xlsx"}'
```

Response

```json
{
    "id": "f-45678",
    "name": "Sales Q1 v2 changed.xlsx",
    "sizeInBytes": 74382,
    "fileExtension": "xlsx",
    "url": "https://app.solvexia.com/api/v1/files/f-45678"
}
```
---

## Upload a file

Uploads file as a form data using streaming.

```apacheconfig
POST /v1/files/{fileId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| fileId | `string` | The file id to upload. |

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must contain form data.


#### Response body
The successful response contains an instance of a [File](./file_schemas.md/#file).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl --location --request POST 'https://app.solvexia.com/api/v1/files/f-2238' \
--header 'Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg' \
--form 'file=@/C:/uploadfile.xlsx'
```

Response

```json
{
    "id": "f-45678",
    "name": "uploadfile.xlsx",
    "sizeInBytes": 74382,
    "fileExtension": "xlsx",
    "url": "https://app.solvexia.com/api/v1/files/f-45678"
}
```
---

## Download a file

Downloads a file.

```apacheconfig
GET /v1/files/{fileId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| fileId | `string` | The id of the file requested to download. |

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must be empty.

#### Response body
The successful response contains file byte array.

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl 'https://app.solvexia.com/api/v1/files/f-2238' -x GET --header 'Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg'--output "./123.txt"
```

Response

---


## Start upload chunk session

Starts an upload chunk session for a file.

```apacheconfig
POST /v1/files/{fileId}/uploadsessions
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| fileId | `string` | The file id to upload. |

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must must be empty.


#### Response body
The successful response contains an instance of [Upload Session](./file_schemas.md/#upload-session).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl 'https://app.solvexia.com/api/v1/files/f-2238/uploadsessions' -x POST --header 'Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg'
```

Response

```json
{
    "uploadSessionId": "2a27a605-d05f-4199-bae0-8da44cd24f70"
}
```
---

## Upload chunk

Uploads a chunk of a file to the upload session for a file.

```apacheconfig
POST /v1/files/{fileId}/uploadsessions/{uploadSessionId}/chunks/{chunkId}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| fileId | `string` | The file id to upload. |
| uploadSessionId | `string` | The upload session id to upload too. |
| chunkId | `string` | The chunk id to upload too, it is the sequential number of the chunk. |

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must contain form data.


#### Response body
The successful response contains an instance of [Chunk](./file_schemas.md/#chunk).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl 'https://app.solvexia.com/api/v1/files/f-2238/uploadsessions/2a27a605-d05f-4199-bae0-8da44cd24f70/chunks/1' -x POST --header 'Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg' --form 'file=@/C:/1'
```

Response

```json
{
    "fileId": "f-2238",
    "uploadSessionId": "2a27a605-d05f-4199-bae0-8da44cd24f70",
    "chunkId": 1,
    "chunkHash": "봨촿麊掂쬴ʅ꺟꼰믐컫蹸쯇삑"
}
```
---

## Commit upload session

Finishes the upload session for a file.

```apacheconfig
POST /v1/files/{fileId}/uploadsessions/{uploadSessionId}/commit
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| fileId | `string` | The file id to finish upload session for. |
| uploadSessionId | `string` | The upload session id to finish. |

#### Query parameters
The query parameters are not expected.

#### Request body
The request body must be empty.


#### Response body
The successful response contains an instance of a [File](./file_schemas.md/#file).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl 'https://app.solvexia.com/api/v1/files/f-2238/uploadsessions/2a27a605-d05f-4199-bae0-8da44cd24f70/commit' -x POST --header 'Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg'
```

Response

```json
{
    "id": "f-2238",
    "name": "uploadfile.xlsx",
    "sizeInBytes": 74382,
    "fileExtension": "xlsx",
    "url": "https://app.solvexia.com/api/v1/files/f-2238"
}
```
---
