# File APIs
[Get file metadata](#get-file-metadata)  
[Update file metadata](#Update-file-metadata)  
[Upload a file](#upload-a-file)  
[Download a file](#Download-a-file)  
[Start Upload Chunks Session](#start-upload-chunk-session)  
[Upload Chunk](#upload-chunk)  
[Commit Upload Chunk Session](#commit-upload-session)  

---

## Get file metadata

Returns metadata information for a file.

```apacheconfig
GET /v1/files/{fileId}/metadata
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
Successful response contains an instance of a [File](./file_schemas.md/#file-object).

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
| fileId | `string` | The file id to request. |

#### Query parameters
Query parameters are not expected.

#### Request body
Request body must contain a [File](./file_schemas.md/#file-object) json.
Only the 'name' field may be changed.

```json
{
    "name": "Sales Q1 v2 changed.xlsx"
}
```

#### Response body
Successful response contains a [File](./file_schemas.md/#file-object) json.

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

Upload file as a form data using streaming.

```apacheconfig
POST /v1/files/{fileId}
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
Successful response contains [File](./file_schemas.md/#file-object) json.

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
Query parameters are not expected.

#### Request body
Request body must be empty.

#### Response body
Successful response contains file byte array.

### Example

Request

```shell
curl 'https://app.solvexia.com/api/v1/files/f-2238' -x GET --header 'Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg'
```

Response

---


## Start Upload Chunk Session

Start an upload chunk session for a file

```apacheconfig
POST /v1/files/{fileId}/uploadsessions
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| fileId | `string` | The file id to upload. |

#### Query parameters
Query parameters are not expected.

#### Request body
Request body must must be empty


#### Response body
Successful response contains a [Upload Session](./file_schemas.md/#upload-session-object) Json.

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

## Upload Chunk

Upload chunk of a file to the upload session for a file

```apacheconfig
POST /v1/files/{fileId}/uploadsessions/{uploadSessionId}/chunks/{chunkid}
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| fileId | `string` | The file id to upload. |
| uploadSessionId | `string` | The upload session id to upload too. |
| chunkid | `string` | The chunk id to upload too, it is the sequential number of the chunk |

#### Query parameters
Query parameters are not expected.

#### Request body
Request body must contain form data


#### Response body
Successful response contains a [Chunk](./file_schemas.md/#chunk-object) Json.

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

## Commit Upload Session

Finish the upload of file chunks

```apacheconfig
POST /v1/files/{fileId}/uploadsessions/{uploadSessionId}/commit
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| fileId | `string` | The file id to upload. |
| uploadSessionId | `string` | The upload session id to upload too. |

#### Query parameters
Query parameters are not expected.

#### Request body
Request body must be empty


#### Response body
Successful response contains [File](./file_schemas.md/#file-object) json.

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