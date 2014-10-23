---
title: GeoReport_v1
permalink: /GeoReport_v1/
---

`The GeoReport v1 spec has been deprecated. Please see the current `[`GeoReport` `v2`](/GeoReport_v2 "wikilink")` spec`

Open 311 API
============

Description
-----------

The Open311 API allows developers to build applications to report non-emergency issues such as graffiti, potholes, and street cleaning directly to government organizations like cities. The following organizations have adopted this API and allow access:

Servers (can receive reports)
-----------------------------

<onlyinclude>

Servers receive and manage reports on behalf of a jurisdiction.

*Note that the URLs require a method and jurisdiction_id at the end, the root URL is not intended to be accessed directly.*

| Name                  | Status                   | API Key                                                    | city_id      | Dev API                                       | Production API       |
|-----------------------|--------------------------|------------------------------------------------------------|---------------|-----------------------------------------------|----------------------|
| **San Francisco**     | *Deprecated August 2013* | [Deprecated]                                               | sfgov.org     | [N/A Dev URL]                                 | [N/A Production URL] |
| **Miami-Dade County** | *Development Ready*      | [Request Key](http://miamidade.gov/mdc-open311/key/create) | miamidade.gov | [Beta URL](http://miamidade.gov/mdc-open311/) | -                    |
||

</onlyinclude>

### city_id

As a means to allow this API to be used by multiple cities we've included a "city_id" which will be the unique identifier for cities. It has been suggested that we use the city's url as the "city_id". We have incorporated that suggestion into our design and the city_id for San Francisco = sfgov.org

### service_list

-   **Purpose:** provide a list of acceptable 311 services and associated service code
-   **Method name:** service_list
-   **URL:**<https://open311.sfgov.org/dev/V1/service_list>
-   **Sample URL:** <https://open311.sfgov.org/dev/V1/service_list?api_key=xyz&city_id=sfgov.org>
-   '''Formats: '''xml
-   '''HTTP Method: '''GET
-   '''Requires Authentication: '''true
-   '''Arguments: '''
    -   api_key
    -   city_id (for SF = sfgov.org)
-   **Response:**
    -   service_name
    -   service_code
    -   service_description

**Example:**


    <ServiceResponse>
        <Open311ServiceList>
            <service service_code="001" service_name="Cans left out 24x7" service_description="Garbage or recycling cans that have been left out for more than 24 hours after collection. Violators will be cited. "/>
            <service service_code="002" service_name="Construction plate shifted" service_description="Metal construction plate covering the street or sidewalk has been moved. "/>
            <service service_code="003" service_name="Curb or curb ramp defect" service_description="Sidewalk curb or ramp has problems such as cracking, missing pieces, holes, and/or chipped curb. "/>
            <service service_code="004" service_name="Damaged city can" service_description="Damage to a city garbage receptacle such as missing parts (lid, door, liner) or other physical damage. "/>
            <service service_code="005" service_name="Damaged side sewer vent cover" service_description="Damage to a side sewer vent cover with problems such as cracking, bending, rusting, or denting"/>
            <service service_code="006" service_name="Damaged tree" service_description="Damage to a city maintained tree. To check whether a tree is city maintained: http://bit.ly/6hsDk1"/>
            <service service_code="007" service_name="Graffiti on bike rack - not offensive" service_description="Graffiti on a bike rack that does not contain racial slurs, profanity, or gang related language"/>
            <service service_code="008" service_name="Graffiti on news rack - not offensive" service_description="Graffiti on a news rack that does not contain racial slurs, profanity, or gang related language "/>
            <service service_code="009" service_name="Graffiti on parking meter - not offensive" service_description="Graffiti on a parking meter that does not contain racial slurs, profanity, or gang related language "/>
            <service service_code="010" service_name="Graffiti on pay phone - not offensive" service_description="Graffiti on a pay phone that does not contain racial slurs, profanity, or gang related language.  "/>
            <service service_code="011" service_name="Graffiti on private property - not offensive" service_description="Graffiti on a privately owned building or structure that does not contain racial slurs, profanity, or gang related language  "/>
            <service service_code="012" service_name="Graffiti on private property - offensive" service_description="Graffiti on a privately owned building or structure that contains racial slurs, profanity, or gang related language "/>
            <service service_code="013" service_name="Graffiti on public property - offensive" service_description="Graffiti on public property (building, pole, sidewalk, hydrant, etc) with racial slurs, profanity, or gang related language "/>
            <service service_code="014" service_name="Graffiti on public property- not offensive" service_description="Graffiti on public property (building, pole, sidewalk, hydrant, etc) without racial slurs, profanity, or gang related language  "/>
            <service service_code="015" service_name="Illegal dumping" service_description="Identify someone that has dumped or is dumping furniture or garbage onto the street or sidewalk. Violators will be cited "/>
            <service service_code="016" service_name="Landscaping request" service_description="Request maintenance on public property (except on park property) such as lawn mowing, bush or strip trimming and removal "/>
            <service service_code="017" service_name="Missed route - mechanical sweeping" service_description="Street cleaning sweeper did not show up as scheduled according to the street cleaning signs "/>
            <service service_code="018" service_name="Missing side sewer vent cover" service_description="The 4" side sewer vent cover (http://bit.ly/57BlOv) is missing from the sidewalk  "/>
            <service service_code="019" service_name="Overflowing city receptacle or dumpster" service_description="City receptacle is overflowing and/or has garbage on and around the container "/>
            <service service_code="020" service_name="Overgrown tree" service_description="Request that a city maintained tree (except on park property) be trimmed.  To check whether a tree is city maintained: http://bit.ly/6hsDk1 "/>
            <service service_code="021" service_name="Pothole in Street" service_description="Defect on the street such as broken, cracked, and sinking asphalt or concrete "/>
            <service service_code="022" service_name="Sewage coming out of catch basin" service_description="Sewage or dirty water coming out of a catchbasin (located at the corner of intersections) "/>
            <service service_code="023" service_name="Water coming from side sewer" service_description="Sewage or odor coming out of a 4" side sewer (http://bit.ly/57BlOv) located on the sidewalk "/>
            <service service_code="024" service_name="Sidewalk cleaning" service_description="Have garbage or human waste removed from the sidewalk and/or request services such as steam cleaning of sidewalks "/>
            <service service_code="025" service_name="Sidewalk defect" service_description="Defect on the sidewalk such as broken, cracked, and/or sinking concrete "/>
            <service service_code="026" service_name="Street cleaning" service_description="Request to have garbage or human waste removed from the street "/>
            <service service_code="027" service_name="Tree damaging property" service_description="Tree is damaging property (except for parks) or housing structure. City will address problem if it is a city maintained tree otherwise the property owner is notified to correct the issue "/>
            <service service_code="028" service_name="Water main break" service_description="Street is flooding due to water coming from within the asphalt or from a catchbasin "/>
            <service service_code="029" service_name="Graffiti on street sign" service_description="Graffiti on a street sign such as a stop sign, street name, and/or other parking and traffic signs "/>
            <service service_code="030" service_name="Odor coming from Side Sewer" service_description="Odor coming out of a 4" side sewer (http://bit.ly/57BlOv) located on the sidewalk.  "/>
            <service service_code="031" service_name="Sewage coming out of manhole cover" service_description="Sewage or dirty water coming out of a manhole cover (typically located in the a street or alley) "/>
            <service service_code="032" service_name="Sewage coming out of sewer vent" service_description="Sewage or dirty water coming out of a sewer vent (located on the sidewalk) "/>
            <service service_code="033" service_name="Pothole in bike lane" service_description="Defect in the bike lane such as broken, cracked, and sinking asphalt or concrete. "/>
        </Open311ServiceList>
    <Open311Error/>
    </ServiceResponse>

### Create Request

-   **Purpose:** Create service requests
-   **Method name:** create_request
-   **URL:** <https://open311.sfgov.org/dev/V1/create_request>
-   **Sample URL:**<https://open311.sfgov.org/dev/V1/create_request?api_key=xyz&city_id=sfgov.org&service_code=001&lat=37.76524078&lon>=-122.4212043&address_string=xxxx6thstreet&customer_email=smit333@sfgov.edu&device_id=tt222111&account_id=&first_name=jo&last_name=smith&phone_number=111111111&description=&media_url=<http://okgogo.gogo>
-   **Formats:** xml
-   **HTTP Method:** GET
-   **Requires Authentication:** true
-   **Arguments:**
    -   api_key
    -   city_id
    -   service_code (obtained from method service_list)
    -   lat [(WGS84)](http://en.wikipedia.org/wiki/World_Geodetic_System) (required - either lat/lon or address string, both are preferred)
    -   lon [(WGS84)](http://en.wikipedia.org/wiki/World_Geodetic_System) (required - either lat/lon or address string, both are preferred)
    -   address_string (human entered description of location)(if no lat/lon must provide this information)
    -   customer_email (optional)
    -   device_id (optional)
    -   account_id (optional)
    -   first_name (optional)
    -   last_name (optional)
    -   phone_number (optional)
    -   description (free form limited to 4,000 characters) (optional)
    -   media_url (url to the page that contains the media)(optional)

<!-- -->

-   '''Response: '''
    -   service_request_id
    -   service_level_agreement (may not be returned)
    -   account_id (may not be returned)
    -   error codes

**Example:**


    <CreateResponse>
        <Open311Error/>

        <Open311Create>
            <service_request_id>293944</service_request_id>

            <service_level_agreement>
                The City will inspect and require the responsible party to correct within 24 hours and/or issue a Correction Notice or Notice of Violation of the Public Works Code
            </service_level_agreement>

            <account_id/>

        </Open311Create>
    </CreateResponse>

### Status Update

-   **Purpose:** provide a status update for service request
-   **Method name:** status_update
-   **URL:** <https://open311.sfgov.org/dev/V1/status_update>
-   **Sample URL:** <https://open311.sfgov.org/dev/V1/status_update?api_key=xyz&city_id=sfgov.org&service_request_id=293450>
-   '''Formats: '''xml
-   '''HTTP Method: '''GET
-   '''Requires Authentication: '''true
-   '''Arguments: '''
    -   api_key\* city_id
    -   service_request_id

<!-- -->

-   **Response:**
    -   service_request_id
    -   status
    -   status_notes (may not be returned)
    -   service_name

**Example:**


    <StatusResponse>

        <Open311Status>
            <service_request_id>293735</service_request_id>
            <status>open</status>
            <status_notes/>
            <service_name>Graffiti on street sign</service_name>
        </Open311Status>

        <Open311Error/>
    </StatusResponse>

### Error Codes

**Response:**

-   errorCode (may not be returned)
-   errorDescription (may not be returned)

<!-- -->

-   service_list:
    -   100 Missing API Key
    -   101 Invalid APi Key
    -   102 General service error ( -- Missing service list file , anything that happens during service_list processing. It should be follow by an error description. The client will need to notify us)

<!-- -->

-   create_request
    -   200 Missing API Key
    -   201 Invalid API Key
    -   202 Missing service Code
    -   203 Invalid Service Code
    -   204 General Service Error ( anything captured during create_request processing , Lagan WS is down , ....An error description will follow. Client will need to notify us)

<!-- -->

-   status_update
    -   300 Missing API key
    -   301 Invalid API Key
    -   302 Id not valid or you are attemting to search for a service request you did not create
    -   302 General Service error ( anything captured during status_update processing. It will always have an error description ..Client will have to notify us)

<!-- -->

-   HTTP error code: (from the browser). So far I have seen this
    -   404 The URL request is invalid or open311 service is not running or reachable. Client should notify us after checking URL

**Example:**

Example URL: [<https://open311.sfgov.org/dev/V1/create_request?api_key=xyz&city_id=sfgov.org&service_code=001&lat=37.76524078&lon>=-122.4212043&address_string=xxxx6thstreet&customer_email=smit333@sfgov.edu&device_id=tt222111&account_id=&first_name=jo&last_name=smith&phone_number=111111111&description=&media_url=<http://okgogo.gogo> <https://open311.sfgov.org/dev/V1/create_request?api_key=xyz>........]


    <CreateResponse xmlns:m="http://org/sfgov/sf311/services" xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
        <Open311Error>
            <errorCode>201</errorCode>
            <errorDescription>Invalid api_key received -- can't proceed with create_request.</errorDescription>
        </Open311Error>
        <Open311Create/>
    </CreateResponse>

Query Service Requests
----------------------

Methods to query services requests have not yet been integrated into the spec. For now there are different options for different cities. Both San Francisco and Washington D.C. provide KML files of all service requests. San Francisco also provides a separate web service for service requests.

#### San Francisco

-   [KML](http://apps.sfgov.org/datafiles/index.php?dir=311)
-   [Guide to RESTful XML Web Service](http://apps.sfgov.org/datafiles/view.php?file=311/webservice.txt)

#### Washington D.C.

-   [KML](http://data.octo.dc.gov/feeds/src/src_current.kml)
-   [XML feed](http://data.octo.dc.gov/feeds/src/src_current.xml)
-   [Custom query](http://data.octo.dc.gov/NewCalendar.aspx?datasetid=4) also provides Shapefile export
-   [Plain text .zip](http://data.octo.dc.gov/feeds/src/src_current_plain.zip)
-   [Excel CSV](http://data.octo.dc.gov/feeds/src/src_current_csv.zip)
-   [Guide to Metadata](http://data.octo.dc.gov/Metadata.aspx?id=4)

#### Example Queries

###### **San Francisco**

<http://crmproxy.sfgov.org/status/ReportService/ProxyService/ReportCommandHandler?request_type=all&start_date=2010-04-13&end_date=2010-04-14>

###### **Washington D.C.**

<http://data.octo.dc.gov/Attachment.aspx?where=Police_Dictrict&area=SECOND&what=XML&date=serviceorderdate&from=4/14/2010%2012:00:00%20AM&to=4/15/2010%2011:59:00%20PM&dataset=SRC&datasetid=4&whereInd=3&areaInd=1&whatInd=2&dateInd=0&whenInd=1&disposition=attachment>
