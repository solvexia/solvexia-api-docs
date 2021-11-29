# Process schemas

[User List Item](#user-list-item)  
[User](#user)  
[Permission](#permission)  
[Permission Role Type](#permission-role-type)

## User List Item

```typescript
type UserListItem = {
    id: string
  ; name: string
}
```

## User

```typescript
type User = {
    id: string
  ; firstName: string
  ; lastName: string
  ; loginName: string
  ; email: string
  ; accountActive: boolean
  ; city: string
  ; country: string
  ; dateOfBirth: string
  ; lastSignInDate: string
  ; phoneNumberLand: string
  ; phoneNumberMobile: string
  ; timeZoneHasDaylightSavings: boolean
  ; timezone: string
  ; userRole: string
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
  Owner = "owner",
  Editor = "editor",
  Executor = "executor",
  Reader = "reader"
}
```