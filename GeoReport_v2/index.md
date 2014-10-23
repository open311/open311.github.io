---
title: GeoReport_v2
permalink: /GeoReport_v2/
---

`This spec has been frozen and finalized, but the documentation will continue to be updated for clarity. Join the `[`Mailing` `List`](http://lists.open311.org/groups/discuss)` for updates.`

The GeoReport API v2 allows developers to build applications to both view and report issues which government entities like cities are responsible for addressing. These interactions are often referred to as "service requests" or "calls for service" and have traditionally been handled by custom web forms or phone based call centers (sometimes using the 311 phone number or other short-code). The GeoReport API is designed to allow both government and third party developers to create new applications and technologies that can integrate directly with these same official contact centers in any government that supports the standard. The current specification is focused on location-based non-emergency issues such as graffiti, potholes, and street cleaning.

The API consists of two main kinds of resources: <span class="strict-value">services</span> and service <span class="strict-value">requests</span>, but some servers that can't generate a realtime service request may also rely on a <span class="strict-value">token</span> resource. In total there are six methods used to interact with these resources: GET services, GET a service definition (a specific service_code id), POST a request, GET requests, GET a request (a specific service_request_id). The documentation below (starting from the API Methods section) is ordered based on a common sequence of interactions where a person first sees a list of available service types, selects one and creates a new service request, and then is able to track the status of that request and other requests. However each method can be accessed independently and some applications may only be focused on querying existing service requests to do analytics.

Status
------

### Specification

<span style="color:orange;font-weight:bold">Stable:</span> The GeoReport v2 Spec has been finalized, but we are still updating documentation for clarity and verifying compliance of implementations

### Servers

<onlyinclude>

Servers receive and manage service requests on behalf of a jurisdiction. **A comprehensive list is being maintained on the [GeoReport v2 Servers](/GeoReport_v2/Servers "wikilink") page** </onlyinclude>

Apps & Resources
----------------

-   See the [GeoReport v2 Developer Resources](/GeoReport_v2/Resources "wikilink") page for code libraries and open source applications.
-   See the [GeoReport v2 Support](/GeoReport_v2/Support "wikilink") page for applications, products, and services that support the spec.

Service Discovery
-----------------

GeoReport v2 and subsequent Open311 APIs are also required to have a standard service discovery file associated with them to provide routing between versions and types of APIs. See the [Service Discovery](/Service_Discovery "wikilink") page for details of the specification.

Internationalization and Encoding
---------------------------------

### Date/time format

All date/time fields must be formatted in a common subset of ISO 8601 as per the [w3 note](http://www.w3.org/TR/NOTE-datetime). Timezone information (either Z meaning UTC, or an HH:MM offset from UTC) **must** be included.

Examples:

-   1994-11-05T08:15:30-05:00 corresponds to November 5, 1994, 8:15:30 am, US Eastern Standard Time.
-   1994-11-05T13:15:30Z corresponds to the same instant.

### Encoding

UTF-8 is required everywhere.

All text returned by the service, whether in XML, JSON, or any other text-based content-type, MUST be encoded as UTF-8. Appropriate HTTP headers must be set, and the root element must be preceded with the XML declaration including the encoding="UTF-8" attribute. All text received by the service from the client will be assumed to be UTF-8 and must be decoded accordingly. Examples of the HTTP content-type headers for each format are shown below under Format Support.

Format Support
--------------

XML is a required format, but JSON can be provided at the discretion of the API provider. The output formats supported by the provider are indicated through the [Service Discovery](/Service_Discovery "wikilink") formats field for the API endpoint being used. The client can specify the desired format by appending the format name to the resource. For example a GET request to /services.xml for text/xml output from the services resource and /services/01.json for application/json ([RFC 4627](http://www.ietf.org/rfc/rfc4627.txt)) output for a specific service definition.

The HTTP content-type headers should look like this for each format:

**POST Service Request:** Content-Type: application/x-www-form-urlencoded; charset=utf-8

**XML:** Content-Type: text/xml; charset=utf-8

**JSON:** Content-Type: application/json; charset=utf-8

### XML Support

XML for the API should be Content-Type: text/xml. The XML output currently defined is schemaless and without a namespace declaration. For now, extending the output with additional namespaces should be done at your own risk. To guarantee that all clients can support the XML output, it is recommended that you adhere to the specification strictly and do not include foreign tags or namespaces. It is also assumed that the default namespace is not specified, but if it must be specified, the XMLNS URI is the URL of the specification: <http://wiki.open311.org/GeoReport_v2>

### JSON Support

JSON for the API should be Content-Type: application/json. JSON support is based on a programmatic mapping of the XML format using the [Spark Convention](http://wiki.open311.org/JSON_and_XML_Conversion#The_Spark_Convention). This means that if you have an XML file, you can easily generate the JSON version with XSL. This can be done using a server side XSLT ([php example](http://sandbox.georeport.org/tools/sparkjson/xml2json_spark_php.txt)).

Definitions
-----------

#### jurisdiction_id

As a means to allow this API to distinguish multiple jurisdictions within one API endpoint we've included a "jurisdiction_id" which will be the unique identifier for cities. It has been suggested that we use the jurisdiction's main website root url (without the www) as the "jurisdiction_id". For San Francisco, the jurisdiction_id is sfgov.org. Implementations can ignore this parameter and treat it as an "Optional Argument" if the implementation only serves one jurisdiction.

#### Optional Arguments

"Optional" means that the response should be the same whether a parameter is passed and is empty or is not passed at all. A null parameter should be treated as equivalent to a non-declared parameter in processing the request.

API methods
-----------

### GET Service List

| Purpose          | provide a list of acceptable 311 service request types and their associated service codes. These request types can be unique to the city/jurisdiction. |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| URL              | [https://[API](https://[API) endpoint]/services.[format]                                                                                               |
| Sample URL       | https://api.city.gov/dev/v2/services.xml?jurisdiction_id=city.gov                                                                                     |
| Formats          | XML (JSON available if denoted by [Service Discovery](/Service_Discovery "wikilink"))                                                                  |
| HTTP Method      | GET                                                                                                                                                    |
| Requires API Key | No                                                                                                                                                     |

#### Required Arguments

| Field Name         | Description | Notes & Requirements                                                                                |
|--------------------|-------------|-----------------------------------------------------------------------------------------------------|
| jurisdiction_id   |             | <span style="color: red">This is only required if the endpoint serves multiple jurisdictions</span> |

#### Response

| Field Name      | Description                                                                                                                                                                                                        | Notes & Requirements                                                                                                                              |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| services ⇊      |
| service ↴       |
| service_code   | The unique identifier for the service request type                                                                                                                                                                 |                                                                                                                                                   |
| service_name   | The human readable name of the service request type                                                                                                                                                                |                                                                                                                                                   |
| description     | A brief description of the service request type.                                                                                                                                                                   |                                                                                                                                                   |
| metadata        | Determines whether there are additional form fields for this service type.

                   -   <span class="strict-value">true</span>: This service request type requires additional metadata so the client will need to make a call to the [Service Definition](/#GET_Service_Definition "wikilink") method.
                   -   <span class="strict-value">false</span>: No additional information is required and a call to the [Service Definition](/#GET_Service_Definition "wikilink") method is not needed.                                | Possible values: <span class="strict-value">true</span>, <span class="strict-value">false</span>.                                                 |
| type            | -   <span class="strict-value">realtime</span>: The service request ID will be returned immediately after the service request is submitted.
                   -   <span class="strict-value">batch</span>: A token will be returned immediately after the service request is submitted. This token can then be later used to return the service request ID.
                   -   <span class="strict-value">blackbox</span>: No service request ID will be returned after the service request is submitted                                                                                       | Possible values: <span class="strict-value">realtime</span>, <span class="strict-value">batch</span>, <span class="strict-value">blackbox</span>. |
| keywords        | A comma separated list of tags or keywords to help users identify the request type. This can provide synonyms of the service_name and group.                                                                      |                                                                                                                                                   |
| group           | A category to group this service type within. This provides a way to group several service request types under one category such as "sanitation"                                                                   |                                                                                                                                                   |

#### Possible Errors

The numbers represent the HTTP status code returned for each error type:

-   404 - jurisdiction_id provided was not found (specify in error response)
-   400 - jurisdiction_id was not provided (specify in error response)
-   400 - General service error (Anything that fails during service list processing. The client will need to notify us)

#### Example response

<tabs> <tab title="XML">

    <?xml version="1.0" encoding="utf-8"?>
    <services>
        <service>
            <service_code>001</service_code>
            <service_name>Cans left out 24x7</service_name>
            <description>Garbage or recycling cans that have been left out for more than 24 hours after collection. Violators will be cited.</description>
            <metadata>true</metadata>
            <type>realtime</type>
            <keywords>lorem, ipsum, dolor</keywords>
            <group>sanitation</group>
        </service>
        <service>
            <service_code>002</service_code>
            <metadata>true</metadata>
            <type>realtime</type>
            <keywords>lorem, ipsum, dolor</keywords>
            <group>street</group>
            <service_name>Construction plate shifted</service_name>
            <description>Metal construction plate covering the street or sidewalk has been moved.</description>
        </service>
        <service>
            <service_code>003</service_code>
            <metadata>true</metadata>
            <type>realtime</type>
            <keywords>lorem, ipsum, dolor</keywords>
            <group>street</group>
            <service_name>Curb or curb ramp defect</service_name>
            <description>Sidewalk curb or ramp has problems such as cracking, missing pieces, holes, and/or chipped curb.</description>
        </service>
    </services>

</tab> <tab title="JSON">

    [
      {
        "service_code":001,
        "service_name":"Cans left out 24x7",
        "description":"Garbage or recycling cans that have been left out for more than 24 hours after collection. Violators will be cited.",
        "metadata":true,
        "type":"realtime",
        "keywords":"lorem, ipsum, dolor",
        "group":"sanitation"
      },
      {
        "service_code":002,
        "metadata":true,
        "type":"realtime",
        "keywords":"lorem, ipsum, dolor",
        "group":"street",
        "service_name":"Construction plate shifted",
        "description":"Metal construction plate covering the street or sidewalk has been moved."
      },
      {
        "service_code":003,
        "metadata":true,
        "type":"realtime",
        "keywords":"lorem, ipsum, dolor",
        "group":"street",
        "service_name":"Curb or curb ramp defect",
        "description":"Sidewalk curb or ramp has problems such as cracking, missing pieces, holes, and/or chipped curb."
      }
    ]

</tab> </tabs>

### GET Service Definition

| Conditional      | Yes - <span style="font-weight : bold; color: red">This call is only necessary if the Service selected has metadata set as *true* from the *GET Services* response</span> |
|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Purpose          | Define attributes associated with a service code. These attributes can be unique to the city/jurisdiction.                                                                |
| URL              | [https://[API](https://[API) endpoint]/services/[service_code].[format]                                                                                                  |
| Sample URL       | https://api.city.gov/dev/v2/services/033.xml?jurisdiction_id=city.gov                                                                                                    |
| Formats          | XML (JSON available if denoted by [Service Discovery](/Service_Discovery "wikilink"))                                                                                     |
| HTTP Method      | GET                                                                                                                                                                       |
| Requires API Key | No                                                                                                                                                                        |

#### Required Arguments

| Field Name                                     | Description | Notes & Requirements                                                                                |
|------------------------------------------------|-------------|-----------------------------------------------------------------------------------------------------|
| jurisdiction_id                               |             | <span style="color: red">This is only required if the endpoint serves multiple jurisdictions</span> |
| <span class="field-url">service_code</span>   |             | The service_code is specified in the main URL path rather than an added query string parameter.    |

#### Response

| Field Name              | Description                                                                                                                                                                                                                              | Notes & Requirements                                                                                                                                                                                                                                                                  |
|-------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| service_definition ↴   |
| service_code           | Returns the service_code associated with the definition, the same one submitted for this call.                                                                                                                                          |                                                                                                                                                                                                                                                                                       |
| attributes ⇊            |
| attribute ↴             |
| variable                | -   <span class="strict-value">true</span> denotes that user input is needed
                           -   <span class="strict-value">false</span> means the attribute is only used to present information to the user within the description field                                                                                              | Possible values: <span class="strict-value">true</span>, <span class="strict-value">false</span>.                                                                                                                                                                                     |
| code                    | A unique identifier for the attribute                                                                                                                                                                                                    |                                                                                                                                                                                                                                                                                       |
| datatype                | Denotes the type of field used for user input.

                           -   <span class="strict-value">string</span>: A string of characters without line breaks. Represented in an HTML form using an <input> tag
                           -   <span class="strict-value">number</span>: A numeric value. Represented in an HTML form using an <input> tag
                           -   <span class="strict-value">datetime</span>: The input generated must be able to transform into a valid ISO 8601 date. Represented in an HTML form using <input> tags
                           -   <span class="strict-value">text</span>: A string of characters that may contain line breaks. Represented in an HTML form using an
                               <textarea>
                               tag

                           -   <span class="strict-value">singlevaluelist</span>: A set of predefined values (specified in this response) where only one value may be selected. Represented in an HTML form using the <select> and <option> tags
                           -   <span class="strict-value">multivaluelist</span>: A set of predefined values (specified in this response) where several values may be selected. Represented in an HTML form using the <select multiple="multiple"> and <option> tags  | Options: <span class="strict-value">string</span>, <span class="strict-value">number</span>, <span class="strict-value">datetime</span>, <span class="strict-value">text</span>, <span class="strict-value">singlevaluelist</span>, <span class="strict-value">multivaluelist</span>. |
| required                | -   <span class="strict-value">true</span> means that the value is required to submit service request
                           -   <span class="strict-value">false</span> means that the value not required.                                                                                                                                                            | Options: <span class="strict-value">true</span>, <span class="strict-value">false</span>.                                                                                                                                                                                             |
| datatype_description   | A description of the datatype which helps the user provide their input                                                                                                                                                                   |                                                                                                                                                                                                                                                                                       |
| order                   | The sort order that the attributes will be presented to the user. 1 is shown first in the list.                                                                                                                                          | Any positive integer not used for other attributes in the same service_code                                                                                                                                                                                                          |
| description             | An description of the attribute field with instructions for the user to find and identify the requested information                                                                                                                      |                                                                                                                                                                                                                                                                                       |
| values ⇊                |
| value ↴                 |
| key                     | The unique identifier associated with an option for singlevaluelist or multivaluelist. This is analogous to the value attribute in an html option tag.                                                                                   |                                                                                                                                                                                                                                                                                       |
| name                    | The human readable title of an option for singlevaluelist or multivaluelist. This is analogous to the innerhtml text node of an html option tag.                                                                                         |                                                                                                                                                                                                                                                                                       |

#### Possible Errors

The numbers represent the HTTP status code returned for each error type:

-   404 - service_code or jurisdiction_id provided were not found (specify in error response)
-   400 - service_code or jurisdiction_id was not provided (specify in error response)
-   400 - General service error (Anything that fails during service list processing. The client will need to notify us)

#### Example response

<tabs> <tab title="XML">

    <?xml version="1.0" encoding="utf-8"?>
    <service_definition>
        <service_code>DMV66</service_code>
        <attributes>
            <attribute>
                <variable>true</variable>
                <code>WHISHETN</code>
                <datatype>singlevaluelist</datatype>
                <required>true</required>
                <datatype_description></datatype_description>
                <order>1</order>
                <description>What is the ticket/tag/DL number?</description>
                <values>
                    <value>
                        <key>123</key>
                        <name>Ford</name>
                    </value>
                    <value>
                        <key>124</key>
                        <name>Chrysler</name>
                    </value>
                </values>
            </attribute>
        </attributes>
    </service_definition>

</tab> <tab title="JSON">

    {
      "service_code":"DMV66",
      "attributes":[
        {
          "variable":true,
          "code":"WHISHETN",
          "datatype":"singlevaluelist",
          "required":true,
          "datatype_description":null,
          "order":1,
          "description":"What is the ticket/tag/DL number?",
          "values":[
            {
              "key":123,
              "name":"Ford"
            },
            {
              "key":124,
              "name":"Chrysler"
            }
          ]
        }
      ]
    }

</tab> </tabs>

### POST Service Request

| Purpose          | Create service requests                                                               |
|------------------|---------------------------------------------------------------------------------------|
| URL              | [https://[API](https://[API) endpoint]/requests.[format]                              |
| Sample URL       | https://api.city.gov/dev/v2/requests.xml                                              |
| Format sent      | Content-Type: application/x-www-form-urlencoded                                       |
| Formats returned | XML (JSON available if denoted by [Service Discovery](/Service_Discovery "wikilink")) |
| HTTP Method      | POST                                                                                  |
| Requires API Key | Yes                                                                                   |

#### Required Arguments

| Field Name                                                   | Description                                                   | Notes & Requirements                                                                                                                                                                                                                                                               |
|--------------------------------------------------------------|---------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| jurisdiction_id                                             |                                                               | <span style="color: red">This is only required if the endpoint serves multiple jurisdictions</span>                                                                                                                                                                                |
| service_code                                                |                                                               | This is obtained from [GET Service List](/#GET_Service_List "wikilink") method                                                                                                                                                                                                     |
| <span class="field-alternatives">location parameter</span>   | A full location parameter must be submitted.                  | One of <span class="strict-value">lat</span> & <span class="strict-value">long</span> or <span class="strict-value">address_string</span> or <span class="strict-value">address_id</span>                                                                                        |
| attribute                                                    | An array of key/value responses based on Service Definitions. | This takes the form of attribute[code]=value where multiple code/value pairs can be specified as well as multiple values for the same code in the case of a multivaluelist datatype (attribute[code1][]=value1&attribute[code1][]=value2&attribute[code1][]=value3) - see example.
                                                                                                                                <span style="color:red">This is only required if the service_code requires a service definition with required fields</span>.                                                                                                                                                       |

#### Optional Arguments

| Field Name        | Description                                                                                              | Notes & Requirements                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|-------------------|----------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lat               | Latitude using the [(WGS84)](http://en.wikipedia.org/wiki/World_Geodetic_System) projection.             | <span class="strict-value">lat</span> & <span class="strict-value">long</span> both need to be sent even though they are sent as two separate parameters. <span class="strict-value">lat</span> & <span class="strict-value">long</span> are required if no <span class="strict-value">address_string</span> or <span class="strict-value">address_id</span> is provided.                                                                           |
| long              | Longitude using the [(WGS84)](http://en.wikipedia.org/wiki/World_Geodetic_System) projection.            | <span class="strict-value">lat</span> & <span class="strict-value">long</span> both need to be sent even though they are sent as two separate parameters. <span class="strict-value">lat</span> & <span class="strict-value">long</span> are required if no <span class="strict-value">address_string</span> or <span class="strict-value">address_id</span> is provided.                                                                           |
| address_string   | Human entered address or description of location.                                                        | This is required if no <span class="strict-value">lat</span>/<span class="strict-value">long</span> or <span class="strict-value">address_id</span> are provided. This should be written from most specific to most general geographic unit, eg address number or cross streets, street name, neighborhood/district, city/town/village, county, postal code.                                                                                         |
| address_id       | The internal address ID used by a jurisdiction's master address repository or other addressing system.   | This is required if no <span class="strict-value">lat</span>/<span class="strict-value">long</span> or <span class="strict-value">address_string</span> are provided.                                                                                                                                                                                                                                                                                |
| email             | The email address of the person submitting the request                                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| device_id        | The unique device ID of the device submitting the request. This is usually only used for mobile devices. | Android devices can use TelephonyManager.getDeviceId() and iPhones can use [UIDevice currentDevice].uniqueIdentifier                                                                                                                                                                                                                                                                                                                                  |
| account_id       | The unique ID for the user account of the person submitting the request                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| first_name       | The given name of the person submitting the request                                                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| last_name        | The family name of the person submitting the request                                                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| phone             | The phone number of the person submitting the request                                                    |                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| description       | A full description of the request or report being submitted.                                             | This may contain line breaks, but not html or code. Otherwise, this is free form text limited to 4,000 characters.                                                                                                                                                                                                                                                                                                                                    |
| media_url        | A URL to media associated with the request, eg an image.                                                 | A convention for parsing media from this URL has yet to be established, so currently it will be done on a case by case basis much like Twitter.com does. For example, if a jurisdiction accepts photos submitted via Twitpic.com, then clients can parse the page at the Twitpic URL for the image given the conventions of Twitpic.com. This could also be a URL to a media RSS feed where the clients can parse for media in a more structured way. |

#### Response

| Field Name             | Description                                                                                                              | Notes & Requirements                                                                            |
|------------------------|--------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
| service_requests ⇊    |
| request ↴              |
| service_request_id   | The unique ID of the service request created.                                                                            | <span style="color: red">This should not be returned if token is returned</span>                |
| token                  | If returned, use this to call [GET service_request_id from a token](/#GET_service_request_id_from_a_token "wikilink"). | <span style="color: red">This should not be returned if service_request_id is returned</span> |
| service_notice        | Information about the action expected to fulfill the request or otherwise address the information reported.              | May not be returned                                                                             |
| account_id            | The unique ID for the user account of the person submitting the request.                                                 | May not be returned                                                                             |

#### Possible Errors

The numbers represent the HTTP status code returned for each error type:

-   404 - service_code or jurisdiction_id was not found (specified in error response)
-   400 - service_code or jurisdiction_id was not provided (specified in error response)
-   400 - General Service Error (Any failure during create request processing, eg CRM is down. Client will need to notify us)

#### Example Request

    POST /dev/v2/requests.xml
    Host: api.city.gov
    Content-Type: application/x-www-form-urlencoded; charset=utf-8

    api_key=xyz&jurisdiction_id=city.gov&service_code=001&lat=37.76524078&long=-122.4212043&address_string=1234+5th+street&email=smit333%40sfgov.edu&device_id=tt222111&account_id=123456&first_name=john&last_name=smith&phone=111111111&description=A+large+sinkhole+is+destroying+the+street&media_url=http%3A%2F%2Ffarm3.static.flickr.com%2F2002%2F2212426634_5ed477a060.jpg&attribute[WHISPAWN]=123456&attribute[WHISDORN]=COISL001

**Example response:** <tabs> <tab title="XML">

    <?xml version="1.0" encoding="utf-8"?>
    <service_requests>
        <request>
            <service_request_id>293944</service_request_id>
            <service_notice>
                The City will inspect and require the responsible party to correct within 24 hours and/or issue a Correction Notice or Notice of Violation of the Public Works Code
            </service_notice>
            <account_id/>
        </request>
    </service_requests>

</tab> <tab title="JSON">

    [
      {
        "service_request_id":293944,
        "service_notice":"The City will inspect and require the responsible party to correct within 24 hours and/or issue a Correction Notice or Notice of Violation of the Public Works Code",
        "account_id":null
      }
    ]

</tab> </tabs>

### GET service_request_id from a token

| Conditional      | Yes - <span style="font-weight : bold; color: red">This call is only necessary if the response from *POST Service Request* contains a token</span> |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| Purpose          | Get the service_request_id from a temporary token. This is unnecessary if the response from creating a service request does not contain a token. |
| URL              | [https://[API](https://[API) endpoint]/tokens/[token id].[format]                                                                                  |
| Sample URL       | https://api.city.gov/dev/v2/tokens/123456.xml?jurisdiction_id=city.gov                                                                            |
| Formats          | XML (JSON available if denoted by [Service Discovery](/Service_Discovery "wikilink"))                                                              |
| HTTP Method      | GET                                                                                                                                                |
| Requires API Key | No                                                                                                                                                 |

#### Required Arguments

| Field Name                             | Description | Notes & Requirements                                                                                |
|----------------------------------------|-------------|-----------------------------------------------------------------------------------------------------|
| jurisdiction_id                       |             | <span style="color: red">This is only required if the endpoint serves multiple jurisdictions</span> |
| <span class="field-url">token</span>   |             | This is obtained from the [POST Service Requests](/#POST_Service_Requests "wikilink") method        |

#### Response

| Field Name             | Description                                                                                                                                 | Notes & Requirements |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|----------------------|
| service_requests ⇊    |
| request ↴              |
| service_request_id   | The unique ID for the service request created. This can be used to call the [GET Service Request](/#GET_Service_Request "wikilink") method. |                      |
| token                  | The token ID used to make this call.                                                                                                        |                      |

#### Possible Errors

The numbers represent the HTTP status code returned for each error type:

-   404 - jurisdiction_id or token not found (specified in error response)
-   400 - jurisdiction_id or token was not provided (specified in error response)
-   400 - General Service error (Any failure during service query processing. Client will have to notify us)

#### Example response

<tabs> <tab title="XML">

    <?xml version="1.0" encoding="utf-8"?>
    <service_requests>
        <request>
            <service_request_id>638344</service_request_id>
            <token>12345</token>
        </request>
    </service_requests>

</tab> <tab title="JSON">

    [
      {
        "service_request_id":638344,
        "token":12345
      }
    ]

</tab> </tabs>

### GET Service Requests

| Purpose          | Query the current status of multiple requests                                                                                                  |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| URL              | [https://[API](https://[API) endpoint]/requests.[format]                                                                                       |
| Sample URL       | https://api.city.gov/dev/v2/requests.xml?start_date=2010-05-24T00:00:00Z&end_date=2010-06-24T00:00:00Z&status=open&jurisdiction_id=city.gov |
| Formats          | XML (JSON available if denoted by [Service Discovery](/Service_Discovery "wikilink"))                                                          |
| HTTP Method      | GET                                                                                                                                            |
| Requires API Key | No                                                                                                                                             |

#### Required Arguments

| Field Name         | Description | Notes & Requirements                                                                                |
|--------------------|-------------|-----------------------------------------------------------------------------------------------------|
| jurisdiction_id   |             | <span style="color: red">This is only required if the endpoint serves multiple jurisdictions</span> |

#### Optional Arguments

| Field Name             | Description                                                                                                                                                                                              | Notes & Requirements                                                                                        |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| service_request_id   | To call multiple Service Requests at once, multiple service_request_id can be declared; comma delimited.                                                                                               | This overrides all other arguments.                                                                         |
| service_code          | Specify the service type by calling the unique ID of the service_code.                                                                                                                                  | This defaults to all service codes when not declared; can be declared multiple times, comma delimited       |
| start_date            | Earliest datetime to include in search. When provided with end_date, allows one to search for requests which have a requested_datetime that matches a given range, but may not span more than 90 days. | When not specified, the range defaults to most recent 90 days. Must use w3 format, eg 2010-01-01T00:00:00Z. |
| end_date              | Latest datetime to include in search. When provided with start_date, allows one to search for requests which have a requested_datetime that matches a given range, but may not span more than 90 days. | When not specified, the range defaults to most recent 90 days. Must use w3 format, eg 2010-01-01T00:00:00Z. |
| status                 | Allows one to search for requests which have a specific status. This defaults to all statuses; can be declared multiple times, comma delimited;                                                          | Options: <span class="strict-value">open</span>, <span class="strict-value">closed</span>                   |

#### Response

| Field Name             | Description                                                                                                                                  | Notes & Requirements                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| service_requests ⇊    |
| request ↴              |
| service_request_id   | The unique ID of the service request created.                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| status                 | The current status of the service request.

                          -   <span class="strict-value">open</span>: it has been reported.
                          -   <span class="strict-value">closed</span>: it has been resolved.                                                                           | Options: <span class="strict-value">open</span>, <span class="strict-value">closed</span>                                                                                                                                                                                                                                                                                                                                                             |
| status_notes          | Explanation of why status was changed to current state or more details on current status than conveyed with status alone.                    | May not be returned                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| service_name          | The human readable name of the service request type                                                                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| service_code          | The unique identifier for the service request type                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| description            | A full description of the request or report submitted.                                                                                       | This may contain line breaks, but not html or code. Otherwise, this is free form text limited to 4,000 characters.                                                                                                                                                                                                                                                                                                                                    |
| agency_responsible    | The agency responsible for fulfilling or otherwise addressing the service request.                                                           | May not be returned                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| service_notice        | Information about the action expected to fulfill the request or otherwise address the information reported.                                  | May not be returned                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| requested_datetime    | The date and time when the service request was made.                                                                                         | Returned in w3 format, eg 2010-01-01T00:00:00Z                                                                                                                                                                                                                                                                                                                                                                                                        |
| updated_datetime      | The date and time when the service request was last modified. For requests with status=closed, this will be the date the request was closed. | Returned in w3 format, eg 2010-01-01T00:00:00Z                                                                                                                                                                                                                                                                                                                                                                                                        |
| expected_datetime     | The date and time when the service request can be expected to be fulfilled. This may be based on a service-specific service level agreement. | May not be returned                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| address                | Human readable address or description of location.                                                                                           | This should be provided from most specific to most general geographic unit, eg address number or cross streets, street name, neighborhood/district, city/town/village, county, postal code.                                                                                                                                                                                                                                                           |
| address_id            | The internal address ID used by a jurisdictions master address repository or other addressing system.                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| zipcode                | The postal code for the location of the service request.                                                                                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| lat                    | latitude using the [(WGS84)](http://en.wikipedia.org/wiki/World_Geodetic_System) projection.                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| long                   | longitude using the [(WGS84)](http://en.wikipedia.org/wiki/World_Geodetic_System) projection.                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| media_url             | A URL to media associated with the request, eg an image.                                                                                     | A convention for parsing media from this URL has yet to be established, so currently it will be done on a case by case basis much like Twitter.com does. For example, if a jurisdiction accepts photos submitted via Twitpic.com, then clients can parse the page at the Twitpic URL for the image given the conventions of Twitpic.com. This could also be a URL to a media RSS feed where the clients can parse for media in a more structured way. |

#### Response Volume

-   Default query limit is a span of 90 days or first 1000 requests returned, whichever is smallest.

#### Possible Errors

The numbers represent the HTTP status code returned for each error type:

-   404 - jurisdiction_id not found (specified in error response)
-   400 - jurisdiction_id was not provided (specified in error response)
-   400 - General Service error (Any failure during service query processing. Client will have to notify us)

#### Example response

<tabs> <tab title="XML">

    <?xml version="1.0" encoding="utf-8"?>
    <service_requests>
        <request>
            <service_request_id>638344</service_request_id>
            <status>closed</status>
            <status_notes>Duplicate request.</status_notes>
            <service_name>Sidewalk and Curb Issues</service_name>
            <service_code>006</service_code>
            <description></description>
            <agency_responsible></agency_responsible>
            <service_notice></service_notice>
            <requested_datetime>2010-04-14T06:37:38-08:00</requested_datetime>
            <updated_datetime>2010-04-14T06:37:38-08:00</updated_datetime>
            <expected_datetime>2010-04-15T06:37:38-08:00</expected_datetime>
            <address>8TH AVE and JUDAH ST</address>
            <address_id>545483</address_id>
            <zipcode>94122</zipcode>
            <lat>37.762221815</lat>
            <long>-122.4651145</long>
            <media_url>http://city.gov.s3.amazonaws.com/requests/media/638344.jpg </media_url>
        </request>
        <request>
            <service_request_id>638349</service_request_id>
            <status>open</status>
            <status_notes></status_notes>
            <service_name>Sidewalk and Curb Issues</service_name>
            <service_code>006</service_code>
            <description></description>
            <agency_responsible></agency_responsible>
            <service_notice></service_notice>
            <requested_datetime>2010-04-19T06:37:38-08:00</requested_datetime>
            <updated_datetime>2010-04-19T06:37:38-08:00</updated_datetime>
            <expected_datetime>2010-04-19T06:37:38-08:00</expected_datetime>
            <address>8TH AVE and JUDAH ST</address>
            <address_id>545483</address_id>
            <zipcode>94122</zipcode>
            <lat>37.762221815</lat>
            <long>-122.4651145</long>
            <media_url>http://city.gov.s3.amazonaws.com/requests/media/638349.jpg </media_url>
        </request>
    </service_requests>

</tab> <tab title="JSON">

    [
      {
        "service_request_id":638344,
        "status":"closed",
        "status_notes":"Duplicate request.",
        "service_name":"Sidewalk and Curb Issues",
        "service_code":006,
        "description":null,
        "agency_responsible":null,
        "service_notice":null,
        "requested_datetime":"2010-04-14T06:37:38-08:00",
        "updated_datetime":"2010-04-14T06:37:38-08:00",
        "expected_datetime":"2010-04-15T06:37:38-08:00",
        "address":"8TH AVE and JUDAH ST",
        "address_id":545483,
        "zipcode":94122,
        "lat":37.762221815,
        "long":-122.4651145,
        "media_url":"http://city.gov.s3.amazonaws.com/requests/media/638344.jpg "
      },
      {
        "service_request_id":638349,
        "status":"open",
        "status_notes":null,
        "service_name":"Sidewalk and Curb Issues",
        "service_code":006,
        "description":null,
        "agency_responsible":null,
        "service_notice":null,
        "requested_datetime":"2010-04-19T06:37:38-08:00",
        "updated_datetime":"2010-04-19T06:37:38-08:00",
        "expected_datetime":"2010-04-19T06:37:38-08:00",
        "address":"8TH AVE and JUDAH ST",
        "address_id":545483,
        "zipcode":94122,
        "lat":37.762221815,
        "long":-122.4651145,
        "media_url":"http://city.gov.s3.amazonaws.com/requests/media/638349.jpg"
      }
    ]

</tab> </tabs>

### GET Service Request

| Purpose          | Query the current status of an individual request                                     |
|------------------|---------------------------------------------------------------------------------------|
| URL              | [https://[API](https://[API) endpoint]/requests/[service_request_id].[format]       |
| Sample URL       | https://api.city.gov/dev/v2/requests/123456.xml?jurisdiction_id=city.gov             |
| Formats          | XML (JSON available if denoted by [Service Discovery](/Service_Discovery "wikilink")) |
| HTTP Method      | GET                                                                                   |
| Requires API Key | No                                                                                    |

#### Required Arguments

| Field Name                                            | Description | Notes & Requirements                                                                                    |
|-------------------------------------------------------|-------------|---------------------------------------------------------------------------------------------------------|
| jurisdiction_id                                      |             | <span style="color: red">This is only required if the endpoint serves multiple jurisdictions</span>     |
| <span class="field-url">service_request_id</span>   |             | The service_request_id is specified in the main URL path rather than an added query string parameter. |

#### Optional Arguments

None

#### Response

| Field Name             | Description                                                                                                                                  | Notes & Requirements                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| service_requests ⇊    |
| request ↴              |
| service_request_id   | The unique ID of the service request created.                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| status                 | The current status of the service request.

                          -   <span class="strict-value">open</span>: it has been reported.
                          -   <span class="strict-value">closed</span>: it has been resolved.                                                                           | Options: <span class="strict-value">open</span>, <span class="strict-value">closed</span>                                                                                                                                                                                                                                                                                                                                                             |
| status_notes          | Explanation of why status was changed to current state or more details on current status than conveyed with status alone.                    | May not be returned                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| service_name          | The human readable name of the service request type                                                                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| service_code          | The unique identifier for the service request type                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| description            | A full description of the request or report submitted.                                                                                       | This may contain line breaks, but not html or code. Otherwise, this is free form text limited to 4,000 characters.                                                                                                                                                                                                                                                                                                                                    |
| agency_responsible    | The agency responsible for fulfilling or otherwise addressing the service request.                                                           | May not be returned                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| service_notice        | Information about the action expected to fulfill the request or otherwise address the information reported.                                  | May not be returned                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| requested_datetime    | The date and time when the service request was made.                                                                                         | Returned in w3 format, eg 2010-01-01T00:00:00Z                                                                                                                                                                                                                                                                                                                                                                                                        |
| updated_datetime      | The date and time when the service request was last modified. For requests with status=closed, this will be the date the request was closed. | Returned in w3 format, eg 2010-01-01T00:00:00Z                                                                                                                                                                                                                                                                                                                                                                                                        |
| expected_datetime     | The date and time when the service request can be expected to be fulfilled. This may be based on a service-specific service level agreement. | May not be returned                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| address                | Human readable address or description of location.                                                                                           | This should be provided from most specific to most general geographic unit, eg address number or cross streets, street name, neighborhood/district, city/town/village, county, postal code.                                                                                                                                                                                                                                                           |
| address_id            | The internal address ID used by a jurisdictions master address repository or other addressing system.                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| zipcode                | The postal code for the location of the service request.                                                                                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| lat                    | latitude using the [(WGS84)](http://en.wikipedia.org/wiki/World_Geodetic_System) projection.                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| long                   | longitude using the [(WGS84)](http://en.wikipedia.org/wiki/World_Geodetic_System) projection.                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| media_url             | A URL to media associated with the request, eg an image.                                                                                     | A convention for parsing media from this URL has yet to be established, so currently it will be done on a case by case basis much like Twitter.com does. For example, if a jurisdiction accepts photos submitted via Twitpic.com, then clients can parse the page at the Twitpic URL for the image given the conventions of Twitpic.com. This could also be a URL to a media RSS feed where the clients can parse for media in a more structured way. |

#### Possible Errors

The numbers represent the HTTP status code returned for each error type:

-   404 - jurisdiction_id not found (specified in error response)
-   400 - jurisdiction_id was not provided (specified in error response)
-   400 - General Service error (Any failure during service query processing. Client will have to notify us)

#### Example response

<tabs> <tab title="XML">

    <?xml version="1.0" encoding="utf-8"?>
    <service_requests>
        <request>
            <service_request_id>638344</service_request_id>
            <status>closed</status>
            <status_notes>Duplicate request.</status_notes>
            <service_name>Sidewalk and Curb Issues</service_name>
            <service_code>006</service_code>
            <description></description>
            <agency_responsible></agency_responsible>
            <service_notice></service_notice>
            <requested_datetime>2010-04-14T06:37:38-08:00</requested_datetime>
            <updated_datetime>2010-04-14T06:37:38-08:00</updated_datetime>
            <expected_datetime>2010-04-15T06:37:38-08:00</expected_datetime>
            <address>8TH AVE and JUDAH ST</address>
            <address_id>545483</address_id>
            <zipcode>94122</zipcode>
            <lat>37.762221815</lat>
            <long>-122.4651145</long>
            <media_url>http://city.gov.s3.amazonaws.com/requests/media/638344.jpg </media_url>
        </request>
    </service_requests>

</tab> <tab title="JSON">

    [
      {
        "service_request_id":638344,
        "status":"closed",
        "status_notes":"Duplicate request.",
        "service_name":"Sidewalk and Curb Issues",
        "service_code":006,
        "description":null,
        "agency_responsible":null,
        "service_notice":null,
        "requested_datetime":"2010-04-14T06:37:38-08:00",
        "updated_datetime":"2010-04-14T06:37:38-08:00",
        "expected_datetime":"2010-04-15T06:37:38-08:00",
        "address":"8TH AVE and JUDAH ST",
        "address_id":545483,
        "zipcode":94122,
        "lat":37.762221815,
        "long":-122.4651145,
        "media_url":"http://city.gov.s3.amazonaws.com/requests/media/638344.jpg"
      }
    ]

</tab> </tabs>

### Errors

#### Response

| Field Name    | Description                                                                                                                       | Notes & Requirements |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------|----------------------|
| errors ⇊      |
| error ↴       |
| code          | The error code representing the type of error. In most cases, this should match the HTTP status code returned in the HTTP header. |                      |
| description   | A human readable description of the error that occurred. This is meant to be seen by the user.                                    |                      |

-   **General Errors**
    -   403 - Missing or Invalid API Key (specify in error message)
    -   400 - The URL request is invalid or open311 service is not running or reachable. Client should notify us after checking URL

HTTP error codes are required, but the code in the response body shouldn't necessarily match the HTTP error code, so that more specific and unique error code identifiers can be used. The HTTP error codes should always be 404 for resources that don't exist, 403 for errors because of wrong or missing api_key and basically 400 for any other error where the request can not be fulfilled as expected. Multiple errors codes and descriptions can be returned in the body (the response is an array).

**Example:** <tabs> <tab title="XML">

    HTTP/1.1 403 Forbidden

    <?xml version="1.0" encoding="utf-8"?>
    <errors>
        <error>
            <code>403</code>
            <description>Invalid api_key received -- can't proceed with create_request.</description>
        </error>
    </errors>

</tab> <tab title="JSON">

    HTTP/1.1 403 Forbidden

    [
      {
        "code":403,
        "description":"Invalid api_key received -- can't proceed with create_request."
      }
    ]

</tab> </tabs>
