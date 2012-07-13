# WifiName API Documentation

## Authentication

You need to supply a ``token`` parameter for authentication. Contact [Developer Relations](mailto:dev.relations@radius-networks.com) to request a token.

## Pinned Contents

A *PinnedContent* is a piece of content that's been pinned to either an SSID
and MAC combination by a mobile device through the API, or just to an SSID by a
user on the web interface.

### Creating a Pinned Content

```
/api/v1/pinned_contents.json
```

You can create a pinned content by posting these attributes:

* ``pinned_content[mac]``: MAC of the device to pin to.
* ``pinned_content[ssid]``: SSID of the device to pin to.
* ``pinned_content[device_mac]``: MAC of the device that's doing the pinning.
* ``pinned_content[lat]``: Latitude of the phone. *optional*
* ``pinned_content[long]``: Longitude of the phone. *optional*
* ``pinned_content[content_type]``: Type of the content being pinned.
* ``pinned_content[content_value]``: Value of the content being pinned.
* ``pinned_content[content_title]``: Title.

#### Example

``` bash
$ curl -d "token=your_token" \
-d "pinned_content[mac]=123" \
-d "pinned_content[ssid]=A" \
-d "pinned_content[device_mac]=1" \
-d "pinned_content[content_type]=facebook_url" \
-d "pinned_content[content_value]=500" \
-d "pinned_content[content_title]=test" \
http://app.wifiname.com/api/v1/pinned_contents.json
```

``` json
{
   "content_type":"facebook_url",
   "content_value":"500",
   "content_title":"Test",
   "created_at":"2012-03-11T18:09:59Z",
   "device_mac":"1",
   "id":1,
   "lat":null,
   "long":null,
   "mac":"123",
   "ssid":"A",
   "updated_at":"2012-03-11T18:09:59Z",
   "user_id":null
}
```

### Send image

You can send a image in two formats: as remote url or base64 string.
Just create a PinnedContent with ``content_type``image`` and ``content_value`` with a valid url or base64 string

```
curl -i \
-H 'Accept: application/json' \
-H 'Content-Type: application/json' \
-X POST \
-d '{ "pinned_content": {"ssid": "your_ssid", "content_type": "image", "content_value": "string_of_image_in_base64_format"}, "token": "your_token" }' \
http://wifiname.com/api/v1/pinned_contents.json
```

### Retrieving Pinned Contents for SSIDs and MACs

```
/api/v1/pinned_contents/by_ssid_and_mac.json
```

You can retrieve Pinned Contents pinned by mobile devices to SSID & MAC
combinations, or by web interface users to SSIDs with these attributes:

* ``ssid_mac_pairs[][ssid]=A``: First SSID
* ``ssid_mac_pairs[][mac]=B``: First MAC
* ``ssid_mac_pairs[][ssid]=C``: Second SSID
* ``ssid_mac_pairs[][mac]=D``: Second MAC
* ``device_mac``: MAC of the device that's doing the request.

#### Example

``` bash
$ curl -X GET -d "token=your_token" \
-d "ssid_mac_pairs[][ssid]=A" \
-d "ssid_mac_pairs[][mac]=123" \
-d "device_mac=2" \
http://app.wifiname.com/api/v1/pinned_contents/by_ssid_and_mac.json
```

``` json
[
  {
    "content_type":"facebook_url",
    "content_value":"500",
    "content_title":"test",
    "created_at":"2012-03-11T18:09:59Z",
    "device_mac":"1",
    "id":1,
    "lat":null,
    "long":null,
    "mac":"123",
    "ssid":"A",
    "updated_at":"2012-03-11T18:09:59Z",
    "user_id":null
  },
  {
    "content_type":"facebook_url",
    "content_value":"500",
    "content_title":"test",
    "created_at":"2012-03-11T18:26:44Z",
    "device_mac":"1",
    "id":2,
    "lat":null,
    "long":null,
    "mac":"123",
    "ssid":"A",
    "updated_at":"2012-03-11T18:26:44Z",
    "user_id":null
  },
  {
    "content_type":"facebook_url",
    "content_value":"500",
    "content_title":"test",
    "created_at":"2012-03-11T18:26:44Z",
    "content_title":"test",
    "created_at":"2012-03-11T18:27:48Z",
    "device_mac":"1",
    "id":3,
    "lat":null,
    "long":null,
    "mac":"123",
    "ssid":"A",
    "updated_at":"2012-03-11T18:27:48Z",
    "user_id":null
  },
  {
    "content_type":"facebook_url",
    "content_value":"500",
    "content_title":"test",
    "created_at":"2012-03-11T18:26:44Z",
    "created_at":"2012-03-11T18:27:48Z",
    "device_mac":"1",
    "id":4,
    "lat":null,
    "long":null,
    "mac":"123",
    "ssid":"A",
    "updated_at":"2012-03-11T18:27:48Z",
    "user_id":null
  },
  {
    "content_type":"facebook_url",
    "content_value":"500",
    "content_title":"test",
    "created_at":"2012-03-11T18:26:44Z",
    "created_at":"2012-03-11T18:27:49Z",
    "device_mac":"1",
    "id":5,
    "lat":null,
    "long":null,
    "mac":"123",
    "ssid":"A",
    "updated_at":"2012-03-11T18:27:49Z",
    "user_id":null
  }
]
```

