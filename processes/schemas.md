# Processes schemas

1. [Process List Item](#process-list-item)
2. [Process](#process)
3. [Created Process Run](#created-process-run)
4. [Process Run List Item](#process-run-list-item)

## Process List Item

```typescript
type ProcessListItem = {
    id: string
    name: string
}
```

## Process

```typescript
type Process = {
  id: string
  name: string
  description: string
  lastModifiedBy: string
  dateModified: string
  dateCreated: string
  alertEmailAddress: string
  alertSMS: string
  availableToSubscriber: boolean
  runsAvailableToSubscriber: boolean
}
```

## Created Process Run

```typescript
type ProcessRun = {
    id: string
}
```

## Process Run List Item

```typescript
type ProcessRunListItem = {
    id: string
    name: string
}