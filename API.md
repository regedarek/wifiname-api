
## Authentication

You need to supply a ``token`` parameter for authentication. Contact [Anton Zolotov](mailto:anton@zolotov.eu) to request a token.

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

#### Example

```
$ curl -d "token=your_token" -d "pinned_content[mac]=123" -d "pinned_content[ssid]=A" -d "pinned_content[device_mac]=1" -d "pinned_content[content_type]=facebook_url" -d "pinned_content[content_value]=500" http://wifiname.herokuapp.com/api/v1/pinned_contents.json
```

```
{"content_type":"facebook_url","content_value":"500","created_at":"2012-03-11T18:09:59Z","device_mac":"1","id":1,"lat":null,"long":null,"mac":"123","ssid":"A","updated_at":"2012-03-11T18:09:59Z","user_id":null}
```

### Retrieving Pinned Contents for SSIDs and MACs



### Retrieving Pinned Contents for coordinates

```
/api/v1/pinned_contents/close_and_recent.json
```

You can retrieve the closest 20 pinned contents, plus the 20 most recent pins
from anywhere in the world by posting these attributes:

* ``lat``: Latitude of the requested position.
* ``long``: Latitude of the requested position.
* ``device_mac``: MAC of the device that's doing the pinning.

## Pin Targets

A *PinTarget* is an SSID & MAC combination that content has been pinned to.

### Retrieve Pin Targets

```
/api/v1/pin_targets.json
```

You can retrieve the 10 closest SSID and MAC combinations of the devices content has been
pinned to by posting these attributes:

* ``lat``: Latitude of the requested position.
* ``long``: Latitude of the requested position.
* ``device_mac``: MAC of the device that's doing the pinning.

#### Example

```
$ curl -X GET -d "token=your_token" \
-d "lat=40" -d "pinned_content[device_mac]=1" \
-d "long=80" \
-d "device_mac=2" \
http://wifiname.herokuapp.com/api/v1/pin_targets.json
```

```
[{"ssid":"A","mac":"B"}]
```

