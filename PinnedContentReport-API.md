## Overview

The PinnedContentReport API allows mobile apps to report an offensive PinnedContent.

A successful request will return a hash with the report`s attributes, including
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
      <td>POST /api/v1/pinned_content_reports</td>
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
-d '{ "pinned_content_report": { "reason": "You can`t insult Bob Marley", "pinned_content_id": "13" }, "token":"authtoken" }' \
http://0.0.0.0:3000/api/v1/pinned_content_reports.json
```
## Report PinnedContent

``POST api/v1/pinned_content_reports.json``

#### Paramaters

```json
{
  "pinned_content_report": {
    "reason": "You can`t insult Bob Marley",
    "pinned_content_id": "13"
  },

  "token":"authtoken"
}
```

#### Successful Request
```
HTTP/1.1 201 Created 
Location: http://0.0.0.0:3000/api/v1/pinned_content_reports/3
Content-Type: application/json; charset=utf-8
X-Ua-Compatible: IE=Edge
Etag: "88ac346f6093f3a01e3307ab6e163000"
Cache-Control: max-age=0, private, must-revalidate
X-Request-Id: b5f7573796d79851b633cde99a575bb4
X-Runtime: 4.730938
Content-Length: 155
Server: WEBrick/1.3.1 (Ruby/1.9.2/2012-04-20)
Date: Fri, 06 Jul 2012 18:13:08 GMT
Connection: Keep-Alive
```

```json
{
  "created_at":"2012-07-06T18:13:08Z",
  "id":3,"pinned_content_id":63,
  "reason":"You can`t insult Bob Marley",
  "updated_at":"2012-07-06T18:13:08Z",
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
    "reason":["You must provide a reason."],
    "pinned_content_id":["can't be blank"]
  }
}

or

{
  "error": 
    "Token is invalid."
} 
```
