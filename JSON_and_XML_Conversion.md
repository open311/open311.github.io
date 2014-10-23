---
title: JSON_and_XML_Conversion
permalink: /JSON_and_XML_Conversion/
---

XML to JSON Conventions
=======================

Not everything in XML can be represented in JSON. The main reason for this is because XML allows inline metadata using tag attributes and there is no standard way of representing this metadata in JSON. Below you will find a reference point for an XML representation along with descriptions and JSON representations for each of these conventions.

### XML Representation

    <?xml-stylesheet type="text/xsl" href="xml2json.xslt"?>
    <reports ns="http://www.w3.org/2005/Atom"
           xmlns:georss="http://www.georss.org/georss">

        <entry>
            <id>tag:open311.sfgov.org,2010-04-15:/dev/V1/reports/637619.xml</id>
            <title>A large tree branch is blocking the road</title>
            <updated>2010-04-13T18:30:02-05:00</updated>
            <link rel="self" href="http://open311.sfgov.org/dev/V1/reports/637619.xml"/>
            <author><name>John Doe</name></author>

            <georss:point>40.7111 -73.9565</georss:point>

            <category label="Damaged tree" term="tree-damage" scheme="https://open311.sfgov.org/dev/V1/categories/006.xml">006</category>

            <content type="xml" ns="http://open311.org/spec/georeport-v1">
                <report_id>637619</report_id>
                <address>1600 Market St, San Francisco, CA 94103</address>
                <description>A large tree branch is blocking the road</description>
                <status>created</status>
                <status_notes />
                <policy>The City will inspect and require the responsible party to correct within 24 hours and/or issue a Correction Notice or Notice of Violation of the Public Works Code</policy>
            </content>

        </entry>

        <entry>
            <id>tag:open311.sfgov.org,2010-04-15:/dev/V1/reports/637620.xml</id>
            <title>A large tree branch is blocking the road</title>
            <updated>2010-04-13T18:30:02-05:00</updated>
            <link rel="self" href="http://open311.sfgov.org/dev/V1/reports/637620.xml"/>
            <author><name>John Doe</name></author>

            <georss:point>40.7111 -73.9565</georss:point>

            <category label="Damaged tree" term="tree-damage" scheme="https://open311.sfgov.org/dev/V1/categories/006.xml">006</category>

            <content type="xml" ns="http://open311.org/spec/georeport-v1">
                <report_id>637620</report_id>
                <address>56 Market St, San Francisco, CA 94103</address>
                <description>A large tree branch is blocking the road</description>
                <status>created</status>
                <status_notes />
                <policy>The City will inspect and require the responsible party to correct within 24 hours and/or issue a Correction Notice or Notice of Violation of the Public Works Code</policy>
            </content>

        </entry>

        <entry>
            <id>tag:open311.sfgov.org,2010-04-15:/dev/V1/reports/637621.xml</id>
            <title>A large tree branch is blocking the road</title>
            <updated>2010-04-13T18:30:02-05:00</updated>
            <link rel="self" href="http://open311.sfgov.org/dev/V1/reports/637621.xml"/>
            <author><name>John Doe</name></author>

            <georss:point>40.7111 -73.9565</georss:point>

            <category label="Damaged tree" term="tree-damage" scheme="https://open311.sfgov.org/dev/V1/categories/006.xml">006</category>

            <content type="xml" ns="http://open311.org/spec/georeport-v1">
                <report_id>637621</report_id>
                <address>1800 Market St, San Francisco, CA 94103</address>
                <description>A large tree branch is blocking the road</description>
                <status>created</status>
                <status_notes />
                <policy>The City will inspect and require the responsible party to correct within 24 hours and/or issue a Correction Notice or Notice of Violation of the Public Works Code</policy>
            </content>

        </entry>

    </reports>

The Parker Convention
---------------------

The Parker convention is lossy, it simply ignores XML attributes. The advantage is that it generates much leaner and cleaner JSON. However, there are a few places where XML attributes are used in the core Atom schema for a report: metadata about the associated category as well as the URI and media type for associated media included in the <link> tags. The metadata for categories is probably not essential as long as the category_id is included (the category metadata is just denormalization).

### References

-   **Documentation**: <http://code.google.com/p/xml2json-xslt/wiki/TransformingRules>
-   **XSLT Library**: <http://xml2json-xslt.googlecode.com/files/xml2json-xslt-r3.zip>

