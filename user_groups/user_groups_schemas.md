# User Group schemas

[User Group List Item](#user-group-list-item)  
[User Group](#user-group) <br />
[Member](#member) 

## User Group List Item

```typescript
type UserGroupListItem = {
    id: string
  ; name: string
}
```

## User Group

```typescript
type UserGroup = {
    id: string
  ; name: string
  ; description: string
}
```

## Member

```typescript
type Member = {
    id: string
  ; loginName: string
}
```