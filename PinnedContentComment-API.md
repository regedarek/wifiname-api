## Overview

The PinnedContentComment API allows mobile apps to comment PinnedContents

A successful request will return a hash with the comment`s attributes, including
comment, comment id, parent_id, pinned_content_id, user_id, created_at and updated_at timestamps

## PinnedContentCommentAPI Endpoint

<table>
  <thead>
    <tr>
      <th>Endpoint</th>
      <th>Required User</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>POST /api/v1/pinned_content_comments</td>
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
-d '{ "pinned_content_comment": { "comment": "Yea Bob Marley man!" }, "pinned_content_id": "13", "token":"authtoken" }' \   
http://0.0.0.0:3000/api/v1/pinned_content_comments.json

```
## Create new comment

``POST api/v1/pinned_content_comments.json``

#### Paramaters

```json
{
  "pinned_content_comment": {
    "comment": "Yea Bob Marley man!",
    "pinned_content_id": "13"
  },

  "token":"authtoken"
}
```

## Comment on another comment

``POST api/v1/pinned_content_comments.json``

#### Paramaters

```json
{
  "pinned_content_comment": {
    "comment": "You are right!",
    "pinned_content_id": "81",
    "parrent_id": "1"
  },

  "token":"authtoken"
}

```
#### Successful Request
```
HTTP/1.1 201 Created 
Location: http://0.0.0.0:3000/api/v1/pinned_content_comments/5
Content-Type: application/json; charset=utf-8
X-Ua-Compatible: IE=Edge
Etag: "267cee6a7f975b71aba4808f35dbc3b0"
Cache-Control: max-age=0, private, must-revalidate
X-Request-Id: 2b5744e57dd33b674c507e044ca93fb5
X-Runtime: 0.107588
Content-Length: 150
Server: WEBrick/1.3.1 (Ruby/1.9.2/2012-04-20)
Date: Fri, 06 Jul 2012 17:48:40 GMT
Connection: Keep-Alive
```

```json
{
    "comment": "Yea Bob Marley man!",
    "created_at": "2012-07-06T13:26:02Z",
    "id": 1,
    "parent_id": null,
    "pinned_content_id": 13,
    "updated_at": "2012-07-06T13:26:02Z",
    "user_id": 45
}
```

#### Unsuccessful Request
```
HTTP/1.1 422 Unprocessable Entity
Content-Type: application/json; charset=utf-8
X-Ua-Compatible: IE=Edge
Cache-Control: no-cache
X-Request-Id: 5a31d28e4d534ddbdedf160b4eff7a84
X-Runtime: 0.119927
Content-Length: 41
Server: WEBrick/1.3.1 (Ruby/1.9.2/2012-04-20)
Date: Fri, 06 Jul 2012 17:49:33 GMT
Connection: Keep-Alive
```

```json
{
  "errors": {
    "comment":[
      "can't be blank"
    ]
  }
}

or

{
  "error": 
    "Token is invalid."
} 
```