### JSON Representation

    {
      "reports":[
        {
          "id":"tag:open311.sfgov.org,2010-04-15:/dev/V1/reports/637619.xml",
          "title":"A large tree branch is blocking the road",
          "updated":"2010-04-13T18:30:02-05:00",
          "link":null,
          "author":{
            "name":"John Doe"
          },
          "georss:point":"40.7111 -73.9565",
          "category":006,
          "content":{
            "report_id":637619,
            "address":"1600 Market St, San Francisco, CA 94103",
            "description":"A large tree branch is blocking the road",
            "status":"created",
            "status_notes":null,
            "policy":"The City will inspect and require the responsible party to correct within 24 hours and/or issue a Correction Notice or Notice of Violation of the Public Works Code"
          }
        },
        {
          "id":"tag:open311.sfgov.org,2010-04-15:/dev/V1/reports/637620.xml",
          "title":"A large tree branch is blocking the road",
          "updated":"2010-04-13T18:30:02-05:00",
          "link":null,
          "author":{
            "name":"John Doe"
          },
          "georss:point":"40.7111 -73.9565",
          "category":006,
          "content":{
            "report_id":637620,
            "address":"56 Market St, San Francisco, CA 94103",
            "description":"A large tree branch is blocking the road",
            "status":"created",
            "status_notes":null,
            "policy":"The City will inspect and require the responsible party to correct within 24 hours and/or issue a Correction Notice or Notice of Violation of the Public Works Code"
          }
        },
        {
          "id":"tag:open311.sfgov.org,2010-04-15:/dev/V1/reports/637621.xml",
          "title":"A large tree branch is blocking the road",
          "updated":"2010-04-13T18:30:02-05:00",
          "link":null,
          "author":{
            "name":"John Doe"
          },
          "georss:point":"40.7111 -73.9565",
          "category":006,
          "content":{
            "report_id":637621,
            "address":"1800 Market St, San Francisco, CA 94103",
            "description":"A large tree branch is blocking the road",
            "status":"created",
            "status_notes":null,
            "policy":"The City will inspect and require the responsible party to correct within 24 hours and/or issue a Correction Notice or Notice of Violation of the Public Works Code"
          }
        }
      ]
    }

The Spark Convention
--------------------

The Spark convention is a slight modification of the Parker convention. It treats nested child elements as demarcating the beginning of an array if there is only one kind of child (a repeating element). This means that it assumes the XML will follow a pattern where there's an explicit container for child elements that should be an array. Parker almost does this, but if there is only one child in the container, it doesn't think it should be an array. The Spark convention ensures that child is always an array even if there's only one of them. This helps create more XML-like consistency for the JSON structure of child elements when the number of child elements is inconsistent in XML.

### Comparison

Seeing a comparison of Parker and Spark may be easier to understand: [Parker vs Spark](/Parker_vs_Spark "wikilink")

### References

-   **Parker Documentation (*not Spark*)**: <http://code.google.com/p/xml2json-xslt/wiki/TransformingRules>
-   **Spark XML to JSON Converter**: <http://dropbox.ashlock.us/open311/json-xml/xml-tools/xml2json_spark.php>
-   **XSL**: <http://dropbox.ashlock.us/open311/json-xml/xml-tools/xml2json_spark.xsl>

