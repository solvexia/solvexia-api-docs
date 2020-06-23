# Process schemas

[Process List Item](#process-list-item)  
[Process](#process)  

## Process List Item

```typescript
type ProcessListItem = {
    id: string
  ; name: string
}
```

## Process

```typescript
type Process = {
    id: string
  ; name: string
  ; description: string
  ; lastModifiedBy: string
  ; dateModified: string
  ; dateCreated: string
  ; alertEmailAddress: string
  ; alertSMS: string
  ; availableToSubscriber: boolean
  ; runsAvailableToSubscriber: boolean
}
```
