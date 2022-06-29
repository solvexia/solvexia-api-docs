## Permission schemas

[Permission](#permission)  
[Permission Role](#permission-role)

### Permission

```typescript
type Permission = {
    resourceId: string
  ; resourceName: string
  ; role: PermissionRole
}
```

### Permission Role

```typescript
enum PermissionRole {
  Owner = "owner",
  Editor = "editor",
  Executor = "executor",
  Reader = "reader"
}
```