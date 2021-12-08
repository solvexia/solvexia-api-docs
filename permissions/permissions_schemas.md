## Permission schemas

[Permission](#permission)  
[Permission Role Type](#permission-role-type)

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
  Owner = "owner",
  Editor = "editor",
  Executor = "executor",
  Reader = "reader"
}
```