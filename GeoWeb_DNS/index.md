---
title: GeoWeb DNS
permalink: /GeoWeb_DNS/
---

GeoWebDNS is a service inspired by DNS and reverse-geocoding. Given a lat/long, what is the URI of the standardized API, protocol, or file for a given service namespace (eg 311 services). The GeoWebDNS servers would be decentralized and redundant, automatically mirroring one-another and propagating out changes much like DNS servers. All that the client would need to do would be to send the lat/long and request the URI for a given namespace. The server would then have to look at the polygon that contains that lat/long for that service namespace and return the URI associated with it.

This model is meant to work in concert with a [Service Discovery](/Service_Discovery "wikilink") spec such as that being used with Open311. A good deal of other work is also occurring in the service discovery space for [data catalogs](http://spec.datacatalogs.org/) and [APIs](http://www.apievangelist.com/2013/02/02/one-api-discovery-definition-to-rule-them-all/).

Reference Implementation
------------------------

-   <https://github.com/open311/geowebdns>
-   See also <https://github.com/SeeClickFix/open311-router>

Protocol
--------

The service will use HTTP. It exists at one URL; in this document we will use the example `http://ns.geowebdns.org/service` as the API endpoint.

A query uses query string arguments:

`lat`: The latitude. (WGS84)

`long`: The longitude. (WGS84)

**Note**: should lat/long be one value? This makes it easier to add new query types. It might be like: `point=100.1234%2035.1234` (i.e., space-separated), or just comma-separated (which doesn't need to be quoted).

`type`: The *type* of object to be returned; this will be a string/URI. This argument may be present multiple times, returning jurisdictions with any of the given types.

A query then looks like:

    GET /service?lat=100.1234&long=35.1234&type=http://ns.geowebdns.org/311/jurisdiction

The *only* coordinate system supported is [WGS 84](http://en.wikipedia.org/wiki/WGS84) (latitude/longitude).

In this example `http://ns.geowebdns.org/311/jurisdiction` might be the URI identifying 311 jurisdictions. URIs act similar to how an [XML namespace](http://en.wikipedia.org/wiki/Xmlns) works; it is an opaque string, but by convention maps to a URL describing the type.

**Note**: should we accept a level of confidence, using the same scale as presented [in the Google geocode API](http://code.google.com/apis/maps/documentation/geocoding/#GeocodingAccuracy)? A low confidence might mean we do a more fuzzy search.

The response is a JSON object like:

    Content-type: application/json

    {"results": [
        {"type": "http://ns.geowebdns.org/311/jursidiction",
         "uri": "http://sfgov.org/311/api",
         "name": "San Francisco 311",
         "kml": "http://ns.geowebdns.org/kml/3940193"
        }
        ]
    }

The return result JSON is an object with one key, `"results"` (other keys may be added later, for example to specifying caching semantics or paging). The `"results"` key has a value of a list of all results matching this location.

Each result is an object with several keys:

`"type"`: The "type" of the jurisdiction. If you specify multiple `type=...` in your query, you can use this to determine which specific type this result is.

`"uri"`: The destination URL.

**Note**: should there be a kind of "id URL" in addition to this more explicit URL? For instance, if there are multiple APIs, they might each have a different "type" but still represent the same basic entity. These could all have the same id URI (e.g., `http://sfgov/311`) but still different specific endpoints.

`"name"`: The name of the entity, a readable string.

**Note**: should this be translated or translatable? E.g., `{"en_US": "San Francisco 311 Information", "es": "San Fransisco 311 Informacion"}` ?

`"kml"`: This *optional* response value points to a KML document describing the entity.

**Note**: would it make sense to inline [GeoJSON](http://geojson.org/)?

No results
----------

If there are absolutely no results, it will return `{"results": []}` with a 404 status code.

Errors
------

If the request is malformed, a 400 Bad Request response is given. The text of this response will be a readable description of the problem.

The readable format is defined by the Content-Type header, but will probably be HTML. Clients that cannot or do not want to present HTML can strip all tags and will get a description that is still readable.

**Note**: are there any predictable errors? E.g., a lat/long that is impossible?

Source
------

Source code for the reference implementation is at <https://github.com/openplans/geowebdns>

To get started, run:

`    $ wget `[`https://github.com/openplans/geowebdns`](https://github.com/openplans/geowebdns)
`    $ chmod +x setup-layout.sh`
`    $ ./setup-layout.sh geowebdns-app`

This product uses [SilverLining](http://cloudsilverlining.org/) for deployment. The stack consists of PostGIS, GeoAlchemy, WebOb.

To bootstrap a database, you can run these scripts:

`   $ cd src/geowebdns/imports`
`   $ mkdir data`
`   $ ./getall.sh`
`   $ export CONFIG_PG_SQLALCHEMY=postgres://postgres:password@localhost/geowebdns  # use your postgres password here`
`   $ ./importall.sh --commit`

Related Technologies
--------------------

-   [LoST: A Location-to-Service Translation Protocol](http://tools.ietf.org/html/rfc5222)
