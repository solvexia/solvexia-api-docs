# Table Schemas

[Table](#table)  
[Column](#column)  

# Table Types
[Table Column Type](#table-column-type)  

---
## Table

```typescript
interface Table {
    id: string
  ; name : string
  ; description: string
  ; sizeInBytes: number
  ; dateCreated: string
  ; dateModified: string
  ; version: number
}
```

## Column

```typescript
interface TableColumn {
    name: string
  ; dataType: TableColumnDataType
  ; nullable: boolean
  ; fieldLength: number
  ; defaultValue: string | boolean | number
}
```
---

## Table Column Type
```typescript
enum TableColumnDataType {
  Number = "number",
  FixedLengthText = "fixedLengthText",
  TrueFalse = "trueFalse",
  Datetime = "datetime",
  Money = "money"
}
```