### JSON Representation

    [
      {
        "id":"tag:open311.sfgov.org,2010-04-15:/dev/V1/reports/637619.xml",
        "title":"A large tree branch is blocking the road",
        "updated":"2010-04-13T18:30:02-05:00",
        "link":null,
        "author":[
          "John Doe"
        ],
        "georss:point":"40.7111 -73.9565",
        "category":006,
        "content":{
          "report_id":637619,
          "address":"1600 Market St, San Francisco, CA 94103",
          "description":"A large tree branch is blocking the road",
          "status":"created",
          "status_notes":null,
          "policy":"The City will inspect and require the responsible party to correct within 24 hours and/or issue a Correction Notice or Notice of Violation of the Public Works Code"
        }
      },
      {
        "id":"tag:open311.sfgov.org,2010-04-15:/dev/V1/reports/637620.xml",
        "title":"A large tree branch is blocking the road",
        "updated":"2010-04-13T18:30:02-05:00",
        "link":null,
        "author":[
          "John Doe"
        ],
        "georss:point":"40.7111 -73.9565",
        "category":006,
        "content":{
          "report_id":637620,
          "address":"56 Market St, San Francisco, CA 94103",
          "description":"A large tree branch is blocking the road",
          "status":"created",
          "status_notes":null,
          "policy":"The City will inspect and require the responsible party to correct within 24 hours and/or issue a Correction Notice or Notice of Violation of the Public Works Code"
        }
      },
      {
        "id":"tag:open311.sfgov.org,2010-04-15:/dev/V1/reports/637621.xml",
        "title":"A large tree branch is blocking the road",
        "updated":"2010-04-13T18:30:02-05:00",
        "link":null,
        "author":[
          "John Doe"
        ],
        "georss:point":"40.7111 -73.9565",
        "category":006,
        "content":{
          "report_id":637621,
          "address":"1800 Market St, San Francisco, CA 94103",
          "description":"A large tree branch is blocking the road",
          "status":"created",
          "status_notes":null,
          "policy":"The City will inspect and require the responsible party to correct within 24 hours and/or issue a Correction Notice or Notice of Violation of the Public Works Code"
        }
      }
    ]

The Badgerfish Convention
-------------------------

The Badgerfish convention is a fairly comprehensive JSON representation of XML in the sense that it accommodates element attributes and namespaces. Unfortunately, this also adds a bit of overhead to the JSON syntax. Each element is given an array for attributes and values. Attribute names are preceded with an @ symbol while values are represented with a $ symbol.

The most comprehensive Badgerfish mapping I've seen is from Cau Guanabara ([demo](http://dropbox.ashlock.us/open311/json-xml/)):

-   Element names become object properties
-   Text content of elements goes in the $ property of an object.
-   Nested elements become nested properties
-   Multiple elements at the same level become array elements.
-   Attributes go in properties whose names begin with @.
-   Active namespaces for an element go in the element's @xmlns property.
-   The default namespace URI goes in @xmlns.$.
-   Other namespaces go in other properties of @xmlns.
-   Elements with namespace prefixes become object properties, too.
-   The @xmlns property goes only in object relative to the element where namespace was declared.
-   Text fragments in mixed contents (elements and text) goes in properties named $1, $2, etc.
-   Comment elements , like the text fragments, go in properties named !1, !2, etc.
-   CDATA sections go in properties named \#1, \#2, etc.

### References

