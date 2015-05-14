---
title: GeoReport v2 Servers
permalink: /GeoReport_v2/Servers/
---

### Open311 GeoReport v2 Servers

The following is a list of official API endpoints for jurisdictions that support the Open311 [GeoReport v2](/GeoReport_v2 "wikilink") specification.

<span class="text-danger">*Note that the URLs require a method like /services.xml (and jurisdiction_id if serving multiple jurisdictions). **The base URL is not intended to be accessed directly**. To ensure the Test and Production endpoint URLs listed here reach a valid resource, they all point to the **GET Services** method as an example* </span>

**<span class="text-primary">New!</span> You can now check on the status of endpoints at: <http://open311status.herokuapp.com/>**

#### Jurisdiction Specific Endpoints

<a class="btn btn-default edit-button" href="//github.com/{{ site.org_name }}/{{ site.repo_name }}/edit/{{ site.branch }}/data/servers.yml"><span class="glyphicon glyphicon-edit"></span> Edit</a>
<a class="btn btn-default" href="/data/servers.yml"><span class="glyphicon glyphicon-download"></span> Download as YML</a>
<a class="btn btn-default" href="../servers.json"><span class="glyphicon glyphicon-download"></span> Download as JSON</a>

<table class="table table-striped table-bordered">
    <tr>
        <th>Name</th>
        <th>Country</th>                
        <th>API Discovery</th>
        <th>API Key Request</th>
        <th>Documentation</th>
        <th>Production URL Example</th>
        <th>Test URL Example</th>
        <th>Gov Domain</th>
    </tr>
{% for server in site.data.servers %}
    {% if server.production_ready %}
        <tr>
            <td>{{ server.name }}</td>
            <td>{{ server.country }}</td>             
            <td><a href="{{ server.api_discovery }}"><span class="glyphicon glyphicon-cloud-download"></span><span class="sr-only">Download</span></a></td>
            <td>{% if server.api_key_request.size > 0 %}<a href="{{ server.api_key_request }}"><span class="glyphicon glyphicon-cloud-download"></span><span class="sr-only">Download</span></a>{% endif %}</td>
            <td>{% if server.api_documentation.size > 0 %}<a href="{{ server.api_documentation }}"><span class="glyphicon glyphicon-file"></span><span class="sr-only">Download</span></a>{% endif %}</td>
            <td><a href="{{ server.base_url }}services.xml?jurisdiction_id={{ server.jurisdiction_id }}">Production /services.xml </a></td>
            <td>{% if server.test_url.size > 0 %}<a href="{{ server.test_url }}services.xml?jurisdiction_id={{ server.jurisdiction_id }}">Test /services.xml</a>{% endif %}</td>
            <td>
                {% if server.gov_domain == true %}<span class="glyphicon glyphicon-ok text-success"></span><span class="sr-only">Yes</span>{% endif %}
                {% if server.gov_domain == false %}<span class="glyphicon glyphicon-remove text-danger"></span><span class="sr-only">No</span>{% endif %}
            </td>
        </tr>
    {% endif %}
{% endfor %}
</table>

#### Other Endpoints in Development
<table class="table table-striped table-bordered">
    <tr>
        <th>Name</th>
        <th>Country</th>                
        <th>API Discovery</th>
        <th>API Key Request</th>
        <th>Documentation</th>
        <th>Production URL Example</th>
        <th>Test URL Example</th>
        <th>Gov Domain</th>
    </tr>
{% for server in site.data.servers %}
    {% if server.production_ready != true %}
        <tr>
            <td>{{ server.name }}</td>
            <td>{{ server.country }}</td>             
            <td><a href="{{ server.api_discovery }}"><span class="glyphicon glyphicon-cloud-download"></span><span class="sr-only">Download</span></a></td>
            <td>{% if server.api_key_request.size > 0 %}<a href="{{ server.api_key_request }}"><span class="glyphicon glyphicon-cloud-download"></span><span class="sr-only">Download</span></a>{% endif %}</td>
            <td>{% if server.api_documentation.size > 0 %}<a href="{{ server.api_documentation }}"><span class="glyphicon glyphicon-file"></span><span class="sr-only">Download</span></a>{% endif %}</td>
            <td><a href="{{ server.base_url }}services.xml?jurisdiction_id={{ server.jurisdiction_id }}">Production /services.xml </a></td>
            <td>{% if server.test_url.size > 0 %}<a href="{{ server.test_url }}services.xml?jurisdiction_id={{ server.jurisdiction_id }}">Test /services.xml</a>{% endif %}</td>
            <td>
                {% if server.gov_domain == true %}<span class="glyphicon glyphicon-ok text-success"></span><span class="sr-only">Yes</span>{% endif %}
                {% if server.gov_domain == false %}<span class="glyphicon glyphicon-remove text-danger"></span><span class="sr-only">No</span>{% endif %}
            </td>
        </tr>
    {% endif %}
{% endfor %}
</table>