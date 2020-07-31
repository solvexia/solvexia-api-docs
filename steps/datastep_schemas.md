# Data Step Schema
[Data Step](#data-step)   

# Data Step Property Schemas

[Data Step Property](#data-step-property)  
[Checkbox Data Step Property](#checkbox-data-step-property)  
[Dropdown Data Step Property](#dropdown-data-step-property)  
[Text Data Step Property](#text-data-step-property)  
[String Data Step Property](#string-data-step-property)  
[Number Data Step Property](#number-data-step-property)  
[Decimal Data Step Property](#decimal-data-step-property)  
[System Variable Data Step Property](#system-variable-data-step-property)  
[DatePicker Data Step Property](#datepicker-data-step-property)  
[File Data Step Property](#file-data-step-property)  

# Property Field Types
[System Variable Type](#system-variable-type)  
[Data Step Property Information Flow Type](#data-step-property-information-flow-type)  
[Data Step Property Data Type](#data-step-property-data-type)  

---

## Data Step

```typescript
type DataStep {
    id: string
  ; name: string
  ; isEnabled: boolean
  ; orderedName: string
}
```
---

## Data Step Property

### Data Step Property
```typescript
interface DataStepProperty {
    id: string
  ; name: string
  ; dataType: DataStepPropertyDataType
  ; required: boolean
  ; visible: boolean
  ; informationFlowType: DataStepPropertyInformationFlowType
  ; mouseoverText: string
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
  ; options: string[]
}
```

### Text Data Step Property
```typescript
interface TextDataStepProperty extends DataStepProperty {
    value: string
  ; foregroundColor: string
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
  ; decimalPoints: number
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
  File: string
}
```

---

### System Variable Type
```typescript
enum SysVarVariableType {
  USERNAME = "USERNAME",
  USER_ID = "USER_ID",
  USER_EMAIL = "USER_EMAIL",
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