-   **Documentation**: <http://www.sklar.com/badgerfish/>
-   **Bidirectional Javascript library** by Cau Guanabara: <http://dropbox.ashlock.us/open311/json-xml/>
-   **PHP Library**: <http://www.sklar.com/badgerfish/file.php?format=text&path=lib/BadgerFish.php> (Depends on PHP [Services JSON](http://pear.php.net/pepr/pepr-proposal-show.php?id=198) library)
-   **Ruby Library**: This can be achieved by combining [Cobra vs Mongoose](http://cobravsmongoose.rubyforge.org/) with the [Ruby JSON Library](http://json.rubyforge.org/).
-   **Lua Library**: <http://dev.alt.textdrive.com/browser/HTTP/XML.lua>
-   Something similar in Python: <http://www.smullyan.org/files/pesterfish.py>

### JSON Representation

This example uses Cau Guanabara's more comprehensive version of Badgerfish.

                {
                    "reports": {
                        "@xmlns": {
                            "$": "http://www.w3.org/2005/Atom",
                            "georss": "http://www.georss.org/georss"
                        },
                        "entry": [{
                            "id": {
                                "$": "tag:open311.sfgov.org,2010-04-15:/dev/V1/reports/637619.xml"
                            },
                            "title": {
                                "$": "A large tree branch is blocking the road"
                            },
                            "updated": {
                                "$": "2010-04-13T18:30:02-05:00"
                            },
                            "link": {
                                "@rel": "self",
                                "@href": "http://open311.sfgov.org/dev/V1/reports/637619.xml"
                            },
                            "author": {
                                "name": {
                                    "$": "John Doe"
                                }
                            },
                            "georss:point": {
                                "$": "40.7111 -73.9565"
                            },
                            "category": {
                                "@label": "Damaged tree",
                                "@term": "tree-damage",
                                "@scheme": "https://open311.sfgov.org/dev/V1/categories/006.xml",
                                "$": 006
                            },
                            "content": {
                                "@type": "xml",
                                "@xmlns": {
                                    "$": "http://open311.org/spec/georeport-v1"
                                },
                                "report_id": {
                                    "$": 637619
                                },
                                "address": {
                                    "$": "1600 Market St, San Francisco, CA 94103"
                                },
                                "description": {
                                    "$": "A large tree branch is blocking the road"
                                },
                                "status": {
                                    "$": "created"
                                },
                                "status_notes": {},
                                "policy": {
                                    "$": "The City will inspect and require the responsible party to correct within 24 hours and/or issue a Correction Notice or Notice of Violation of the Public Works Code"
                                }
                            }
                        },
                        {
                            "id": {
                                "$": "tag:open311.sfgov.org,2010-04-15:/dev/V1/reports/637620.xml"
                            },
                            "title": {
                                "$": "A large tree branch is blocking the road"
                            },
                            "updated": {
                                "$": "2010-04-13T18:30:02-05:00"
                            },
                            "link": {
                                "@rel": "self",
                                "@href": "http://open311.sfgov.org/dev/V1/reports/637620.xml"
                            },
                            "author": {
                                "name": {
                                    "$": "John Doe"
                                }
                            },
                            "georss:point": {
                                "$": "40.7111 -73.9565"
                            },
                            "category": {
                                "@label": "Damaged tree",
                                "@term": "tree-damage",
                                "@scheme": "https://open311.sfgov.org/dev/V1/categories/006.xml",
                                "$": 006
                            },
                            "content": {
                                "@type": "xml",
                                "@xmlns": {
                                    "$": "http://open311.org/spec/georeport-v1"
                                },
                                "report_id": {
                                    "$": 637620
                                },
                                "address": {
                                    "$": "56 Market St, San Francisco, CA 94103"
                                },
                                "description": {
                                    "$": "A large tree branch is blocking the road"
                                },
                                "status": {
                                    "$": "created"
                                },
                                "status_notes": {},
                                "policy": {
                                    "$": "The City will inspect and require the responsible party to correct within 24 hours and/or issue a Correction Notice or Notice of Violation of the Public Works Code"
                                }
                            }
                        },
                        {
                            "id": {
                                "$": "tag:open311.sfgov.org,2010-04-15:/dev/V1/reports/637621.xml"
                            },
                            "title": {
                                "$": "A large tree branch is blocking the road"
                            },
                            "updated": {
                                "$": "2010-04-13T18:30:02-05:00"
                            },
                            "link": {
                                "@rel": "self",
                                "@href": "http://open311.sfgov.org/dev/V1/reports/637621.xml"
                            },
                            "author": {
                                "name": {
                                    "$": "John Doe"
                                }
                            },
                            "georss:point": {
                                "$": "40.7111 -73.9565"
                            },
                            "category": {
                                "@label": "Damaged tree",
                                "@term": "tree-damage",
                                "@scheme": "https://open311.sfgov.org/dev/V1/categories/006.xml",
                                "$": 006
                            },
                            "content": {
                                "@type": "xml",
                                "@xmlns": {
                                    "$": "http://open311.org/spec/georeport-v1"
                                },
                                "report_id": {
                                    "$": 637621
                                },
                                "address": {
                                    "$": "1800 Market St, San Francisco, CA 94103"
                                },
                                "description": {
                                    "$": "A large tree branch is blocking the road"
                                },
                                "status": {
                                    "$": "created"
                                },
                                "status_notes": {},
                                "policy": {
                                    "$": "The City will inspect and require the responsible party to correct within 24 hours and/or issue a Correction Notice or Notice of Violation of the Public Works Code"
                                }
                            }
                        }]
                    }
                }


The GData Convention
--------------------

The Google Data (or GData) Convention is basically the same as Badgerfish except that it drops the @ symbol for attributes and uses $t instead of just $ for values.

### References

-   **Documentation**: <http://code.google.com/apis/gdata/docs/json.html>
-   **Javascript Library** for interacting with GData JSON Objects: <http://code.google.com/apis/gdata/docs/js.html>

... that JS library may currently be the only important use case for the JSON format, unless somebody rolls their own client code and really dislikes XML. As noted at <http://code.google.com/apis/gdata/docs/json.html> , "The Google Data client libraries don't currently support JSON."

### JSON Representation

    ({
        "reports": {
            "entry": [{
                "id": {
                    "$t": "tag:open311.sfgov.org,2010-04-15:\/dev\/V1\/reports\/637619.xml"
                },
                "title": {
                    "$t": "A large tree branch is blocking the road"
                },
                "updated": {
                    "$t": "2010-04-13T18:30:02-05:00"
                },
                "link": {
                    "rel": "self",
                    "href": "http:\/\/open311.sfgov.org\/dev\/V1\/reports\/637619.xml"
                },
                "author": {
                    "name": {
                        "$t": "John Doe"
                    }
                },
                "georss:point": {
                    "$t": "40.7111 -73.9565"
                },
                "category": {
                    "$t": "006",
                    "label": "Damaged tree",
                    "term": "tree-damage",
                    "scheme": "https:\/\/open311.sfgov.org\/dev\/V1\/categories\/006.xml"
                },
                "content": {
                    "report_id": {
                        "$t": "637619"
                    },
                    "address": {
                        "$t": "1600 Market St, San Francisco, CA 94103"
                    },
                    "description": {
                        "$t": "A large tree branch is blocking the road"
                    },
                    "status": {
                        "$t": "created"
                    },
                    "status_notes": [],
                    "policy": {
                        "$t": "The City will inspect and require the responsible party to correct within 24 hours and\/or issue a Correction Notice or Notice of Violation of the Public Works Code"
                    },
                    "type": "xml"
                }
            },
            {
                "id": {
                    "$t": "tag:open311.sfgov.org,2010-04-15:\/dev\/V1\/reports\/637620.xml"
                },
                "title": {
                    "$t": "A large tree branch is blocking the road"
                },
                "updated": {
                    "$t": "2010-04-13T18:30:02-05:00"
                },
                "link": {
                    "rel": "self",
                    "href": "http:\/\/open311.sfgov.org\/dev\/V1\/reports\/637620.xml"
                },
                "author": {
                    "name": {
                        "$t": "John Doe"
                    }
                },
                "georss:point": {
                    "$t": "40.7111 -73.9565"
                },
                "category": {
                    "$t": "006",
                    "label": "Damaged tree",
                    "term": "tree-damage",
                    "scheme": "https:\/\/open311.sfgov.org\/dev\/V1\/categories\/006.xml"
                },
                "content": {
                    "report_id": {
                        "$t": "637620"
                    },
                    "address": {
                        "$t": "56 Market St, San Francisco, CA 94103"
                    },
                    "description": {
                        "$t": "A large tree branch is blocking the road"
                    },
                    "status": {
                        "$t": "created"
                    },
                    "status_notes": [],
                    "policy": {
                        "$t": "The City will inspect and require the responsible party to correct within 24 hours and\/or issue a Correction Notice or Notice of Violation of the Public Works Code"
                    },
                    "type": "xml"
                }
            },
            {
                "id": {
                    "$t": "tag:open311.sfgov.org,2010-04-15:\/dev\/V1\/reports\/637621.xml"
                },
                "title": {
                    "$t": "A large tree branch is blocking the road"
                },
                "updated": {
                    "$t": "2010-04-13T18:30:02-05:00"
                },
                "link": {
                    "rel": "self",
                    "href": "http:\/\/open311.sfgov.org\/dev\/V1\/reports\/637621.xml"
                },
                "author": {
                    "name": {
                        "$t": "John Doe"
                    }
                },
                "georss:point": {
                    "$t": "40.7111 -73.9565"
                },
                "category": {
                    "$t": "006",
                    "label": "Damaged tree",
                    "term": "tree-damage",
                    "scheme": "https:\/\/open311.sfgov.org\/dev\/V1\/categories\/006.xml"
                },
                "content": {
                    "report_id": {
                        "$t": "637621"
                    },
                    "address": {
                        "$t": "1800 Market St, San Francisco, CA 94103"
                    },
                    "description": {
                        "$t": "A large tree branch is blocking the road"
                    },
                    "status": {
                        "$t": "created"
                    },
                    "status_notes": [],
                    "policy": {
                        "$t": "The City will inspect and require the responsible party to correct within 24 hours and\/or issue a Correction Notice or Notice of Violation of the Public Works Code"
                    },
                    "type": "xml"
                }
            }]
        }
    });

The Abdera Convention
---------------------

The Abdera convention is what is used within the Apache Abdera project to show Atom entries using JSON. This convention is sort of a cross between GData and Parker in that it mixes metadata in with regular values unless the attributes are part of foreign markup not specified within Atom. The difference from GData is that it doesn't create a nested array unless it has to represent attributes. Also, if there is both metadata attributes and children of the element, then nested arrays are created for attributes and children values.

### References

-   **Documentation**: <http://www.ibm.com/developerworks/library/x-atom2json.html>
-   **Documentation**: <https://cwiki.apache.org/ABDERA/json-serialization.html>
-   **Apache Abdera (Java)**: <http://abdera.apache.org/>

### JSON Representation

I'm not entirely sure if this is accurate since I did it by hand from inference.

    ({
        "reports": {
            "entry": [{
                "id": "tag:open311.sfgov.org,2010-04-15:\/dev\/V1\/reports\/637619.xml",
                "title": "A large tree branch is blocking the road",
                "updated": "2010-04-13T18:30:02-05:00",
                "link": {
                    "rel": "self",
                    "href": "http:\/\/open311.sfgov.org\/dev\/V1\/reports\/637619.xml"
                },
                "author": {
                    "name": "John Doe"
                },
                "georss:point": "40.7111 -73.9565",
                "category": {
                    "attributes": {
                        "label": "Damaged tree",
                        "term": "tree-damage",
                        "scheme": "https:\/\/open311.sfgov.org\/dev\/V1\/categories\/006.xml"
                    },
                    "children": ["006"]
                },
                "content": {
                    "children": [{
                        "report_id": "637619",
                        "address": "1600 Market St, San Francisco, CA 94103",
                        "description": "A large tree branch is blocking the road",
                        "status": "created",
                        "status_notes": [],
                        "policy": "The City will inspect and require the responsible party to correct within 24 hours and\/or issue a Correction Notice or Notice of Violation of the Public Works Code"
                    }],
                    "attributes": {
                        "type": "xml"
                    }
                }
            },
            {
                "id": "tag:open311.sfgov.org,2010-04-15:\/dev\/V1\/reports\/637620.xml",
                "title": "A large tree branch is blocking the road",
                "updated": "2010-04-13T18:30:02-05:00",
                "link": {
                    "rel": "self",
                    "href": "http:\/\/open311.sfgov.org\/dev\/V1\/reports\/637620.xml"
                },
                "author": {
                    "name": "John Doe"
                },
                "georss:point": "40.7111 -73.9565",
                "category": {
                    "attributes": {
                        "label": "Damaged tree",
                        "term": "tree-damage",
                        "scheme": "https:\/\/open311.sfgov.org\/dev\/V1\/categories\/006.xml"
                    },
                    "children": ["006"]
                },
                "content": {
                    "children": [{
                        "report_id": "637620",
                        "address": "1600 Market St, San Francisco, CA 94103",
                        "description": "A large tree branch is blocking the road",
                        "status": "created",
                        "status_notes": [],
                        "policy": "The City will inspect and require the responsible party to correct within 24 hours and\/or issue a Correction Notice or Notice of Violation of the Public Works Code"
                    }],
                    "attributes": {
                        "type": "xml"
                    }
                }
            },
            {
                "id": "tag:open311.sfgov.org,2010-04-15:\/dev\/V1\/reports\/637620.xml",
                "title": "A large tree branch is blocking the road",
                "updated": "2010-04-13T18:30:02-05:00",
                "link": {
                    "rel": "self",
                    "href": "http:\/\/open311.sfgov.org\/dev\/V1\/reports\/637620.xml"
                },
                "author": {
                    "name": "John Doe"
                },
                "georss:point": "40.7111 -73.9565",
                "category": {
                    "attributes": {
                        "label": "Damaged tree",
                        "term": "tree-damage",
                        "scheme": "https:\/\/open311.sfgov.org\/dev\/V1\/categories\/006.xml"
                    },
                    "children": ["006"]
                },
                "content": {
                    "children": [{
                        "report_id": "637620",
                        "address": "1600 Market St, San Francisco, CA 94103",
                        "description": "A large tree branch is blocking the road",
                        "status": "created",
                        "status_notes": [],
                        "policy": "The City will inspect and require the responsible party to correct within 24 hours and\/or issue a Correction Notice or Notice of Violation of the Public Works Code"
                    }],
                    "attributes": {
                        "type": "xml"
                    }
                }
            }]
        }
    });

JsonML Convention
-----------------

JsonML was designed specifically to losslessly round-trip between XML and JSON. As such it was designed to handle mixed-mode content (i.e. textual data outside of or next to elements). Mixed-mode content is commonly meaningful in XML formats such as XHTML. JsonML handles namespaces in the same way that XML 1.0 does: attributes for xmlns and tag names with colons.

### References

-   "Documentation": <http://jsonml.org>
-   "Documentation": <http://www.ibm.com/developerworks/library/x-jsonml/>

### The JSON Representation

    [
        "reports",
        {
            "xmlns" : "http://www.w3.org/2005/Atom"
        },
        [
            "entry",
            [
                "id",
                "tag:open311.sfgov.org,2010-04-15:/dev/V1/reports/637619.xml"
            ],
            [
                "title",
                "A large tree branch is blocking the road"
            ],
            [
                "updated",
                "2010-04-13T18:30:02-05:00"
            ],
            [
                "link",
                {
                    "href" : "http://open311.sfgov.org/dev/V1/reports/637619.xml",
                    "rel" : "self"
                }
            ],
            [
                "author",
                [
                    "name",
                    "John Doe"
                ]
            ],
            [
                "georss:point",
                {
                    "xmlns:georss" : "http://www.georss.org/georss"
                },
                "40.7111 -73.9565"
            ],
            [
                "category",
                {
                    "label" : "Damaged tree",
                    "scheme" : "https://open311.sfgov.org/dev/V1/categories/006.xml",
                    "term" : "tree-damage"
                },
                "006"
            ],
            [
                "content",
                {
                    "type" : "xml",
                    "xmlns" : "http://open311.org/spec/georeport-v1"
                },
                [
                    "report_id",
                    "637619"
                ],
                [
                    "address",
                    "1600 Market St, San Francisco, CA 94103"
                ],
                [
                    "description",
                    "A large tree branch is blocking the road"
                ],
                [
                    "status",
                    "created"
                ],
                [
                    "status_notes"
                ],
                [
                    "policy",
                    "The City will inspect and require the responsible party to correct within 24 hours and/or issue a Correction Notice or Notice of Violation of the Public Works Code"
                ]
            ]
        ],
        [
            "entry",
            [
                "id",
                "tag:open311.sfgov.org,2010-04-15:/dev/V1/reports/637620.xml"
            ],
            [
                "title",
                "A large tree branch is blocking the road"
            ],
            [
                "updated",
                "2010-04-13T18:30:02-05:00"
            ],
            [
                "link",
                {
                    "href" : "http://open311.sfgov.org/dev/V1/reports/637620.xml",
                    "rel" : "self"
                }
            ],
            [
                "author",
                [
                    "name",
                    "John Doe"
                ]
            ],
            [
                "georss:point",
                {
                    "xmlns:georss" : "http://www.georss.org/georss"
                },
                "40.7111 -73.9565"
            ],
            [
                "category",
                {
                    "label" : "Damaged tree",
                    "scheme" : "https://open311.sfgov.org/dev/V1/categories/006.xml",
                    "term" : "tree-damage"
                },
                "006"
            ],
            [
                "content",
                {
                    "type" : "xml",
                    "xmlns" : "http://open311.org/spec/georeport-v1"
                },
                [
                    "report_id",
                    "637620"
                ],
                [
                    "address",
                    "56 Market St, San Francisco, CA 94103"
                ],
                [
                    "description",
                    "A large tree branch is blocking the road"
                ],
                [
                    "status",
                    "created"
                ],
                [
                    "status_notes"
                ],
                [
                    "policy",
                    "The City will inspect and require the responsible party to correct within 24 hours and/or issue a Correction Notice or Notice of Violation of the Public Works Code"
                ]
            ]
        ],
        [
            "entry",
            [
                "id",
                "tag:open311.sfgov.org,2010-04-15:/dev/V1/reports/637621.xml"
            ],
            [
                "title",
                "A large tree branch is blocking the road"
            ],
            [
                "updated",
                "2010-04-13T18:30:02-05:00"
            ],
            [
                "link",
                {
                    "href" : "http://open311.sfgov.org/dev/V1/reports/637621.xml",
                    "rel" : "self"
                }
            ],
            [
                "author",
                [
                    "name",
                    "John Doe"
                ]
            ],
            [
                "georss:point",
                {
                    "xmlns:georss" : "http://www.georss.org/georss"
                },
                "40.7111 -73.9565"
            ],
            [
                "category",
                {
                    "label" : "Damaged tree",
                    "scheme" : "https://open311.sfgov.org/dev/V1/categories/006.xml",
                    "term" : "tree-damage"
                },
                "006"
            ],
            [
                "content",
                {
                    "type" : "xml",
                    "xmlns" : "http://open311.org/spec/georeport-v1"
                },
                [
                    "report_id",
                    "637621"
                ],
                [
                    "address",
                    "1800 Market St, San Francisco, CA 94103"
                ],
                [
                    "description",
                    "A large tree branch is blocking the road"
                ],
                [
                    "status",
                    "created"
                ],
                [
                    "status_notes"
                ],
                [
                    "policy",
                    "The City will inspect and require the responsible party to correct within 24 hours and/or issue a Correction Notice or Notice of Violation of the Public Works Code"
                ]
            ]
        ]
    ]

The oData Convention
--------------------

I haven't fully read up on the ways that oData uses Atom representations versus JSON representations, but it doesn't look like they completely map over. It looks like the JSON representation is mostly just concerned with the data contained with the content element of the Atom entry.

### References

-   **Documentation**: [Representing JSON Entries](http://www.odata.org/developers/protocols/json-format#RepresentingEntries) versus [Representing Atom Entries](http://www.odata.org/developers/protocols/atom-format#RepresentingEntries)
-   **oData Libraries**: <http://www.odata.org/developers/odata-sdk>

Additional Resources
--------------------

Other relevant resources:

-   <http://www.terracoder.com/index.php/xml-objectifier/xml-objectifier-examples>
-   <http://json-lib.sourceforge.net/>
-   <http://sandeep-aparajit.blogspot.com/2010/01/json-to-xml-and-xml-to-json-converter.html>
-   [Atom to JSON with Erlang](http://intertwingly.net/blog/2007/09/05/Atom-to-JSON-with-Erlang)
-   [application/atom+json proposal](http://intertwingly.net/blog/2007/01/15/application-atom-json) ... basically a big argument about whether this is a good idea, particularly in the face of atom extensions.

Geospatial Features in XML and JSON
===================================

GeoRSS Example
--------------

(Based on GML) See [GeoRSS.org](http://georss.org/GML)

    <?xml version="1.0" encoding="utf-8"?>
     <feed ns="http://www.w3.org/2005/Atom"
          xmlns:georss="http://www.georss.org/georss"
          xmlns:gml="http://www.opengis.net/gml">
       <title>Earthquakes</title>

       <subtitle>International earthquake observation labs</subtitle>
       <link href="http://example.org/"/>
       <updated>2005-12-13T18:30:02Z</updated>
       <author>
          <name>Dr. Thaddeus Remor</name>
          <email>tremor@quakelab.edu</email>
       </author>
       <id>urn:uuid:60a76c80-d399-11d9-b93C-0003939e0af6</id>
       <entry>
          <title>M 3.2, Mona Passage</title>
          <link href="http://example.org/2005/09/09/atom01"/>
          <id>urn:uuid:1225c695-cfb8-4ebb-aaaa-80da344efa6a</id>
          <updated>2005-08-17T07:02:32Z</updated>
          <summary>We just had a big one.</summary>
          <georss:where>
             <gml:Point>
                <gml:pos>45.256 -71.92</gml:pos>
             </gml:Point>
          </georss:where>
       </entry>
     </feed>

GeoJSON Example
---------------

See [GeoJSON.org](http://geojson.org)

    { "type": "FeatureCollection",
      "features": [
        { "type": "Feature",
          "geometry": {"type": "Point", "coordinates": [102.0, 0.5]},
          "properties": {"prop0": "value0"}
          },
        { "type": "Feature",
          "geometry": {
            "type": "LineString",
            "coordinates": [
              [102.0, 0.0], [103.0, 1.0], [104.0, 0.0], [105.0, 1.0]
              ]
            },
          "properties": {
            "prop0": "value0",
            "prop1": 0.0
            }
          },
        { "type": "Feature",
           "geometry": {
             "type": "Polygon",
             "coordinates": [
               [ [100.0, 0.0], [101.0, 0.0], [101.0, 1.0],
                 [100.0, 1.0], [100.0, 0.0] ]
               ]
           },
           "properties": {
             "prop0": "value0",
             "prop1": {"this": "that"}
             }
           }
         ]
       }