---
title: Parker_vs_Spark
permalink: /Parker_vs_Spark/
---

This is a comparison of the Parker and Spark convention for XML to JSON mapping. The example uses the XML for [Service Discovery](/Service_Discovery "wikilink"):

In addition to the differences noted on the [JSON & XML Conversion](http://wiki.open311.org/JSON_and_XML_Conversion#The_Spark_Convention) page, the XSL being used to convert to the Parker convention does not seem to be stripping the root element even though that is supposed to be one of the properties of Parker. The Spark example does do this.

The easiest way to spot the key difference between Parker and Spark is to see how the <formats> and child <format> elements are handled in each example. The Parker example demonstrates an internal inconsistency based on the number of <format> elements while it is consistent with the Spark example regardless of how many <format> elements there are.

<tabs> <tab title="XML">

    <?xml version="1.0" encoding="UTF-8"?>
    <discovery>
        <changeset>2011-02-03 14:18</changeset>
        <contact>You can email or call for assistance api@mycity.org +1 (555) 555-5555</contact>
        <key_service>You can request a key here: http://api.mycity.gov/api_key/request</key_service>
        <endpoints>
            <endpoint>
                <specification>http://wiki.open311.org/GeoReport_v2.1</specification>
                <url>http://open311.mycity.gov/v2_1</url>
                <changeset>2010-11-23 09:01</changeset>
                <type>production</type>
                <formats>
                    <format>text/xml</format>
                </formats>
            </endpoint>
            <endpoint>
                <specification>http://wiki.open311.org/GeoReport_v2.1</specification>
                <url>http://open311.mycity.gov/test/v2_1</url>
                <changeset>2010-10-02 09:01</changeset>
                <type>test</type>
                <formats>
                    <format>text/xml</format>
                    <format>text/json</format>
                    <format>text/html</format>
                </formats>
            </endpoint>
            <endpoint>
                <specification>http://wiki.open311.org/GeoReport_v3</specification>
                <url>http://open311.mycity.gov/v3</url>
                <changeset>2011-02-03 14:18</changeset>
                <type>test</type>
            </endpoint>
        </endpoints>
    </discovery>

</tab> <tab title="Parker JSON">

    {
      "discovery":{
        "changeset":"2011-02-03 14:18",
        "contact":"You can email or call for assistance api@mycity.org +1 (555) 555-5555",
        "key_service":"You can request a key here: http://api.mycity.gov/api_key/request",
        "endpoints":[
          {
            "specification":"http://wiki.open311.org/GeoReport_v2.1",
            "url":"http://open311.mycity.gov/v2_1",
            "changeset":"2010-11-23 09:01",
            "type":"production",
            "formats":{
              "format":"text/xml"
            }
          },
          {
            "specification":"http://wiki.open311.org/GeoReport_v2.1",
            "url":"http://open311.mycity.gov/test/v2_1",
            "changeset":"2010-10-02 09:01",
            "type":"test",
            "formats":[
              "text/xml",
              "text/json",
              "text/html"
            ]
          },
          {
            "specification":"http://wiki.open311.org/GeoReport_v3",
            "url":"http://open311.mycity.gov/v3",
            "changeset":"2011-02-03 14:18",
            "type":"test"
          }
        ]
      }
    }

</tab> <tab title="Spark JSON">

    {
      "changeset":"2011-02-03 14:18",
      "contact":"You can email or call for assistance api@mycity.org +1 (555) 555-5555",
      "key_service":"You can request a key here: http://api.mycity.gov/api_key/request",
      "endpoints":[
        {
          "specification":"http://wiki.open311.org/GeoReport_v2.1",
          "url":"http://open311.mycity.gov/v2_1",
          "changeset":"2010-11-23 09:01",
          "type":"production",
          "formats":[
            "text/xml"
          ]
        },
        {
          "specification":"http://wiki.open311.org/GeoReport_v2.1",
          "url":"http://open311.mycity.gov/test/v2_1",
          "changeset":"2010-10-02 09:01",
          "type":"test",
          "formats":[
            "text/xml",
            "text/json",
            "text/html"
          ]
        },
        {
          "specification":"http://wiki.open311.org/GeoReport_v3",
          "url":"http://open311.mycity.gov/v3",
          "changeset":"2011-02-03 14:18",
          "type":"test"
        }
      ]
    }

</tab> </tabs>
