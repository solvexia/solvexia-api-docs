# User schemas

[User List Item](#user-list-item)  
[User](#user)  

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