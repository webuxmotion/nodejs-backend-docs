---
id: api_user
title: USER
sidebar_label: USER
---

Welcome to API

## /api/auth/register
Method:
```
POST
```

Body
```
{
    "email": "example10@gmail.com",
    "password": "123456"
}
```
**Headers:**

Content-Type:
```
application/json
```
Authorization:
```
Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImV4YW1wbGUyQGdtYWlsLmNvbSIsInVzZXJJZCI6IjVkMjczNDMzNGQwOWExMDU2YWVhNDFiMyIsImlhdCI6MTU2Mjg1MDUxOSwiZXhwIjoxNTYyODU0MTE5fQ.A0STDjlX4DQJ_0Gd0x49gqNpcwZymadX8aBA5FyAy2A
```

**Responses**
1. When user not authorized or token is expired. (**401 Unauthorized**)
```
Unauthorized
```
2. When dublicated email. (**409 Conflict**)
```
{
    "message": "This email already used"
}
```
3. When user was registered. (**201 Created**)
```
{
    "_id": "5d29195e8bf868055f7fdc27",
    "email": "myemail@gmail.com",
    "password": "$2a$10$tp1Elw1HMwbOUPm7YtfqlOI.CSsgRYyZbDvtMGeyQd1G6X2W7R90m",
    "__v": 0
}
```

## /api/auth/login

Method:
```
POST
```

Body
```
{
    "email": "example10@gmail.com",
    "password": "123456"
}
```
**Headers:**

Content-Type:
```
application/json
```

**Responses**
1. When user not found. (**404 Not Found**)
```
{
    "message": "User not found"
}
```
2. When password dont match. (**401 Unauthorized**)
```
{
    "message": "This email already used"
}
```
3. When user was logined. (**200 OK**)
```
{
    "token": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im15ZW1haWxAZ21haWwuY29tIiwidXNlcklkIjoiNWQyOTE5NWU4YmY4NjgwNTVmN2ZkYzI3IiwiaWF0IjoxNTYyOTc0ODEzLCJleHAiOjE1NjI5Nzg0MTN9.PkKZ0XqvUgL_-nU3lI-UXtUE4fba65vMH8e54oX1W04"
}
```