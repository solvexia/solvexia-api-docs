# Process schemas

[User Group List Item](#user-group-list-item)  
[User Group](#user-group)  
[Permission](#permission)  

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
## Permission

### Permission

```typescript
type Permission = {
    resourceId: string
  ; resourceName: string
  ; role: PermissionRoleType
}
```

### Permission Role Type

```typescript
enum PermissionRoleType {
  Owner = "Owner",
  Editor = "Editor",
  Executor = "Executor",
  Reader = "Reader"
}
```