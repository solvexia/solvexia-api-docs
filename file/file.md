# File

| API Endpoints                           |
| --------------------------------------- |
| 1. [Get file metadata](#get-file-metadata) |
| 2. [Upload a file by chunks](#upload-a-file-by-chunks) |
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

## Upload a file by chunks

Upload metadata information for a file.

### Step-1
Initiate an upload session for a file.

```apacheconfig
POST /v1/files/{fileId}/uploadByChunks
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| fileId | `string` | The file id to upload. |

#### Query parameters
Query parameters are not expected.

#### Request body
Request body must be empty.

#### Response body
Successful response contains an id of a current upload session for the file.

```json
{
    "uploadId": "dc05dffe-fb22-424b-8f8c-9f765964434e"
}
```

#### Response codes

| Response code | Description |
| ------------- |------------- |
| 200 | Upload session initiation was successful |

#### Technically on server side:
A unique folder named same as {uploadId} created in the temp folder.

### Step-2
Upload chunks in a session.

```apacheconfig
POST /v1/files/{fileId}/uploadByChunks/{uploadId}

MIME Type: multipart/form-data
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| fileId | `string` | The file id to upload. |
| uploadId | `string` | The id of a current upload session. |

#### Query parameters
| Name | Type | Description |
| ------------- |------------- | -------------|
| sequenceId | `integer` | Represents the chunk number: <br/> <ul><li>It starts from one(1)</li><li>This will be used to detect the order when about to merge all chunks into one file.</li></ul> |

#### Request body
Request body must contain a file chunk (byte array).

#### Response body
Successful response is as follow.

```json
{
    "fileId": "f-2434",
    "uploadId": "dc05dffe-fb22-424b-8f8c-9f765964434e",
    "sequenceId": 1324,
    "sequenceHash": ""
}
```

| Name | Type | Description |
| ------------- |------------- | -------------|
| fileId | `string` | The file id to upload. |
| uploadId | `string` | The id of a current upload session. |
| sequenceId | `integer` | Represents the chunk number: <br/> <ul><li>It starts from one(1)</li><li> This will be used to detect the order when about to merge all chunks into one file.</li></ul> |
| sequenceHash | `string` | Represents the SHA-256 hash of the current chunk <br/> <ul><li>You can use it to check the integrity of the chunk (validated for corruption).</li></ul>  |

#### Response codes

| Response code | Description |
| ----------- | ----------- |
| 200 | A chunk was accepted. |
| 415, 500, 501 | A file type is not supporeted, abort the entire upload session. |
| Any other code | Try to upload a chunk again. |

### Step-3
Complete the upload.

```apacheconfig
POST /v1/files/{fileId}/uploadByChunks/{uploadId}/commit
```

#### Path parameters

| Name | Type | Description |
| ------------- |------------- | -------------|
| fileId | `string` | The file id to upload. |
| uploadId | `string` | The id of a current upload session. |

#### Query parameters
Query parameters are not expected.

#### Request body
Request body must be empty.

#### Response body
Successful response contains an instance of a [File](./file_schemas.md) Object.

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

#### Response codes

| Response code | Description |
| ------------- |------------- |
| 200 | A chunk was accepted. |

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

```json
{
}
```

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
    "url": "https://app.solvexia.com/api/v1/files/734/download",
    "fileState": 1
}
```