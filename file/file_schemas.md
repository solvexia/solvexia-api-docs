# File Schemas

[File Object](#file-object)  
[Upload Session object](#upload-session-object)  
[Chunk object](#chunk-object)  
---

## File Object

```typescript
type File = {
  id: Pointer
  name: string
  sizeInBytes: number
  fileExtension: string
  url: string
}
```

## Upload Session object
```typescript
type UploadSession = {
  uploadsessionid: string
}
```

## Chunk object
```typescript
type UploadSession = {
  fileId: string
  uploadsessionid: string
  chunkId: number
  chunkHash: string
}
```