### Retrieving Pinned Contents for coordinates

```
/api/v1/pinned_contents/close_and_recent.json
```

You can retrieve the closest 20 pinned contents, plus the 20 most recent pins
from anywhere in the world with these attributes:

* ``lat``: Latitude of the requested position.
* ``long``: Latitude of the requested position.
* ``device_mac``: MAC of the device that's doing the request.

#### Example

``` bash
$ curl -X GET -d "token=your_token" \
-d "lat=40" \
-d "long=80" \
-d "device_mac=2" \
http://app.wifiname.com/api/v1/pinned_contents/close_and_recent.json
```

``` json
{
   "recent":[
      {
         "content_type":"url",
         "content_value":"http://www.web.de",
         "content_title":"test",
         "created_at":"2012-03-11T18:33:46Z",
         "device_mac":"1",
         "id":6,
         "lat":"40.0",
         "long":"80.0",
         "mac":"B",
         "ssid":"A",
         "updated_at":"2012-03-11T18:33:46Z",
         "user_id":null
      },
      {
         "content_type":"facebook_url",
         "content_value":"500",
         "content_title":"test",
         "created_at":"2012-03-11T18:27:49Z",
         "device_mac":"1",
         "id":5,
         "lat":null,
         "long":null,
         "mac":"123",
         "ssid":"A",
         "updated_at":"2012-03-11T18:27:49Z",
         "user_id":null
      },
      {
         "content_type":"facebook_url",
         "content_value":"500",
         "content_title":"test",
         "created_at":"2012-03-11T18:27:48Z",
         "device_mac":"1",
         "id":4,
         "lat":null,
         "long":null,
         "mac":"123",
         "ssid":"A",
         "updated_at":"2012-03-11T18:27:48Z",
         "user_id":null
      },
      {
         "content_type":"facebook_url",
         "content_value":"500",
         "content_title":"test",
         "created_at":"2012-03-11T18:27:48Z",
         "device_mac":"1",
         "id":3,
         "lat":null,
         "long":null,
         "mac":"123",
         "ssid":"A",
         "updated_at":"2012-03-11T18:27:48Z",
         "user_id":null
      },
      {
         "content_type":"facebook_url",
         "content_value":"500",
         "content_title":"test",
         "created_at":"2012-03-11T18:26:44Z",
         "device_mac":"1",
         "id":2,
         "lat":null,
         "long":null,
         "mac":"123",
         "ssid":"A",
         "updated_at":"2012-03-11T18:26:44Z",
         "user_id":null
      },
      {
         "content_type":"facebook_url",
         "content_value":"500",
         "content_title":"test",
         "created_at":"2012-03-11T18:09:59Z",
         "device_mac":"1",
         "id":1,
         "lat":null,
         "long":null,
         "mac":"123",
         "ssid":"A",
         "updated_at":"2012-03-11T18:09:59Z",
         "user_id":null
      }
   ],
   "closest":[
      {
         "content_type":"url",
         "content_value":"http://www.web.de",
         "content_title":"test",
         "created_at":"2012-03-11T18:33:46Z",
         "device_mac":"1",
         "id":6,
         "lat":"40.0",
         "long":"80.0",
         "mac":"B",
         "ssid":"A",
         "updated_at":"2012-03-11T18:33:46Z",
         "user_id":null
      }
   ]
}
```

## Pin Targets

A *PinTarget* is an SSID & MAC combination that content has been pinned to.

### Retrieve Pin Targets

```
/api/v1/pin_targets.json
```

You can retrieve the 10 closest SSID and MAC combinations of the devices content has been
pinned to with these attributes:

* ``lat``: Latitude of the requested position.
* ``long``: Latitude of the requested position.
* ``device_mac``: MAC of the device that's doing the request.

#### Example

``` bash
$ curl -X GET -d "token=your_token" \
-d "lat=40" \
-d "long=80" \
-d "device_mac=2" \
http://app.wifiname.com/api/v1/pin_targets.json
```

``` json
[
  {
    "ssid":"A",
    "mac":"B"
  }
]
```

