# Process runs schemas

1. [Process Run](#process-run)

## Process Run

```typescript
type Process = {
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