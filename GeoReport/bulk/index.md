---
title: GeoReport Bulk Data Specification
permalink: /GeoReport/bulk
---

The GeoReport Bulk data specification allows developers, researchers, and others to download issues which have been reported to government entities like cities for resolution. These interactions are often referred to as "service requests" or "calls for service" and have traditionally been handled by custom web forms or phone based call centers (sometimes using the 311 phone number or other short-code). The current specification is focused on location-based non-emergency issues such as graffiti, potholes, and street cleaning. It is designed to allow access to larger numbers of records (more than 1,000) that are impractical for a typical [GeoReport_V2 API](/GeoReport_v2/) implementation to provide.

Many governments make service request data available in bulk form even if they do not offer a GeoReport API, however they do so in a highly inconsisent manner. For more information on how this specification was initially developed, see [Untangling 311 Request Data](http://govex.jhu.edu/untangling-311-request-data/). A [mapping of more than 25 existing bulk data sources to the proposed specification](https://docs.google.com/spreadsheets/d/1N9TSt6anpSJkZQv5ZhwtH4r4UX_QegerC4IRnzhkrzI/edit#gid=1781540284) is also available.

Status
------

### Specification

<span style="color:red;font-weight:bold">Proposed</span>: The GeoReport Bulk Spec has been researched and proposed, but no publishers have yet implemented it.

### Servers

None at present; several U.S. cities are working to implement, including: 

[Louisville, KY](https://twitter.com/edblayney/status/736228693220204544)
Raleigh, NC


Internationalization and Encoding
---------------------------------

### Date/time format

All date/time fields must be formatted in a common subset of ISO 8601 as per the [w3 note](http://www.w3.org/TR/NOTE-datetime). Timezone information (either Z meaning UTC, or an HH:MM offset from UTC) **must** be included.

Examples:

-   1994-11-05T08:15:30-05:00 corresponds to November 5, 1994, 8:15:30 am, US Eastern Standard Time.
-   1994-11-05T13:15:30Z corresponds to the same instant.

### Encoding

UTF-8 is required for all text responses, except when a [DataPackage](http://specs.frictionlessdata.io/data-packages/) via an archive is provided.

All text provided by the server, whether in CSV, XML, JSON, or any other text-based content-type, MUST be encoded as UTF-8. Appropriate HTTP headers must be set, and the root element must be preceded with the XML declaration including the encoding="UTF-8" attribute. All text received by the service from the client will be assumed to be UTF-8 and must be decoded accordingly. Examples of the HTTP content-type headers for each format are shown below under Format Support.

Format Support
--------------

The GeoReport Bulk data format is intended to be format-independent, though the most likely formats are those which include column/element identifiers such as CSV, JSON, and XML.

The HTTP content-type headers should be matched to the format in which the bulk data is to be transferred:

**CSV:** Content-Type: text/csv; charset=utf-8

**XML:** Content-Type: text/xml; charset=utf-8

**JSON:** Content-Type: application/json; charset=utf-8

### CSV Support

CSV for the data should be Content-Type: text/csv. The CSV output must be compatible with [RFC4180](https://tools.ietf.org/html/rfc4180). Column headers MUST be included.

### XML Support

XML for the data should be Content-Type: text/xml. The XML output currently defined is schemaless and without a namespace declaration. For now, extending the output with additional namespaces should be done at your own risk. To guarantee that all clients can support the XML output, it is recommended that you adhere to the specification strictly and do not include foreign tags or namespaces. It is also assumed that the default namespace is not specified, but if it must be specified, the XMLNS URI is the URL of the specification: <http://wiki.open311.org/GeoReport_Bulk_v1>

### JSON Support

JSON for the data should be Content-Type: application/json. JSON support is based on a programmatic mapping of the XML format using the [Spark Convention](http://wiki.open311.org/JSON_and_XML_Conversion#The_Spark_Convention). This means that if you have an XML file, you can easily generate the JSON version with XSL. This can be done using a server side XSLT ([php example](http://sandbox.georeport.org/tools/sparkjson/xml2json_spark_php.txt)).

Data Output
-----------

#### Fields

{: .table .table-bordered .table-striped .response-table}
| Field Name | Data Type | Value Format | Optional | In GeoReport_V2 | Description |
|--------------------|-----------|------------------------------------------|----------|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| service_request_id | Text |  | No | Yes | The unique ID of the service request created. Ideally this ID should be the same as in the source system, though a surrogate key can be substituted. |
| requested_datetime | DateTime | See [Date/Time Format](#datetime-format) | No | Yes | The date and time when the service request was made. |
| updated_datetime | DateTime | See [Date/Time Format](#datetime-format) | No | Yes | The date and time when the service request was last modified. For requests with status=closed, this will be the date the request was closed. |
| closed_date | DateTime | See [Date/Time Format](#datetime-format) | Yes | No | Date and time the request record was closed or cancelled. This field should be empty/null until the service request has been closed. |
| status_description | Text |  | No | Partial | A single-word indicator of the current state of the service request; typically 'Open', 'Processing', 'Hold', or 'Closed' but terms may vary by system. (Note: [GeoReport V2](/GeoReport_v2/) only permits 'open' and 'closed') |
| status_notes | Text |  | No | Yes | Explanation of why status was changed to current state or more details on current status than conveyed with status alone. |
| source | Text |  | Yes | No | Mechanism or path by which the service request was received; typically 'Phone', 'Text/SMS', 'Website', 'Mobile App', 'Twitter', etc but terms may vary by system. |
| service_name | Text |  | No | Yes | The human readable name of the service request type |
| service_subtype | Text |  | Yes | No | The human readable name of the service request subtype |
| description | Text |  | Yes | Yes | A full description of the request or report submitted. |
| agency_responsible | Text |  | Yes | Yes | The agency responsible for fulfilling or otherwise addressing the service request. |
| address | Text |  | No | Yes | Human readable address or description of location. This should be provided from most specific to most general geographic unit, separated by commas, e.g. address number or cross streets, street name, neighborhood/district, city/town/village, county, postal code. |
| lat | Number | Decimal Degrees (D.D˚) | No | Yes | Latitude of the location, using the WGS84 projection. |
| long | Number | Decimal Degrees (D.D˚) | No | Yes | Longitude of the location, using the WGS84 projection. |

#### Example Outputs

{: .nav .nav-tabs}
- <a href="#csv-service-request" role="tab" data-toggle="tab">CSV</a>
- <a href="#xml-service-request" role="tab" data-toggle="tab">XML</a>
- <a href="#json-service-request" role="tab" data-toggle="tab">JSON</a>

<div class="tab-content" markdown="1">

{: .tab-pane .active #csv-service-request}
~~~~
"service_request_id","requested_datetime","updated_datetime","closed_date","status_description","status_notes","source","service_name","service_subtype","description","agency_responsible","address","lat","long"
"638344","2010-04-14T06:37:38-08:00",2010-04-14T06:37:38-08:00","2010-04-14T06:37:38-08:00","closed","Duplicate Request.","Phone","Sidewalk and Curb Issues","sample subtype","sample description","sample agency","8TH AVE and JUDAH ST","37.762221815","-122.4651145"
~~~~

{: .tab-pane #xml-service-request}
~~~~
<?xml version="1.0" encoding="utf-8"?>
<service_requests>
    <request>
        <service_request_id>638344</service_request_id>
        <requested_datetime>2010-04-14T06:37:38-08:00</requested_datetime>
        <updated_datetime>2010-04-14T06:37:38-08:00</updated_datetime>
        <closed_datetime>2010-04-14T06:37:38-08:00</updated_datetime>
        <status_description>closed</status>
        <status_notes>Duplicate request.</status_notes>
        <source>Phone/source>
        <service_name>Sidewalk and Curb Issues</service_name>
        <service_subtype>sample subtype</service_subtype>
        <description>sample description</description>
        <agency_responsible>sample agency</agency_responsible>
        <address>8TH AVE and JUDAH ST</address>
        <lat>37.762221815</lat>
        <long>-122.4651145</long>
    </request>
</service_requests>
~~~~

{: .tab-pane #json-service-request}
~~~~
[
  {
    "service_request_id":638344,
    "requested_datetime":"2010-04-14T06:37:38-08:00",
    "updated_datetime":"2010-04-14T06:37:38-08:00",
    "closed_datetime":"2010-04-14T06:37:38-08:00",
    "status_description":"closed",
    "status_notes":"Duplicate request.",
    "source","Phone",
    "service_name":"Sidewalk and Curb Issues",
    "service_subtype":"sample subtype",
    "description":"sample description",
    "agency_responsible":"sample agency",
    "address":"8TH AVE and JUDAH ST",
    "lat":37.762221815,
    "long":-122.4651145
  }
]
~~~~
</div>