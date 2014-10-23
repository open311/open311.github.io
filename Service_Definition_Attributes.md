---
title: Service_Definition_Attributes
permalink: /Service_Definition_Attributes/
---

Problem Statement
-----------------

<http://developer.open311.org/ticket/30>

It's generally seen as a best practice to wrap an array or listing of a data type in a container. This is done for the output of values in Get Service Definitions and it's done for the output of services in Get Services, but it's not done for attributes in Get Service Definitions. So not only is this not following a best practice, it's also internally inconsistent.

Resources
---------

Below are snippets of the current data structures and proposed data structures. Eric Carson has also posted examples of this data along with XSL transformations with Ruby for JSON using the Parker convention at: <https://github.com/connectedbits/open311_xml2json#readme>

There's also a webform that can be used to experiment with arbitrary XML to JSON conversion using the Parker convention at <http://sandbox.georeport.org/tools/parkerjson/>

Current XML
-----------

The hierarchy is currently as such:

    <?xml version="1.0" encoding="utf-8"?>
    <service_definition>
        <service_code>DMV66</service_code>
        <attribute>
            <variable>true</variable>
            <code>WHISHETN</code>
            <datatype>singlevaluelist</datatype>
            <required>true</required>
            <datatype_description></datatype_description>
            <order>1</order>
            <description>What is the make of the vehicle?</description>
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
        <attribute>
            <variable>true</variable>
            <code>YATCHK</code>
            <datatype>singlevaluelist</datatype>
            <required>false</required>
            <datatype_description></datatype_description>
            <order>1</order>
            <description>What is the color of the vehicle?</description>
            <values>
                <value>
                    <key>123</key>
                    <name>Blue</name>
                </value>
                <value>
                    <key>124</key>
                    <name>Red</name>
                </value>
            </values>
        </attribute>
    </service_definition>

XML with Fix
------------

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
                <description>What is the make of the vehicle?</description>
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
            <attribute>
                <variable>true</variable>
                <code>YATCHK</code>
                <datatype>singlevaluelist</datatype>
                <required>false</required>
                <datatype_description></datatype_description>
                <order>1</order>
                <description>What is the color of the vehicle?</description>
                <values>
                    <value>
                        <key>123</key>
                        <name>Blue</name>
                    </value>
                    <value>
                        <key>124</key>
                        <name>Red</name>
                    </value>
                </values>
            </attribute>
        </attributes>
    </service_definition>

Current XML as Parker JSON
--------------------------

    {
      "service_definition":{
        "service_code":"DMV66",
        "attribute":{
          "variable":true,
          "code":"WHISHETN",
          "datatype":"singlevaluelist",
          "required":true,
          "datatype_description":null,
          "order":1,
          "description":"What is the make of the vehicle?",
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
        },
        "attribute":{
          "variable":true,
          "code":"YATCHK",
          "datatype":"singlevaluelist",
          "required":false,
          "datatype_description":null,
          "order":1,
          "description":"What is the color of the vehicle?",
          "values":[
            {
              "key":123,
              "name":"Blue"
            },
            {
              "key":124,
              "name":"Red"
            }
          ]
        }
      }
    }

Fixed XML as Parker JSON
------------------------

    {
      "service_definition":{
        "service_code":"DMV66",
        "attributes":[
          {
            "variable":true,
            "code":"WHISHETN",
            "datatype":"singlevaluelist",
            "required":true,
            "datatype_description":null,
            "order":1,
            "description":"What is the make of the vehicle?",
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
          },
          {
            "variable":true,
            "code":"YATCHK",
            "datatype":"singlevaluelist",
            "required":false,
            "datatype_description":null,
            "order":1,
            "description":"What is the color of the vehicle?",
            "values":[
              {
                "key":123,
                "name":"Blue"
              },
              {
                "key":124,
                "name":"Red"
              }
            ]
          }
        ]
      }
    }