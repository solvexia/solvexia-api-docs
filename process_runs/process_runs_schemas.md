# Process runs schemas

1. [Process Run](#process-run)
2. [Process Run Request Type](#process-run-request-type)
3. [Process Run Status](#process-run-status)
4. [Data Step Property](#data-step-property)

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

## Data Step Property

### Data Step Property Object
```typescript
interface DataStepProperty {
  id: Pointer
  name : string
  dataType: DataStepPropertyDataType
  required: boolean
  visible: boolean
  informationFlowType: DataStepPropertyInformationFlowType
  mouseoverText: string
}
```

### Checkbox Data Step Property
```typescript
interface CheckboxDataStepProperty extends DataStepProperty {
  value: boolean
}
```

### Dropdown Data Step Property
```typescript
interface DropdownDataStepProperty extends DataStepProperty {
  value: string
  options: string[]
}
```

### Text Data Step Property
```typescript
interface TextDataStepProperty extends DataStepProperty {
  value: string
  foregroundColor: string
}
```

### String Data Step Property
```typescript
interface StringDataStepProperty extends DataStepProperty {
  value: string
}
```

### Number Data Step Property
```typescript
interface NumberDataStepProperty extends DataStepProperty {
  value: number
}
```

### Decimal Data Step Property
```typescript
interface DecimalDataStepProperty extends DataStepProperty {
  value: number
  decimalPoint: number
}
```

### System Variable Data Step Property
```typescript
interface SystemVariableDataStepProperty extends DataStepProperty {
  value: SystemVariableType
}
```

### DatePicker Data Step Property
```typescript
interface DatePickerDataStepProperty extends DataStepProperty {
  value: string
}
```

### File Data Step Property
```typescript
interface FileDataStepProperty extends DataStepProperty {
  File: Pointer
}
```

### System Variable Type
```typescript
enum SysVarVariableType {
  USERNAME = "USERNAME",
  USER_ID = "USER_ID",
  PROCESS_ID = "PROCESS_ID",
  PROCESS_NAME = "PROCESS_NAME",
  CURRENT_DATE_TIME = "CURRENT_DATE_TIME"
}
```

### Data Step Property Information Flow Type
```typescript
enum DataStepPropertyInformationFlowType {
  INPUT = "INPUT",
  OUTPUT = "OUTPUT",
  NONE = "NONE"
}
```

### Data Step Property Data Type
```typescript
enum DataStepPropertyDataType {
  Dropdown = "Dropdown",
  Text = "Text",
  String = "String",
  Number = "Number",
  Decimal = "Decimal",
  CheckBox = "CheckBox",
  SystemVariable = "SystemVariable",
  Datepicker = "Datepicker",
  File = "File"
}
```