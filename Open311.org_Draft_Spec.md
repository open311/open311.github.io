---
title: Open311.org Draft Spec
permalink: /Open311.org_Draft_Spec/
---

Abstract
--------

The Open311 API provides a way to work with service requests between citizens, governments and non-governmental organizations.

Open311 is decentralized. There is no central registry to which a providing system is required to register. There is also no central authority that lists the responsible Open311 providers for a particular location or set of concerns.

Open311 is intended to be applicable every where for all languages. The spec has been initially written in English with English terms solely for the convenience of the authors. All attempts were made to provide for the API to work for all language locales.

Open311 uses only standard HTTP requests and responses.

The Open311 API is a RESTful service. All GET requests are idempotent, they have no side effect other then returning data in a response to the client.

It is expected that multiple versions of the Open311 API will exist and interoperate concurrently. The spec is designed to allow service providers of different versions to be able to communicate together.

Case Studies
------------

-   [San Francisco API draft](http://apps.sfgov.org/Open311API/)
-   [Washington DC API v2 draft](http://octolabs.pbworks.com/Open-311-API-v2-Documentation)
-   [SeeClickFix API draft](http://docs.google.com/View?id=dc8k3dxw_45gcnhm4dp)

Terminology
-----------

### Provider or Service Provider

The system on which the API calls are made. This is the system that is mapped to by the URIs that a client makes HTTP calls to.

### Client

The entity or system from which API calls are made. This could be a citizen's browser, a third party computer system or another service provider.

### Issue

A specific, geographically stationary, concern that has a concrete definable fix. Some common names include: service request, work order or ticket.

### Citizen

Any natural person.

### Non-Governmental Organization

An entity that is not a government.

### Government

The organization that manages a political unit of any size.

### Latitude / Longitude

All latitudes and longitude values MUST be WGS84 (World Geodetic System 1984) datum values expressed in decimal format. See <http://en.wikipedia.org/wiki/WGS84>

`   Example: 37.40320,-121.977521`

Schema
------

You can use syntax highlighting to help display a schema, eg JSON. See the [Help:Editing](/Help:Editing "wikilink") for more information. Content pulled from working doc: <http://etherpad.com/Gg1kfcXQR3>

**Service Request**

    -id (alpha-numeric)
    -status ("submitted", "incomplete", "rejected", "open", "assigned", "closed","more info", "in progress")
    -location (location type)
    -data feed URL (atom feed subscription)
    -List of:
      -who (string)
      -activity date (date timestamp)
      -description (text blob)

**Location**

    -jurisdiction returns acceptable location schema (lat/lng, human readable address, internal ID)
    -location {
            lat/lng: GS84 (or what ever is the standard)
            human readable location (String blob?)
            3rd party addressing scheme (defined in meta data returned by jurisdiction)
        }


**Linking service requests** ( serial/parallel ? )

    -id { [id:status] }

Location Schema

System Architecture
-------------------

Please note that this illustrates a proposal and does not represent the current API specs being implemented in Washington D.C. or San Francisco.

1.  Service request (SR) data and location are entered from open311 app. App requests SR jurisdiction API URI from [GeoWeb DNS](/GeoWeb_DNS "wikilink") (if not already cached).
2.  The jurisdiction API URI is returned (eg <http://api.nyc.gov/311>). If no URI is found, default to an adhoc SR service (an equivalent of FixMyStreet or SeeClickFix)
3.  A generic SR (core schema) is sent to the jurisdiction API
4.  If successful, check if the app and jurisdiction supports extensions for additional details. If so, additional details for the identified SR type are requested (sr_type.get)
5.  Additional details are sent to the jurisdiction by any app and any person (not necessarily the original reporter) at a later date.

[Image:311-flowchart.png](/Image:311-flowchart.png "wikilink")
