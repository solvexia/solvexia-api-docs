# File

| API Endpoints                           |
| --------------------------------------- |
| 1. [Get file metadata](#get-file-metadata) |
| 2. [Upload a file (by chunks)](#upload-a-file-(by-chunks)) |
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
    "url": "https://api.au.solvexia.com/v1/files/732/download",
    "fileState": 1
}
```

## Upload a file (by chunks)

Returns metadata information for a file.

### Step-1
Initiate an upload session for the file.

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

#### Error codes

| Error code | Description |
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
| sequenceHash | `string` | Represents the SHA-256 hash of the current chunk <br/> <ul><li>This will be used by API consumer to check the integrity of the chunk (valided for corruption), if he/she chooses to do so.</li></ul>  |

#### Error codes

| Error code | Description |
| ----------- | ----------- |
| 200 | A chunk was accepted. |
| 415, 500, 501 | A file type is not supporeted, abort the entire upload session. |
| Any other code | Try to upload a chunk again. |

#### Technically on server side:
- A chunk is saved to folder named {uploadId} in the temp folder
- Calculate the HASH of the saved chunk and compare against the supplied HASH; If they don’t match delete the chunk and return error code
- A chunk is retained there until `/v1/files/``{fileId}``/uploadByChunks/``{uploadId}``/commit` is called

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
    "url": "https://api.au.solvexia.com/v1/files/732/download",
    "fileState": 1
}
```

#### Error codes

| Error code | Description |
| ------------- |------------- |
| 200 | A chunk was accepted. |

#### Technically on server side:
- All the chunks in the folder {uploadId} are merged and created one big file
- Push that one file into database
- Upon successful push to databse, delete the folder {uploadId} including chunks and one big file and return success to user;
- Upon failure push to databse, delete the folder {uploadId} including chunks and one big file and return failure to user (with error code indicating the complete retry with new session)

#### Cleanup rules:
We would delete folders inside temp folder whose create date is older than 24 hour

## Download a file

Returns file byte array.

```apacheconfig
GET /v1/files/{fileId}/download
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
Successful response contains file byte array.

```json
{
}
```

## Update file metadata

Updates metadata information for a file.

```apacheconfig
POST /v1/files/{fileId}/
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
    "name": "Sales Q1 v2.xlsx",
    "sizeInBytes": 55741,
    "fileExtension": "xlsx",
    "url": "https://api.au.solvexia.com/v1/files/732/download",
    "fileState": 1
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
    "url": "https://api.au.solvexia.com/v1/files/734/download",
    "fileState": 1
}
```