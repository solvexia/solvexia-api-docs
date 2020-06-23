# File Schemas

[File](#file)  
[Upload Session](#upload-session)  

[File Chunk](#file-chunk)  

## File

```typescript
type File = {
  id: Pointer
  name: string
  sizeInBytes: number
  fileExtension: string
  url: string
}
```

## Upload Session
```typescript
type UploadSession = {
  uploadSessionId: string
}
```

## File Chunk
```typescript
type FileChunk = {
  fileId: string
  uploadSessionId: string
  chunkId: number
  chunkHash: string
}
```