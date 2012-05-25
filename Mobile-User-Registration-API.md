## Register a new user

``POST /api/v1/mobile_users.json``

#### Paramaters

```json
{
  "mobile_user": {
    "email": "test@test.com",
    "username": "test",
    "password": "testtest",
    "password_conformation": "testtest"
  },

  "token":"authtoken"
}
```

#### Successful Request
```
HTTP/1.1 201 Created`
```

```json
{
  "authentication_token":"bwSnTTkYGrVJvpuuvLPq",
  "email":"test@test.com",
  "username":"test"
}
```

#### Unsuccessful Request
```
HTTP/1.1 422 Unprocessable Entity
```

```json
{
  "email":[
    "has already been taken"
  ],
  "password":[
    "can't be blank",
    "doesn't match confirmation"
  ],
  "username":[
    "can't be blank"
  ]
}
```