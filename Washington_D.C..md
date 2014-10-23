---
title: Washington_D.C.
permalink: /Washington_D.C./
---

*This was taken from the Notes from Cities portion of the [Open311 DevCamp Etherpad](http://etherpad.com/wCotZZ0OCE)*

### General Description

Ran apps for democracy contest in Spring 09, ideas was not just to provide data, but provide read/write API. Crowdsoource data collection for service requests. Hard to provide a stable API, and migrated from Hanson CRM to Motorolla CRM and migration is still wrapping up. Have existing version of API, would like to rewrite it so that anyone can use it and make it more aware of other cities. Service area: with same app could identify teh city to send request to. Interested in real-time technologies, eg PuSH. Explanation of Backend: discussions about blackbox of receiving SR. Communications system... Not actually work order system, small cities often integrate into call center, run by public works, etc. Also on backend, has data catalog, which can provide real-time data and can get

### Open 311 API

Approach
--------

Distinct characteristics of DC Open 311 API are following:

1.  Metadata services to provide list of types of requests handled by 311 and definition of those services
2.  Structured service request data - new service requests must be entered in structured way (not just single text blob)
3.  Asynchronous submission - on submission of new ticket, API returns temporary token, that will be exchanged to service request ID once backend processing is done (usually done in minutes)
4.  Anonymous submission - tickets can be entered anonymously, but customer information can be provided for additional tracking by users.

Overall Architecture
--------------------

[<File:DC_Open_311_Architecture.png>](/File:DC_Open_311_Architecture.png "wikilink")

API Documentation
-----------------

[DC's Open 311 API v2](http://octolabs.pbworks.com/Open-311-API-v2-Documentation)
