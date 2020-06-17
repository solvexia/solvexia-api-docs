# Process runs schemas

[Process Run](#process-run)  
[Process Run Request ](#process-run-request)  
[Process Run Status](#process-run-status)  

# Process runs Types
[Process Run Request Type](#process-run-request-type)
[Process Run Status Type](#process-run-status-type)

---

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
## Process Run Request

```typescript
type ProcessRunRequest = {
  request: ProcessRunRequestType
  processRunId: string
}
```

## Process Run Status
```typescript
type ProcessRunStatus = {
  id: string
  dateStarted: string
  dateFinished: string
  runDurationInSeconds: number
  status: ProcessRunStatus
}
```
---

## Process Run Request Type

```typescript
enum ProcessRunRequestType {
  startRun = "ProcessRun_StartRq",
  cancelRun = "ProcessRun_CancelRq"
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