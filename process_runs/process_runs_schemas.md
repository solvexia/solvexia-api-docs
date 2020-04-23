# Process runs schemas

1. [Process Run](#process-run)
2. [Process Run Request Type](#process-run-request-type)
3. [Process Run Status](#process-run-status)

## Process Run

```typescript
type ProcessRun = {
  id: string
  name: string
  process: string
  description: string
  lastModifiedBy: string
  dateModified: string
  dateCreated: string
  alertEmailAddress: string
  alertSMS: string
  runButtonName: string
}
```

## Process Run Request Type

```typescript
enum ProcessRunRequestType {
  startRun = "startRun",
  cancelRun = "cancelRun"
}
```

## Process Run Status

#### Process Run Status Object
```typescript
type ProcessRunStatus = {
  id: string
  dateFinished: string
  dateStarted: string
  runDurationInSec: number
  status: ProcessRunStatusType
}
```

#### Process Run Status Type
```typescript
enum ProcessRunStatusType {
  "NotStarted" = 1,
  "Scheduled" = 2,
  "Running" = 3,
  "Finished" = 4,
  "Cancelled" = 5,
  "TimedOut" = 6
}
```

#### Process Step Status Type
```typescript
enum ProcessStepStatusType {
  "NotStarted" = 1,
  "Running" = 2,
  "Success" = 3,
  "Warning" = 4,
  "Failed" = 5,
  "Scheduled" = 6,
  "Cancelled" = 7,
  "Skipped" = 8
}
```