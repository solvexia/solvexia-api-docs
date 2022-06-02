# User schemas

[User List Item](#user-list-item)  
[User](#user)  
[Account Status](#account-status)

## User List Item

```typescript
type User = {
    id: string
  ; loginName: string
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
  ; accountStatus: string
  ; city: string
  ; country: string
  ; department: string
  ; dateOfBirth: string
  ; lastSignInDate: string
  ; phoneNumberLand: string
  ; phoneNumberMobile: string
  ; timezone: string
  ; userRole: string
}
```

## Account Status
```typescript
enum AccountStatus = {
    "Active": "Active"
  ; "Suspended": "Suspended"
  ; "Locked": "Locked"
}
```