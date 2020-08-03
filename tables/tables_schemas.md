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
  ; sizeInBytes: decimal
  ; dateCreated: string
  ; dateModified: string
  ; version: int
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
  Decimal = "decimal",
  Money = "money"
}
```
