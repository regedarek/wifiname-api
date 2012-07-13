## Overview

The Pin2Owner API allows mobile apps to pin content to SSID.

A successful request will return a hash with the Pin2Owner report`s attributes, including
reason, report id, pinned_content_id, user_id(id of user who wants to report PinnedContent),
 created_at and updated_at timestamps

## PinnedContentReport API Endpoint

<table>
  <thead>
    <tr>
      <th>Endpoint</th>
      <th>Required User</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>POST /api/v1/pin2_owners</td>
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
-d '{ "pin2_owner": { "ssid": "reggaeClub", "message":"test message" }, "token":"auth_token" }' \
http://app.wifiname.dev/api/v1/pin2_owners.json
```
## Report PinnedContent

``POST api/v1/pin2_owners.json``

#### Paramaters

```json
{
  "pin2owner": {
    "ssid": "bob_marley",
    "message": "Positive Vibrations!"
  },

  "token":"authtoken"
}
```

#### Successful Request
```
HTTP/1.1 201 Created 
Location: http://0.0.0.0:3000/api/v1/pin2_owners/10
Content-Type: application/json; charset=utf-8
X-Ua-Compatible: IE=Edge
Etag: "4390cc5e7e5250712107c5d9af81ba7f"
Cache-Control: max-age=0, private, must-revalidate
X-Request-Id: eea54d444201a64eef5fe297b7e3510f
X-Runtime: 10.165925
Content-Length: 153
Server: WEBrick/1.3.1 (Ruby/1.9.2/2012-04-20)
Date: Fri, 13 Jul 2012 10:28:13 GMT
Connection: Keep-Alive
```

```json
{
  "created_at":"2012-07-13T10:28:10Z",
  "id":10,
  "message":"test message",
  "ssid":"bob_marley",
  "updated_at":"2012-07-13T10:28:10Z",
  "user_id":45
} 
```

#### Unsuccessful Request
```
HTTP/1.1 422  
Content-Type: application/json; charset=utf-8
X-Ua-Compatible: IE=Edge
Cache-Control: no-cache
X-Request-Id: 128982a6cf0f191dd667909773dd3189
X-Runtime: 0.045160
Content-Length: 91
Server: WEBrick/1.3.1 (Ruby/1.9.2/2012-04-20)
Date: Fri, 06 Jul 2012 18:20:58 GMT
Connection: Keep-Alive
```

```json
{
  "errors": {
    "ssid":["can't be blank"],
    "message":["can't be blank"]
  }
}

or

{
  "error": 
    "Token is invalid."
} 
```
