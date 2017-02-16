---
title: GeoReport v2 Resources
permalink: /GeoReport_v2/Resources/
---

Open source developer resources for the [GeoReport v2](/GeoReport_v2 "wikilink") specification.

#### Server Software

Server applications provide an API endpoint and can receive and manage reports.

-   [uReport Open311 Server](https://github.com/City-of-Bloomington/uReport). PHP-based Open311 Server & CRM by Bloomington
-   [open311server](https://github.com/andrewsage/open311server) - Ruby Sinatra Open311 Server
-   [GeoReport v2 Server](https://github.com/miamidade/georeport-server) - Python-based middleware/server by Miami-Dade County. There's also a [Java implementation in development](https://github.com/miamidade/open311)
-   [Mark-a-Spot Drupal Distribution](https://github.com/markaspot/mark-a-spot). There's also [Integration](https://github.com/markaspot/mas-open311) for the older standalone [Mark-a-Spot CakePHP](https://github.com/markaspot/Mark-a-Spot-1.6-CakePHP) code.
-   [Accela Open311](https://github.com/Accela-Inc/accela-open311) - Node.js Server
-   [Open311 Simple CRM](https://github.com/GSA/open311-simple-crm/) - Very basic CRM based on FMS-Endpoint
-   [FMS-Endpoint Open311 API for FixMyStreet](https://github.com/mysociety/fms-endpoint) - "fms-endpoint" using Codeigniter PHP - by MySociety
-   [FixMyStreet integration](https://github.com/search?type=Everything&language>=&q=open311+repo%3Amysociety%2Ffixmystreet&repo=&langOverride=&x=0&y=0&start_value=1). See [FixMyStreet.com/open311](http://fixmystreet.com/open311) and example of support within a city: [Southampton UK](http://southampton.fixmystreet.com/open311)
-   [Open311 Plugin for Ushahidi](https://github.com/mapmeld/Open311-Plugin-for-Ushahidi) (in development. [More background on the Ushahidi wiki](http://wiki.ushahidi.com/pages/viewpage.action?pageId=4260162))
-   [Open311 on Joget](https://github.com/codeforamerica/open311-on-joget). See [Blog post](http://codeforamerica.org/2011/09/09/ashishs-cfa-summer-starting-the-open311-center/). (in development).
-   See also: search results on GitHub for [Open311 or GeoReport](https://github.com/search?o=desc&q=open311+OR+georeport&ref=searchresults&s=updated&type=Repositories) 

#### Client Applications

Software that interacts with an Open311 server by connecting to an API.

-   [GeoReporter Open311 Android app](https://github.com/City-of-Bloomington/open311-android) - download [GeoReporter from Google play](https://play.google.com/store/apps/details?id=gov.in.bloomington.georeporter&hl=en)
-   [GeoReporter Open311 iPhone app](https://github.com/City-of-Bloomington/open311-mobile) - download [GeoReporter from the Apple App Store](http://itunes.apple.com/us/app/georeporter/id487304759)
-   [Open311 Wordpress Plugin](https://github.com/GSA/wp-open311) (still early development)
-   [Open311 Proxy](https://github.com/City-of-Bloomington/open311-proxy) - a PHP/HTML/javascript client that doesn't expose API keys
-   [Open311 Facebook app](https://github.com/codeforamerica/open311_facebook)
-   [Open311 Plugin for Ushahidi](https://github.com/mapmeld/Open311-Plugin-for-Ushahidi) - can reroute issues from Ushahidi to an external Open311 endpoint.
-   [OpenBlock](http://openblockproject.org) is not an Open311 client per se, but can consume and display Open311 reports on a map; [see Boston demo](http://demo.openblockproject.org/open311-service-requests/)

##### Dashboards & Data Viz
-   [chicagoworksforyou.com](http://chicagoworksforyou.com/)[forked](https://github.com/smartchicago/311-fm-webapp) from [311.fm](https://github.com/codeforamerica/311fm)
-   [Open311 Data Analysis Proxy](https://github.com/codeforamerica/311-fm-data) used for 311.fm
-   [Open311 Dashboard](https://github.com/codeforamerica/open311dashboard) See the [Blog post](http://codeforamerica.org/2011/08/31/chriss-cfa-summer-preview-the-open311-dashboard/) (in development)
- [https://hackadashery.github.io](https://hackadashery.github.io/?p=explore) by [Code for Philly](https://codeforphilly.org/projects/philly_311_dashboard)

###### Deprecated Projects 
- [The Daily Brief](http://dailybrief.311labs.org/) - See live at [dailybrief.311labs.org](http://dailybrief.311labs.org/) 
- [311.fm](http://www.311.fm/) - Code still available at [311-fm-webapp](https://github.com/smartchicago/311-fm-webapp) 

See also open source libraries for [Visualizations](/Visualizations "wikilink")

#### Client Libraries (API Wrappers)

Client libraries make it easier to build client applications that work with the spec.

-   [PHP](https://github.com/codeforamerica/open311_php) by Ronaldo Barbachano at Code for America
-   [Python](https://github.com/codeforamerica/three) by Zach Williams at Code for America
-   [Ruby Gem](http://rubygems.org/gems/open311) by Code for America labs et al (see it on [GitHub](https://github.com/codeforamerica/open311))
-   [Node.js](https://github.com/codeforamerica/node-open311) by Mark Headd and Ben Sheldon
-   [C\#](https://github.com/mheadd/csharp-open311) by Mark Headd
-   [Clojure](https://github.com/ryanbriones/open311-clj) by Ryan Briones
-   [Java](https://github.com/codeforamerica/open311_java) by Santiago Munín at Code for America

#### Test Suites

Test suites are used to verify that a server is compliant with the specification.

-   <https://github.com/seeclickfix/open311-validator/> (ruby based, initial release Nov 2011)
-   <http://github.com/open311/open311-validator-py> (python based, not up to date)
-   [GeoReporter Client](http://itunes.apple.com/us/app/georeporter/id487304759) can be used to test GeoReport v2 endpoints.
-   <https://github.com/ryanbriones/open311-api-tests>

#### Products & Services

See also [GeoReport v2 Support](/GeoReport_v2/Support "wikilink") for products and services.
