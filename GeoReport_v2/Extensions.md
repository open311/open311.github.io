---
title: GeoReport v2 Extensions
permalink: /GeoReport_v2/Extensions/
---
This page is meant to document all extensions to the [GeoReport v2 specification](../) that have been implemented in the wild. Open311 endpoints that implement these extensions are expected to fully support the GeoReport v2 standard, but additionally incorporate these as-of-yet non-standard extensions to the specification. By documenting where these extensions have been implemented and how they've fared in real world use we can be better informed about incorporating them into a future version of the specification. 

As with all pages on the wiki, this page is editable. See the contributor guidelines for information on making edits or feel free to chime in on the mailing list. 


Pagination
------

[Issue #16](https://github.com/open311/open311.github.io/issues/16)

The GeoReport v2 spec didn't specify any consistent way to control the size of the response payload for service requests, it simply defined a default, "Default query limit is a span of 90 days or first 1000 requests returned, whichever is smallest." and left all other filtering up to additional query parameters. Very quickly users and implementers felt the need for paramenters to define the size of the response and to page through it using the `page` and `page_size` paramenters. Currently, this appears to be the most widely and consistently implemented extension to the GeoReport v2 specification. 

### Implementing Endpoints

- Chicago
- Boston
- Toronto
- Bloomington
- San Francisco


Media Handling
------

[Issue #9](https://github.com/open311/open311.github.io/issues/9)

The GeoReport v2 spec punted on defining how to submit media (such as an image file from a smartphone) as part of the service request. Instead, it simply defined a field (`media_url`) for referencing a public URL for a media file. This left it up to the client to implement the transactions for receiving the file and posting it to that public URL. Over time, many GeoReport implementors have expressed interest in incorporating this directly into the API specification and a few have demonstrated this in production.

A central question of how this is implemented is whether it is done as part of the same payload as the service request itself or if it's decoupled asynchronously as a separate request that's then linked with the service request. If the media is uploaded as part of the request it would have to be base64 encoded to work using `application/x-www-form-urlencoded` otherwise uploading in binary with `multipart/form-data` would break backward compatibility with the existing specification.

`--- explanation of implementation(s) should go here ---`

### Implementing Endpoints

- Helsinki
- Bloomington


Comment Handling
------

[Issue #10](https://github.com/open311/open311.github.io/issues/10)

Editing & Updating Requests
------

[Issue #11](https://github.com/open311/open311.github.io/issues/11)

Extended Attributes
------

[Issue #35](https://github.com/open311/open311.github.io/issues/35)

While the current specification states, "it is recommended that you adhere to the specification strictly and do not include foreign tags or namespaces" many have extended their implementations with additional fields or whole new response objects as part of the GET service request response. In most cases, the default response will not include these extended attributes, but the `extensions` query parameter can be used to return them, e.g. `&extensions=true`

Here's an example of a request response with extended attributes:

~~~
[
  {
    "service_request_id": "4944710",
    "status": "open",
    "service_name": "Street or Sidewalk Cleaning",
    "service_code": "518d5892601827e3880000c5",
    "description": "Garbage on sidewalk",
    "requested_datetime": "2015-07-27T16:24:28-07:00",
    "updated_datetime": "2015-07-27T16:24:28-07:00",
    "address": "Intersection of Mcallister St & Van Ness Ave",
    "lat": 37.7797,
    "long": -122.42,
    "media_url": "http://mobile311.sfgov.org/media/san_francisco/report/photos/55b6bda3df86c6d37f6d33a4/photo_20150727_162341.jpg",
    "attributes": [
      {
        "label": "Object",
        "name": "request_type",
        "value": "Other Loose Garbage / Debris",
        "code": "Other_loose_garbage_debris_yard_waste"
      }
    ],
    "extended_attributes": {
      "channel": "android",
      "x": 6006819.576650221,
      "y": 2112060.1528775054,
      "photos": [
        {
          "media_url": "http://mobile311.sfgov.org/media/san_francisco/report/photos/55b6bda3df86c6d37f6d33a4/photo_20150727_162341.jpg",
          "title": "Submitted",
          "width": 864,
          "height": 1536,
          "orientation": "portrait",
          "created_at": "2015-07-27T16:24:25-07:00"
        }
      ]
    },
    "notes": [
      {
        "datetime": "2015-07-27T16:24:19-07:00",
        "description": "Submitted via Android",
        "type": "submitted"
      },
      {
        "datetime": "2015-07-27T16:24:28-07:00",
        "description": "Opened",
        "type": "opened"
      }
    ]
  }
]
~~~

### Implementing Endpoints

- Chicago
- Boston
- San Francisco


