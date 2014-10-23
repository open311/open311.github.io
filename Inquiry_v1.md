---
title: Inquiry_v1
permalink: /Inquiry_v1/
---

<div style="background-color:#FFF79C">
Please refer to the NYC Developer Portal for the latest 311 API documentation (https://developer.cityofnewyork.us/api/open311-inquiry)

Additionally, NYC will be decommissioning its inquiry API in the Spring of 2014. Users should visit the NYC Developer portal from that point on.

Note: some of this content is NYC-specific (such as URLs and Category values). Future updates to the specification will need to have these items separated out.

**Use [Inquiry v2 Draft](/Inquiry_v2_Draft "wikilink") to review and add ideas for the next iteration of this proposal and please use the [mailing list](http://lists.open311.org/groups/discuss) for discussion**

</div>
HTTP 302 responses (Found/Moved Temporarily) should be accepted and followed by client agents.

Note: NYC's implementation is case-sensitive.

While it's not required, please consider registering for NYC's endpoint to be informed about any updates or changes to their API. Their registration page and more information can be found on [nyc.gov](http://home2.nyc.gov/apps/311/allServices.htm?searchUrl=/apps/311/simpleSearchResults.htm%3Fsearch%3DAPI&requestType=service&levelOneId=079351C6-06AD-11DE-AC9C-EF5AFBC474DE&levelTwoId=079351C6-06AD-11DE-AC9C-EF5AFBC474DE-0&serviceName=311+Content+API&finalSubLevel=2&intentId=E9E66310-8137-11DE-8E9F-96DAE110FEB8)

Services
========

Services are services and information that are offered to the public

The Get Services functionality consists of two methods. The first method, “Get Service List”, retrieves a list of all of the services when invoked. The second method, “Get Service”, retrieves detailed information about the Service requested when invoked.

Get Service List
----------------

This method retrieves a list of links to all services and a brief description of each Service. This method takes a category or a type as an optional input. If a category is provided, the list of Services returned will be restricted such that only Services which belong to that category will be included in the response.

### URL

<http://><content_api_root>/services/<category>.<content_type>

#### Sample URLs

-   <http://www.nyc.gov/portal/apps/311_contentapi/services/all.xml>
-   <http://www.nyc.gov/portal/apps/311_contentapi/services/all.json>
-   <http://www.nyc.gov/portal/apps/311_contentapi/services/Social%20Services.xml>
-   <http://www.nyc.gov/portal/apps/311_contentapi/services/web.xml>
-   <http://www.nyc.gov/portal/apps/311_contentapi/services/finder.json>

### Inputs

-   category (/type) – a category or type for a Service. If a category is supplied then the list of Services returned will be restricted to Services belonging to this category. The following categories are supported:

| Category                               | URL Encoded Value                                |
|----------------------------------------|--------------------------------------------------|
| Transportation, Streets, and Sidewalks | Transportation%2C%20Streets%2C%20and%20Sidewalks |
| Environment and Sanitation             | Environment%20and%20Sanitation                   |
| Property, Buildings and Homes          | Property%2C%20Buildings%2C%20and%20Homes         |
| Education and Employment               | Education%20and%20Employment                     |
| Business and Finance                   | Business%20and%20Finance                         |
| Social Services                        | Social%20Services                                |
| Health and Medicine                    | Health%20and%20Medicine                          |
| Public Safety and Law                  | Public%20Safety%20and%20Law                      |
| Government and Civil Services          | Government%20and%20Civil%20Services              |

The following types are supported:

| Type                     | URL Encoded Value | Description                                                                                                                                                                                     |
|--------------------------|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Top Mobile Services      | mobile            | Services selected by the 311 Content Team to be promoted as “Top Services” on the 311 iPhone application. (A service may exist as a top service for a web platform, a mobile platform or both). |
| Top Web Services         | web               | Services selected by the 311 Content Team to be promoted as “Top Services” on the 311 Online Homepage. ( A service may exist as a top service for a web platform, a mobile platform or both).   |
| Facility Finder Services | finder            | 311 Online services that have a Facility Finder functionality embedded on the service’s page.                                                                                                   |

### Response Structure

#### Field Descriptions

-   id – the unique identifier of the Service record
-   service_name – name of the Service record
-   expiration – the date the Service expires. Expiration will occur at 12:00 AM of the date specified.
-   brief_description – a short description of the Service

<tabs> <tab title="XML">

    <services>
      <service>
        <id>20090318-FA993876-13C9-11DE-9981-FA93D1CD8644</id>
        <service_name>Noise Complaint</service_name>
        <expiration>2011-12-31T23:59:59Z</expiration>
        <brief_description>Complaint about excessive noise.</brief_description>
      </service>
    </services>

</tab> <tab title="JSON">

    [
      {
        "id":"20090318-FA993876-13C9-11DE-9981-FA93D1CD8644",
        "service_name":"Noise Complaint",
        "expiration":"2011-12-31T23:59:59Z",
        "brief_description":"Complaint about excessive noise."
      }
    ]

</tab> </tabs>

Get Service
-----------

This method retrieves detailed information about the Service requested. Services are specified using the Id of the Service.

### URL

<http://><content_api_root>/services/<service_id>.<content_type>

#### Sample URLs

-   <http://www.nyc.gov/portal/apps/311_contentapi/services/2003-07-21-11-45-37_000010083f1c0aa44000a0e7.xml>
-   <http://www.nyc.gov/portal/apps/311_contentapi/services/2003-07-21-11-45-37_000010083f1c0aa44000a0e7.json>

### Inputs

-   service_id – the Id of the Service being requested.

### Response Structure

#### Field Descriptions

-   id – the unique identifier of the Service record
-   service_name – the name of the Service record
-   expiration – the date the Service expires. Expiration will occur at 12:00 AM of the date specified.
-   categories – a list of taxonomy categories that the Service belongs to
-   url – the URL that points to the Service on 311 Online
-   brief_description – a short description of the Service
-   description – the detailed description of the Service, cleansed of HTML elements
-   description_html – the detailed description of the Service, contains HTML elements
-   web actions – a list of links or plain text that specify actions available pertaining to a service
-   type – the type of Web Action. Possible values are: “Service Request”, “Link”, and “Literature”
-   label – human readable text label for a web action
-   url – the URL for a Web Action that is a link

<tabs> <tab title="XML">

    <services>
      <service>
        <id> 2003-07-21-11-45-37_000010083f1c0aa44000a0e7</id>
        <service_name> Home Ownership Kit</service_name>
        <expiration>2011-12-31T23:59:59Z</expiration>
        <cateogries>
          <category_name>Property, Buildings & Homes</category_name>
        </cateogries>
        <url> http://www.nyc.gov/apps/311/allServices.htm?requestType=topService&serviceName=Home+Ownership+Kit </url>
        <brief_description> Get a kit to guide you through the process of becoming a homeowner. </brief_description>
        <description> The City offers information about becoming a New York City homeowner, including: Lists of affordable homes that are currently accepting applications The steps of the buying process Down payment assistance Homebuyer education training</description>
        <description_html>
          <![CDATA[The City offers information about becoming a New York City homeowner, including:<br /><br /><ul class="dashes"><li>Lists of affordable homes that are currently accepting applications</li><li>The steps of the buying process</li><li>Down payment assistance</li><li>Homebuyer education training</li></ul>]]>
        </description_html>
        <web_actions>
          <web_action type="Link">
            <label> Get information about home ownership.</label>
            <url> http://www.nyc.gov/html/hpd/html/buyers/guide.shtml</url>
          </web_action>
          <web_action type="Link">
            <label> Download the Home Ownership Kit (PDF).</label>
            <url> http://www.nyc.gov/download/311/HPD/homeownership-kit.pdf</url>
          </web_action>
        </web_actions>
      </service>
    </services>

</tab> <tab title="JSON">

    [
      {
        "id":" 2003-07-21-11-45-37_000010083f1c0aa44000a0e7",
        "service_name":" Home Ownership Kit",
        "expiration":"2011-12-31T23:59:59Z",
        "categories":[
          {
            "category_name":"Property, Buildings & Homes"
          }
        ],
        "url":" http://www.nyc.gov/apps/311/allServices.htm?requestType=topService&serviceName=Home+Ownership+Kit ",
        "brief_description":" Get a kit to guide you through the process of becoming a homeowner. ",
        "description":"The City offers information about becoming a New York City homeowner, including: Lists of affordable homes that are currently accepting applications The steps of the buying process Down payment assistance Homebuyer education training",
        "description_html":" The City offers information about becoming a New York City homeowner, including:<br /><br /><ul class="dashes"><li>Lists of affordable homes that are currently accepting applications</li><li>The steps of the buying process</li><li>Down payment assistance</li><li>Homebuyer education training</li></ul>",
        "web_actions":[
          {
            "type":"Link",
            "label":"Get information about home ownership.",
            "url":" http://www.nyc.gov/html/hpd/html/buyers/guide.shtml"
          },
          {
            "type":"Link",
            "label":"Download the Home Ownership Kit (PDF).",
            "url":" http://www.nyc.gov/download/311/HPD/homeownership-kit.pdf"
          }
        ]
      }
    ]

</tab> </tabs>

Facilities
==========

Facilities include offices, providers, and recreational locations available to the public.

The Get Facility functionality consists of two methods. The first method, “Get Facility List”, retrieves a list of all of the facilities when invoked. The second method, “Get Facility”, retrieves detailed information about the Facility requested when invoked.

Get Facility List
-----------------

This method retrieves a list of links to all Facilities and a brief description of each Facility. This method takes a category as an optional input. If a category is provided, the list of Facilities returned will be restricted such that only Facilities of the specified category will be included in the response.

### URL

<http://><content_api_root>/facilities/<category>.<content_type>

#### Sample URLs

-   <http://www.nyc.gov/portal/apps/311_contentapi/facilities/all.xml>
-   <http://www.nyc.gov/portal/apps/311_contentapi/facilities/all.json>
-   <http://www.nyc.gov/portal/apps/311_contentapi/facilities/Beach.json>

### Inputs

-   category - a category for a Facility. If this argument is supplied then the list of Facilities returned will be restricted to Facilities of this type. The following category values are supported:

| Input Value                 | Encoded Input Value               |
|-----------------------------|-----------------------------------|
| After School Program        | After%20School%20Program          |
| Beach                       | Beach                             |
| Business Solution Center    | Business%20Solution%20Center      |
| Child Care Center           | Child%20Care%20Center             |
| Clinic                      | Clinic                            |
| Community Board             | Community%20Board                 |
| Cultural Institution        | Cultural%20Institution            |
| DRIE Enrollment Center      | DRIE%20Enrollment%20Center        |
| DSNY Garage                 | DSNY%20Garage                     |
| EITC Assistance Center      | EITC%20Assistance%20Center        |
| Financial Education Site    | Financial%20Education%20Site      |
| Food Provider               | Food%20Provider                   |
| Food Stamp Center           | Food%20Stamp%20Center             |
| Golf                        | Golf                              |
| Green Market                | Green%20Market                    |
| HomeBase Site               | HomeBase%20Site                   |
| Hospital                    | Hospital                          |
| Immigrant Service Provider  | Immigrant%20Service%20Provider    |
| Jail Release Services       | Jail%20Release%20Services         |
| Library                     | Library                           |
| Medicaid Office             | Medicaid%20Office                 |
| Medicare Drug Counseling    | Medicare%20Drug%20Counseling      |
| Municipal Parking Facility  | Municipal%20Parking%20Facility    |
| Non-Profit Organization     | Non-Profit%20Organization         |
| Nurse Home Visiting Program | Nurse%20Home%20Visiting%20Program |
| Park                        | Park                              |
| Pool                        | Pool                              |
| Precinct                    | Precinct                          |
| Quit Smoking Clinic         | Quit%20Smoking%20Clinic           |
| Recreation Center           | Recreation%20Center               |
| School                      | School                            |
| School District             | School%20District                 |
| Summer Meal Program         | Summer%20Meal%20Program           |
| Universal Pre-K             | Universal%20Pre-K                 |
| Workforce1 Career Center    | Workforce1%20Career%20Center      |
| Youth Employment            | Youth%20Employment                |

### Response Structure

#### Field Descriptions

-   id – the unique identifier for a Facility record
-   facility_name – the name of a Facility record
-   expiration – the date that the Facility expires. Expiration will occur at 12:00 AM of the date specified.
-   brief_description – a short description of the Facility
-   Note: When requesting a list of all facilities, the facility type (category) will also be included.

<tabs> <tab title="XML">

    <facilities>
      <facility>
        <id>20090318-FA993876-13C9-11DE-9981-FA93D1CD8644</id>
        <facility_name>Tompkins Square Park</facility_name>
        <expiration>2011-12-31T23:59:59Z</expiration>
        <type>Park</type>
        <brief_description>A small park located in the Alphabet City section of the East Village in Manhattan.
        </brief_description>
      </facility>
    </facilities>

</tab> <tab title="JSON">

    [
      {
        "id":"20090318-FA993876-13C9-11DE-9981-FA93D1CD8644",
        "facility_name":"Tompkins Square Park",
        "expiration":"2011-12-31T23:59:59Z",
        "type":"Park",
        "brief_description":"A small park located in the Alphabet City section of the East Village in Manhattan."
      }
    ]

</tab> </tabs>

Get Facility
------------

This method retrieves detailed information about the Facility requested. Facilities are specified using the ID of the Facility.

### URL

<http://><content_api_root>/facilities/<facility_id>.<content_type>

#### Sample URLs

-   <http://www.nyc.gov/portal/apps/311_contentapi/facilities/20040329-052C82FA-81F5-11D8-ACEF-DCA5D018311B.xml>
-   <http://www.nyc.gov/portal/apps/311_contentapi/facilities/20040329-052C82FA-81F5-11D8-ACEF-DCA5D018311B.json>

### Inputs

-   facility_id – the Id of the Facility being requested.

### Response Structure

#### Field Descriptions:

-   id – the unique identifier for a Facility record
-   facility_name – the name of a Facility
-   expiration – the date that the Facility expires. Expiration will occur at 12:00 AM of the date specified.
-   type – the type of office, provider, or recreational Facility
-   brief_description – a short description of the Facility
-   description – the detailed description of the Facility
-   features – characteristics of a Facility
-   feature_name – the name of a Facility Feature
-   address – the street address of the Facility
-   additional_address_information – additional information about the Facility’s location
-   borough – the borough of the Facility. Possible values are: Manhattan, Brooklyn, The Bronx, Queens, and Staten Island
-   city – the city the Facility is located in.
-   state – the state the Facility is located in
-   zipcode – the zip code of the Facility
-   displayed_hours – hours of operation for a Facility
-   lat – the latitude of the Facility (this value may only be compatible with NY State Plane coordinate systems)
-   long – the longitude of the Facility (this value may only be compatible with NY State Plane coordinate systems)
-   eligibility_information – requirements for being eligible to use the Facility.

<tabs> <tab title="XML">

    <facilities>
      <facility>
        <id>20040329-052C82FA-81F5-11D8-ACEF-DCA5D018311B</id>
        <facility_name>Mccarren Park</facility_name>
        <expiration>12-31-2099T00:00:00Z</expiration>
        <type>Park</type>
        <brief_description>Brooklyn large park.</brief_description>
        <description>Brooklyn large park.</description>
        <features>
          <feature_name>Basketball</feature_name>
          <feature_name>Football</feature_name>
          <feature_name>Playground</feature_name>
          <feature_name>Soccer</feature_name>
          <feature_name>Sprinklers</feature_name>
          <feature_name>Tennis</feature_name>
        </features>
        <address>N/A</address>
        <additional_address_information>Nassau Avenue, Bayard, Leonard and North 12th Streets</additional_address_information>
        <borough>BROOKLYN</borough>
        <city>BROOKLYN</city>
        <state>NY</state>
        <zipcode>11211</zipcode>
        <displayed_hours>Daily: 6:00 AM - 1:00 AM; unless other hours are posted</displayed_hours>
        <lat/>
        <long/>
        <eligibility_information/>
      </facility>
    </facilities>

</tab> <tab title="JSON">

    [
    {
        "id":"20040329-052C82FA-81F5-11D8-ACEF-DCA5D018311B",
        "facility_name":"Mccarren Park",
        "expiration":"12-31-2099T00:00:00Z",
        "type":"Park",
        "brief_description":"Brooklyn large park.",
        "description":"Brooklyn large park.",
        "features":[
                {"feature_name":"Basketball"},
                {"feature_name":"Football"},
                {"feature_name":"Playground"}   ,
                {"feature_name":"Soccer"}   ,
                {"feature_name":"Sprinklers"},
                {"feature_name":"Tennis"}
        ],
        "address":"N/A",
        "additional_address_information":"Nassau Avenue, Bayard, Leonard and North 12th Streets",
        "borough":"BROOKLYN",
        "city":"BROOKLYN",
        "state":"NY",
        "zipcode":"11211",
        "displayed_hours":"Daily: 6:00 AM - 1:00 AM; unless other hours are posted",
        "lat":"",
        "long":"",
        "eligibility_information":""
    }
    ]

</tab> </tabs>

Frequently Asked Questions
==========================

Frequently Asked Questions (FAQ) are questions (with their corresponding answers) that are posted as part of 311 online.

The FAQ functionality consists of two methods. The first method, “Get Frequently Asked Questions List”, retrieves a list of FAQs when invoked. The second method, “Get Frequently Asked Question”, retrieves detailed information about a specific FAQ when invoked.

Get Frequently Asked Questions List
-----------------------------------

This method retrieves a list of links to all FAQs and a brief description of each question. This method takes a category or a type as an optional input. If a category is provided, the list of Services returned will be restricted such that only FAQs which belong to that category will be included in the response.

### URL

<http://><content_api_root>/web_faqs/<category>.<content_type>

#### Sample URLs

-   <http://www.nyc.gov/portal/apps/311_contentapi/web_faqs/all.xml>
-   <http://www.nyc.gov/portal/apps/311_contentapi/web_faqs/all.json>
-   <http://www.nyc.gov/portal/apps/311_contentapi/web_faqs/Transportation,%20Streets%20and%20Sidewalks.xml>
-   <http://www.nyc.gov/portal/apps/311_contentapi/faqs/web.xml>

### Inputs

-   category (/type) – a category or type for a FAQ. If a category is supplied then the list of FAQs returned will be restricted to FAQs belonging to that category. The following categories are supported:

| Category                               | URL Encoded Value                                |
|----------------------------------------|--------------------------------------------------|
| Transportation, Streets, and Sidewalks | Transportation%2C%20Streets%2C%20and%20Sidewalks |
| Environment and Sanitation             | Environment%20and%20Sanitation                   |
| Property, Buildings, and Homes         | Property%2C%20Buildings%2C%20and%20Homes         |
| Education and Employment               | Education%20and%20Employment                     |
| Business and Finance                   | Business%20and%20Finance                         |
| Social Services                        | Social%20Services                                |
| Health and Medicine                    | Health%20and%20Medicine                          |
| Public Safety and Law                  | Public%20Safety%20and%20Law                      |
| Government and Civil Services          | Government%20and%20Civil%20Services              |

The following types are supported:

| Type     | URL Encoded Value | Description                                                                                                                                                                                                                                                |
|----------|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| All FAQs | all               | Returns a list of all available FAQs                                                                                                                                                                                                                       |
| Top FAQs | web               | FAQs curated by the 311 Content Team to be promoted as “Top FAQs”. Please note that the URL path for this method is currently inconsistent with the rest of the FAQ methods. Use <http://><content_api_root>/faqs/web.<content_type> until further notice. |

### Response Structure

#### Field Descriptions

-   id – the unique identifier of the FAQ record
-   question – name of the FAQ record
-   expiration – the date the FAQ record expires. Expiration will occur at 12:00 AM of the date specified.

<tabs> <tab title="XML">

    <faqs>
      <faq>
        <id>20120917-8BA27FD8-00DB-11E2-AC9C-EF5AFBC474DE</id>
        <question>Can I smoke in the park?</question>
        <expiration>2011-12-31T23:59:59Z</expiration>
      </faq>
    </faqs>

</tab> <tab title="JSON">

    [
      {
        "id":"20120917-8BA27FD8-00DB-11E2-AC9C-EF5AFBC474DE",
        "question":"Can I smoke in the park?",
        "expiration":"2011-12-31T23:59:59Z",
      }
    ]

</tab> </tabs>

Get FAQ
-------

This method retrieves detailed information about the FAQ requested. FAQs are specified using the Id of the FAQ.

### URL

<http://><content_api_root>/web_faqs/<faq_id>.<content_type>

#### Sample URLs

-   <http://www.nyc.gov/portal/apps/311_contentapi/web_faqs/20120917-8BA27FD8-00DB-11E2-AC9C-EF5AFBC474DE.xml>
-   <http://www.nyc.gov/portal/apps/311_contentapi/web_faqs/20120917-8BA27FD8-00DB-11E2-AC9C-EF5AFBC474DE.json>

### Inputs

-   faq_id – the Id of the FAQ record being requested.

### Response Structure

#### Field Descriptions

-   id – the unique identifier of the FAQ record
-   question – the question / name of the FAQ record
-   expiration – the date the FAQ expires. Expiration will occur at 12:00 AM of the date specified.
-   categories – a list of taxonomy categories that the FAQ belongs to
-   url – the URL that points to the FAQ on 311 Online
-   answer – the response to the question
-   answer_html – the response to the question in encoded HTML. This is typically used to provide links to additional relevant content outside of the 311 inquiry API.
-   services – a list of services which are related to this FAQ. Developers should check the nested service expiration date to ensure the each returned service is currently valid

<tabs> <tab title="XML">

    <faqs>
      <faq>
        <id>20120917-8BA27FD8-00DB-11E2-AC9C-EF5AFBC474DE</id>
        <question>Can I smoke in the park?</question>
        <expiration>12-31-2099T00:00:00Z</expiration>
        <url>http://www.nyc.gov/apps/311/allFaqs.htm?requestType=recentFaq&faqId=20120917-8BA27FD8-00DB-11E2-AC9C-EF5AFBC474DE</url>
        <answer>No, smoking is not allowed in parks, playgrounds, beaches, boardwalks, pools, golf courses, sports stadium grounds, or pedestrian plazas. If you break the law, you could get a $50 ticket.</answer>
        <answer_html>No, <a href="http://www.nycgovparks.org/sub_about/smoke_free_parks_and_beaches.html">smoking is not allowed</a> in parks, playgrounds, beaches, boardwalks, pools, golf courses, sports stadium grounds, or pedestrian plazas. If you break the law, you could get a $50 ticket.</answer_html>
        <categories>
          <category_name>Culture and Recreation</category_name>
        </categories>
        <services>
          <service>
            <id>20040330-DFA1E1B0-82B2-11D8-AE86-DCA5D018311B</id>
            <service_name>Find a Park</service_name>
            <expiration>12-31-2099T00:00:00Z</expiration>
          </service>
          <service>
            <id>20040923-BC872322-0DA7-11D9-8816-831DC6174F8A</id>
            <service_name>Violation of Park Rules</service_name>
            <expiration>12-31-2099T00:00:00Z</expiration>
          </service>
        </services>
      </faq>
    </faqs>

</tab> <tab title="JSON">

    [{
        "id":"20120917-8BA27FD8-00DB-11E2-AC9C-EF5AFBC474DE",
        "question":"Can I smoke in the park?",
        "expiration":"12-31-2099T00:00:00Z",
        "url":"http://www.nyc.gov/apps/311/allFaqs.htm?requestType=recentFaq&faqId=20120917-8BA27FD8-00DB-11E2-AC9C-EF5AFBC474DE",
        "answer":"No, smoking is not allowed in parks, playgrounds, beaches, boardwalks, pools, golf courses, sports stadium grounds, or pedestrian plazas. If you break the law, you could get a $50 ticket.",
        "answer_html":"No, <a href=\\\"http:\\\/\\\/www.nycgovparks.org\\\/sub_about\\\/smoke_free_parks_and_beaches.html\\\">smoking is not allowed<\\\/a> in parks, playgrounds, beaches, boardwalks, pools, golf courses, sports stadium grounds, or pedestrian plazas. If you break the law, you could get a $50 ticket.",
        "categories":[
                    {"category_name":"Culture and Recreation"}
        ],
        "services":[
            {
                 "id":"20040330-DFA1E1B0-82B2-11D8-AE86-DCA5D018311B",
                "service_name":"Find a Park",
                "expiration":"12-31-2099T00:00:00Z"
            },
            {
                "id":"20040923-BC872322-0DA7-11D9-8816-831DC6174F8A",
                "service_name":"Violation of Park Rules",
                "expiration":"12-31-2099T00:00:00Z"
            }
        ]
    }]

</tab> </tabs>

311 Today
=========

The 311 Today feed provides daily status messages regarding Public Schools, Alternate Side Parking, and Garbage/Recycling pick up. Important City announcements based on current events may also be provided through this feed.

311 Today feed is implemented in RSS format. There is no parameter required when the feed is requested.

311 Today Feed
--------------

This method retrieves an RSS feed that contains a total of 39 days of 311 Today data (the current day, plus 7 days in the past, and 31 days in the future). No parameter is required as an input. Two extensions modules are used on top of the default RSS format: Content (content:encoded) and Dublic Core (dc:coverage).

### URL

<http://><content_api_root>/311TodayContent.rss

#### Sample URLs

-   <http://www.nyc.gov/apps/311/311Today.rss>

### Inputs

N/A

### Response Structure

#### Field Descriptions

**Root level**

-   rss – the beginning of the RSS feed
-   channel – the beginning of 311 Today RSS feed. There will only be 1 channel for this feed.
-   title – name of the feed. It will always be NYC 311 Today RSS feed
-   link – link back to the 311 Online homepage
-   description – description of the feed

**Item level**

-   item – tag that wraps around the date’s content
-   title – the title for the date’s content
-   pubDate – publishing date for this story. Note that this is not the date for the content. This is the date the information is being pushed out.
-   guid – unique ID for the date’s content.
-   <content:encoded> – HTML code wrapped for the detail of the content around the CDATA tag. This data is expected to rendered as HTML code.
-   dc:coverage – describes the event date of the content. It is in yyyy-MM-dd format.

<tabs> <tab title="XML">

    <rss xmlns:content="http://purl.org/rss/1.0/modules/content/" xmlns:dc="http://purl.org/dc/elements/1.1/" version="2.0">
      <channel>
        <title>NYC 311 Today RSS feed</title>
        <link>http://www.nyc.gov/apps/311/</link>
        <description>NYC 311 Today</description>
        <item>
          <title>NYC 311 Today for Friday, May 20, 2011</title>
          <pubDate>Fri, 27 May 2011 17:34:48 GMT</pubDate>
          <guid isPermaLink="false">20110520</guid>
          <content:encoded><![CDATA[<P>Public schools are open.<br />Alternate side parking is in effect.<br /> Garbage/Recycling pick-up is suspended.Edited1<br /></P> <P><P>This was the status at the end of the day. It does not reflect earlier updates.</P></P>]]></content:encoded>
          <dc:coverage>2011-05-20</dc:coverage>
        </item>
        <item>
          <title>NYC 311 Today for Saturday, May 21, 2011</title>
          <pubDate>Fri, 27 May 2011 17:34:48 GMT</pubDate>
          <guid isPermaLink="false">20110521</guid>
          <content:encoded><![CDATA[P>This was the status at the end of the day. It does not reflect earlier updates.</P></P>]]></content:encoded>
          <dc:coverage>2011-05-21</dc:coverage>
        </item>
    ...
    ...
      </channel>
    </rss>

</tab> </tabs>
