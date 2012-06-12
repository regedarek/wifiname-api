## Overview

The registration API allows mobile apps to:

1. Create user accounts

2. Sign users in

A successful authentication request will return a hash with the user's
account information, including the token to authenticate further API
requests on behalf of the user.

**Important!** Previously, there was one token per app that was used to
authenticate all API requests. Since we now have user accounts, that
auth token should only be used to for the API calls described on this
page. When a user is registered or signed in successfully, the response
contains an ``authentication_token``. That token should be used to
authenticate API requests on behalf of the user, so we can track what
they do.

## API Endpoints and Required Users

<table>
  <thead>
    <tr>
      <th>Endpoint</th>
      <th>Required User</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>GET /pin_targets</td>
      <td>ApiUser or User</td>
    </tr>
    <tr>
      <td>POST /pinned_contents</td>
      <td>User</td>
    </tr>
    <tr>
      <td>GET /pinned_contents/by_ssid_and_mac</td>
      <td>ApiUser or User</td>
    </tr>
    <tr>
      <td>GET /pinned_contents/close_and_recent</td>
      <td>ApiUser or User</td>
    </tr>
    <tr>
      <td>POST /users</td>
      <td>ApiUser</td>
    </tr>
    <tr>
      <td>POST /users/sign_in</td>
      <td>ApiUser</td>
    </tr>
    <tr>
      <td>POST /users/sign_out</td>
      <td>ApiUser</td>
    </tr>
    <tr>
      <td>PUT /users/:token</td>
      <td>User</td>
    </tr>
  </tbody>
</table>

### Headers

Set ``Content-Type`` and ``Accept`` to ``application/json``.

### Sending parameters

Send parameters as a JSON object, not urlencoded.

**Example with curl:**

```bash
curl -i \
-H 'Accept: application/json' \
-H 'Content-Type: application/json' \
-X POST \
-d '{ "user": { "email": "anton@zolotov.eu", "username": "azolotov", "password": "testtest", "password_confirmation": "testtest" }, "token":"zUF7uZxxe8LiisF6s958" }' \
https://app.wifiname.com/api/v1/users.json
```

## Register a new user

``POST /api/v1/users.json``

#### Paramaters

```json
{
  "user": {
    "email": "test@test.com",
    "username": "test",
    "first_name": "Bob",
    "last_name": "Marley",
    "password": "testtest",
    "password_confirmation": "testtest"
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

## Log In an Existing User

You can log in a user either with a a username and password or an email
and password.

```
POST /api/v1/users/sign_in.json
```

#### Parameters
```json
{
  "user":{
    "username":"test",
    "password":"testtest"
  },
  "token":"authtoken"
}
```

or

```json
{
  "user":{
    "email":"test@test.com",
    "password":"testtest"
  },
  "token":"authtoken"
}
```

#### Successful Request

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
X-UA-Compatible: IE=Edge
Etag: "6b8099347fa80fd910f7545a30897171"
Cache-Control: max-age=0, private, must-revalidate
Set-Cookie: _wifiname_session=BAh7B0kiD3Nlc3Npb25faWQGOgZFRkkiJTBjNTc5ZjNhZTRlNTRmNGY4MWYzM2ExYTUzYTY1MTM0BjsAVEkiIHdhcmRlbi51c2VyLm1vYmlsZV91c2VyLmtleQY7AFRbCEkiD01vYmlsZVVzZXIGOwBGWwZpC0kiIiQyYSQxMCQvQjZDcFZuZk5aMFJucmYvb0NkNi5PBjsAVA%3D%3D--6f077baf0d1425ecc28b6e3076f6c50c945ccba2; path=/; HttpOnly
X-Request-Id: 6b1ab0d717d77ffb4139c455b7c23539
X-Runtime: 0.099220
Connection: close
```

```json
{
  "success":true,
  "auth_token":"bwSnTTkYGrVJvpuuvLPq",
  "username":"test",
  "email":"test@test.com"
}
```

#### Unsuccessful Request

```
HTTP/1.1 401 Unauthorized
```

```json
{
  "success":false,
  "message":"Error with your login or password"
}
```

## Sign Out

You must sign out to reset the user's token.

```
DELETE /api/v1/users/sign_out.json
```

#### Parameters
```json
{
  "user":{
    "username":"test",
  },
  "token":"authtoken"
}
```

#### Successful Request
```
HTTP/1.1 200 OK
```

```json
{
  "success":true,
  "message":"Signed out successfully!"
}
```

## Update User

```
PUT /api/v1/users/:token.json
```

where ``:token`` is the user's authentication token.

#### Parameters
```json
{
  "user":{
    "username":"test",
  },
  "token":"authtoken"
}
```

#### Successful Request
```
HTTP/1.1 200 OK
```

```json
{
  "success":true,
  "auth_token":"bwSnTTkYGrVJvpuuvLPq",
  "username":"test",
  "email":"test@test.com"
}
```
