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


