---
title: Service Discovery
permalink: /Service_Discovery/
---

`This spec has been frozen and finalized, but the documentation will continue to be updated for clarity. Join the `[`Mailing` `List`](http://lists.open311.org/groups/discuss)` for updates.`

### About

This is the specification for the service discovery mechanism which is required for Open311 GeoReport v2 and subsequent Open311 APIs.

The service discovery mechanism is intended serve several functions:

1.  Establish a single universal URL for a jurisdiction that can route to various different API endpoints including multiple versions of the Open311 APIs and multiple levels of API stability (eg. production and testing)
2.  Provide an aggregated look-up to flag whether there have been any significant changes to the data held within each API. This is done with the changeset field and can imply different things for different APIs. In the case of the Open311 GeoReport v2 specification, an updated changeset indicates that there has been an update to the Service Discovery list or to the Service Definitions. This is basically a flag to indicated whether clients should refresh frequently cached data.
3.  Provide key meta data about each API endpoint including the output formats supported (eg. whether JSON is supported).
4.  Establish a single universal URL for information about API services such as getting an API key, contacting the API maintainers, and checking on the status of the API (eg under maintenance)

This service discovery specification is meant to be read-only and can be provided either dynamically or using a manually edited static file.

### Base URL

The base URL for Service Discovery is meant to supercede the base URL for the Open311 endpoint. This service discovery could potentially be used for other APIs other than the Open311 API, so the endpoint for Service Discovery could be located somewhere entirely different than the Open311 endpoint.

Provider endpoints **must** specify a url that will likely not change. This url **must** end in /discovery.<format>

Format **must be** both:

-   xml
-   json

While it's not required, it's recommended that an HTML version of this file be made available too. This can be done automatically from the XML using an XSL style sheet. To make it easier for people to discover your endpoints, you may wish to make the HTML transformation of your discovery file the default page served by the webserver when someone browses to the root of your endpoints. In otherwords, an HTML version of the discovery file could be served for the discovery endpoint without requiring discovery.xml at the end of the URL. You may also wish to offer this at the endpoint for the root of your Open311 GeoReport v2 URLs since currently nothing is served there. A sample XSL transform can be seen on this [demonstration discovery file](http://sandbox.georeport.org/tools/discovery/discovery.xml) which uses this [XSL stylesheet](http://sandbox.georeport.org/tools/discovery/transform.xsl).

### Formats

The discovery file must be provided as both XML and JSON. The JSON structure is meant to follow a programmatic mapping based on the XML structure using the [Spark Convention](http://wiki.open311.org/JSON_and_XML_Conversion#The_Spark_Convention). This means that if you have an XML file, you can easily generate the JSON version with XSL. This can be done using a server side XSLT ([php example](http://sandbox.georeport.org/tools/sparkjson/xml2json_spark_php.txt)) which is also available as a generic tool if you want to simply copy and paste the generated JSON: <http://sandbox.georeport.org/tools/sparkjson/>

### Fields for All Versions

All fields are required.

-   **changeset** - *String* - Sortable field that specifies the last time this document was updated.
-   **contact** - *String* - Human readable information on how to get more information on this provider.
-   **key_service** - *String* - Human readable information on how to get an API key.
-   **endpoints** - *Array* - Data structure holding the endpoints supported by this provider
-   **endpoints.endpoint** - *Hash* - Data structure holding the metadata for each endpoint supported by this provider
-   **endpoints.endpoint.specification** - *String* - The token of the service specification that is supported. This token will be defined by each spec. In general the format is a URL that identifies the specification and version number much like an XMLNS declaration. (eg <http://wiki.open311.org/GeoReport_v2>)
-   **endpoints.endpoint.url** - *String* - URL of the endpoint provider
-   **endpoints.endpoint.changeset** - *String* - Sortable field that specifies the last time this document was updated.
-   **endpoints.endpoint.type** - *String* - Either "production" or "test" defines whether the information is live and will be acted upon.
-   **endpoints.endpoint.formats** - *Array* - Data structure of supported MIME types.
-   **endpoints.endpoint.formats.format** - *String* - Supported MIME type for this endpoint.

### Examples

<tabs> <tab title="XML">

    <?xml version="1.0" encoding="UTF-8"?>
    <discovery>
        <changeset>2011-02-03 14:18</changeset>
        <contact>You can email or call for assistance api@mycity.org +1 (555) 555-5555</contact>
        <key_service>You can request a key here: http://api.mycity.gov/api_key/request</key_service>
        <endpoints>
            <endpoint>
                <specification>http://wiki.open311.org/GeoReport_v2</specification>
                <url>http://open311.mycity.gov/v2</url>
                <changeset>2010-11-23 09:01</changeset>
                <type>production</type>
                <formats>
                    <format>text/xml</format>
                </formats>
            </endpoint>
            <endpoint>
                <specification>http://wiki.open311.org/GeoReport_v2</specification>
                <url>http://open311.mycity.gov/test/v2</url>
                <changeset>2010-10-02 09:01</changeset>
                <type>test</type>
                <formats>
                    <format>text/xml</format>
                    <format>application/json</format>
                </formats>
            </endpoint>
            <endpoint>
                <specification>http://wiki.open311.org/GeoReport_v3</specification>
                <url>http://open311.mycity.gov/v3</url>
                <changeset>2011-02-03 14:18</changeset>
                <type>test</type>
                <formats>
                    <format>text/xml</format>
                    <format>application/json</format>
                </formats>
            </endpoint>
        </endpoints>
    </discovery>

</tab> <tab title="JSON">

    {
      "changeset":"2011-02-03 14:18",
      "contact":"You can email or call for assistance api@mycity.org +1 (555) 555-5555",
      "key_service":"You can request a key here: http://api.mycity.gov/api_key/request",
      "endpoints":[
        {
          "specification":"http://wiki.open311.org/GeoReport_v2",
          "url":"http://open311.mycity.gov/v2",
          "changeset":"2010-11-23 09:01",
          "type":"production",
          "formats":[
            "text/xml"
          ]
        },
        {
          "specification":"http://wiki.open311.org/GeoReport_v2",
          "url":"http://open311.mycity.gov/test/v2",
          "changeset":"2010-10-02 09:01",
          "type":"test",
          "formats":[
            "text/xml",
            "application/json"
          ]
        },
        {
          "specification":"http://wiki.open311.org/GeoReport_v3",
          "url":"http://open311.mycity.gov/v3",
          "changeset":"2011-02-03 14:18",
          "type":"test",
          "formats":[
            "text/xml",
            "application/json"
          ]
        }
      ]
    }

</tab> </tabs>
