# Sites

## GET Sites by Hostname

{% code-tabs %}

{% code-tabs-item title="cURL" %}

```bash
curl --request GET \
    --header "Authorization: Token $token" \
    --header "Accept: application/vnd.salemove.v1+json" \
    "https://api.salemove.com/sites?hostname=$hostname"
```

{% endcode-tabs-item %}

{% code-tabs-item title=JavaScript %}

```javascript
var XMLHttpRequest = require('xmlhttprequest').XMLHttpRequest;

var xhr = new XMLHttpRequest();

xhr.open('GET', 'https://api.salemove.com/sites?hostname=$hostname', false);

xhr.setRequestHeader('authorization', `Token ${token}`);
xhr.setRequestHeader('accept', 'application/vnd.salemove.v1+json');

xhr.send();

var response = JSON.parse(xhr.responseText);

console.log(response);
```

{% endcode-tabs-item %}

{% code-tabs-item title=Ruby %}

```ruby
require 'httparty'

ENDPOINT = "https://api.salemove.com/sites"

token = ARGV[0].strip
hostname = ARGV[1].strip

headers = {
  :authorization => "Token #{token}",
  :accept => "application/vnd.salemove.v1+json"
}

raw_response = HTTParty.get(
  "#{ENDPOINT}?hostname=#{hostname}",
  headers: headers
)

response = JSON.parse raw_response.body

puts response
```

{% endcode-tabs-item %}

{% endcode-tabs %}

> Generates the output

```json
{
  "last_page": "https://api.salemove.com/sites?hostname=company.com&page=1",
  "sites": [
    {
      "href": "https://api.salemove.com/sites/2e56b224-6708-4755-b6c9-35f9889e42dd",
      "id": "2e56b224-6708-4755-b6c9-35f9889e42dd",
      "addresses": [
        "company.com",
        "service.company.com",
        "company.mobi",
        "company.io"
      ]
    }
  ]
}
```

**Action:** `GET /sites?hostname=$hostname`

Fetches an array of sites that have the given `hostname` assigned to them.

A site can have one or more `addresses`, where an `address` is a combination of
`hostname` + `path`. For example, a valid address could be `salemove.com/auto`
where `hostname`=`salemove.com` and `path`=`/auto`.

<!--- NEW SITE -->

{% api-method method="post" host="https://api.salemove.com" path="/sites" %}

{% api-method-summary %}

New Site

{% endapi-method-summary %}

{% api-method-description %} Creates a new site. Only users with the
`super_manager` role can create new sites. {% endapi-method-description %}

{% api-method-spec %}

{% api-method-request %}

{% api-method-query-parameters %}

{% api-method-parameter name="name" type="string" required=true %} The name for
the new site. {% endapi-method-parameter %}

{% api-method-parameter name="addresses" type="array" required=true %} A list of
the site's addresses. Addresses must be without protocol prefixes and ports. Can
be a domain name (`www.example.com`) to let Glia run on all sites, or include
path to restrict the access (`www.example.com/home`).
{% endapi-method-parameter %}

{% api-method-parameter name="clone_from_id" type="string" required=false %} The
new site will be configured using this `site_id` as a template. The new site
will copy the visuals, teams and business rules from the `site_id` passed in
this parameter. {% endapi-method-parameter %}

{% endapi-method-query-parameters %}

{% endapi-method-request %}

{% api-method-response %}

{% api-method-response-example httpCode=200 %}

```json
{
  "href": "https://api.salemove.com/sites/3a5c1497-a0f8-470c-af10-c5c2b8fe88cc",
  "id": "3a5c1497-a0f8-470c-af10-c5c2b8fe88cc",
  "hostnames": ["institution.com", "login.institution.com"],
  "name": "Institution",
  "salemove_enabled": false
}
```

{% endapi-method-response-example %}

{% endapi-method-response %}

{% endapi-method-spec %}

{% endapi-method %}

{% code-tabs %}

{% code-tabs-item title="cURL" %}

```bash
curl --request POST \
    --header "Authorization: Bearer $access_token" \
    --header "Content-Type: application/json" \
    --header "Accept: application/vnd.salemove.v1+json" \
    --data-binary '{
      "name": "Institution",
      "addresses": ["institution.com","login.institution.com"]
    }' \
    "https://api.salemove.com/sites"
```

{% endcode-tabs-item %}

{% code-tabs-item title=undefined %}

```javascript
var XMLHttpRequest = require('xmlhttprequest').XMLHttpRequest;

var xhr = new XMLHttpRequest();

xhr.open('POST', 'https://api.salemove.com/sites', false);

xhr.setRequestHeader('authorization', `Bearer ${accessToken}`);
xhr.setRequestHeader('content-type', 'application/json');
xhr.setRequestHeader('accept', 'application/vnd.salemove.v1+json');

var data = {
  name: 'Institution',
  addresses: ['institution.com', 'login.institution.com']
};

var query = JSON.stringify(data);

xhr.send(query);

var response = JSON.parse(xhr.responseText);

console.log(response);
```

{% endcode-tabs-item %}

{% code-tabs-item title=undefined %}

```ruby
require 'httparty'

ENDPOINT = "https://api.salemove.com/sites"


token = ARGV[0].strip

headers = {
  :authorization => "Bearer #{access_token}",
  :content_type => "application/json",
  :accept => "application/vnd.salemove.v1+json"
}

options = {
  headers: headers,
  query: {
    "name": "Institution",
    "addresses": ["institution.com","login.institution.com"]
  }
}

raw_response = HTTParty.post(
  ENDPOINT,
  options
)

response = JSON.parse raw_response.body

puts response
```

{% endcode-tabs-item %}

{% endcode-tabs %}

<!--- GET SITE -->

## GET Site

{% code-tabs %}

{% code-tabs-item title="cURL" %}

```bash
curl --request GET \
    --header "Authorization: Bearer $access_token" \
    --header "Accept: application/vnd.salemove.v1+json" \
    "https://api.salemove.com/sites/$site_id"
```

{% endcode-tabs-item %}

{% code-tabs-item title=undefined %}

```javascript
var XMLHttpRequest = require('xmlhttprequest').XMLHttpRequest;

var xhr = new XMLHttpRequest();

xhr.open('GET', 'https://api.salemove.com/sites/$site_id', false);

xhr.setRequestHeader('authorization', `Bearer ${accessToken}`);
xhr.setRequestHeader('accept', 'application/vnd.salemove.v1+json');

xhr.send();

var response = JSON.parse(xhr.responseText);

console.log(response);
```

{% endcode-tabs-item %}

{% code-tabs-item title=undefined %}

```ruby
require 'httparty'

ENDPOINT = "https://api.salemove.com/sites"

token = ARGV[0].strip
site_id = ARGV[1].strip

headers = {
  :authorization => "Bearer #{access_token}",
  :accept => "application/vnd.salemove.v1+json"
}

raw_response = HTTParty.get(
  "#{ENDPOINT}/#{site_id}",
  headers: headers
)

response = JSON.parse raw_response.body

puts response
```

{% endcode-tabs-item %}

{% endcode-tabs %}

> Generates the output

```json
{
  "href": "https://api.salemove.com/sites/3a5c1497-a0f8-470c-af10-c5c2b8fe88cc",
  "id": "3a5c1497-a0f8-470c-af10-c5c2b8fe88cc",
  "name": "Institution",
  "hostnames": ["institution.com","login.institution.com"],
  "logo": {
    "url": null
  }
  "default_operator_picture": {
    "url": null
  },
  "always_use_default_operator_picture": false,
  "widget_mode": true,
  "reactive_enabled": true,
  "reactive_call_timeout": 30,
  "proactive_enabled": true,
  "proactive_call_timeout": 15,
  "multi_engagement_enabled": true,
  "multi_engagement_default_availability": "unavailable",
  "multi_engagement_max_count": 2,
  "multi_engagement_idle_time": 15,
  "time_zone": "Eastern Time (US & Canada)",
  "missed_call_unavailability_enabled": true,
  "welcome_message": null,
  "visitor_user_agent_whitelist": ["safari", "chrome"],
  "observation_enabled": true,
  "store_recording": true,
  "cobrowse_permission_required": false,
  "public_visitor_custom_attribute_changes_allowed": true,
  "interactive_cobrowsing_enabled": true,
  "allowed_login_ips": [],
  "allowed_file_content_types": ["image/png", "image/jpeg", "application/pdf"],
  "video_in_call_visualizer": "two-way",
  "store_file_attachments": true,
  "custom_code": "",
  "interpret_document_mode_as_ie_version": true,
  "operator_console_omnibrowse": true,
  "reactive_tab": {
    "back_color": "#6bc56f",
    "contact_when_unstaffed": true,
    "font_size": 20,
    "format": "mix",
    "front_color": "#eeeeee",
    "hover_color": "#05a94d",
    "icon_class": "ico-text",
    "placement": "left",
    "position": "right",
    "show_unavailable": true,
    "size": 100,
    "text": "Let's talk!",
    "vertical_offset": 50,
    "visible_operator_count": 3
  },
  "visitor_page_adaption": "div",
  "salemove_enabled": true,
  "map": {
    "latitude": 25.0,
    "longitude": 5.0,
    "zoom": 2
  },
  "store_data": true,
  "allowed_file_senders": {
    "operator": false,
    "visitor": false
  },
  "addresses": ["example.local.dev", "example-eu.local.dev", "example-us.local.dev"],
  "visitor_app_phone_extension_enabled": false,
  "boot_delay_ms": 0,
  "shortcuts_enabled": true,
  "phone_number_default_country": "us"
}
```

**Action:** `GET /sites/{id}`

This request fetches the site with the ID of `id`. The user must have at least
the `manager` role on the fetched site.

### Output

| Field                                             | Type    | Required | Description                                                                                                                                                                                                                                   |
| :------------------------------------------------ | :------ | :------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `href`                                            | String  | Yes      | The URL of requested site.                                                                                                                                                                                                                    |
| `id`                                              | String  | Yes      | The ID of the site that is requested.                                                                                                                                                                                                         |
| `name`                                            | String  | No       | The site `name` that is being requested.                                                                                                                                                                                                      |
| `hostname`                                        | Array   | Yes      | **DEPRECATED**. An array of client's allowed sites. Used as the same purpose for `addresses` but kept for backward compatibility.                                                                                                             |
| `logo`                                            | String  | No       | The site's logo in base64 format. If `null` then the picture is deleted.                                                                                                                                                                      |
| `default_operator_picture`                        | String  | No       | The site's default operator picture in base64 format. If `null` then the picture is deleted.                                                                                                                                                  |
| `always_use_default_operator_picture`             | Boolean | No       | Always use default operator picture instead of user's profile picture.                                                                                                                                                                        |
| `widget_mode`                                     | Boolean | No       | If `true`, the visitor's engagement panel detaches and is movable. If `false`, the visitor's engagement panel remains intact to the edge of the window.                                                                                       |
| `reactive_enabled`                                | Boolean | No       | If `true` then the reactive tb is shown to the visitor. If `false` then the reactive tab is hidden from the visitor.                                                                                                                          |
| `reactive_call_timeout`                           | Integer | No       | The time (in seconds) that operators have to answer an incoming engagement request before the request is re-tried or marked as declined.                                                                                                      |
| `proactive_enabled`                               | Boolean | No       | If `true`, the operator is able to call the visitor. If `false`, the operator can only wait for the visitor to call.                                                                                                                          |
| `proactive_call_timeout`                          | Integer | No       | The time (in seconds) that visitors have to answer an incoming engagement before the engagement is re-tried or marked as declined.                                                                                                            |
| `multi_engagement_enabled`                        | Boolean | No       | If `true`, the operator is able to conduct multiple engagements simultaneously. If `false`, the operator is only able to be engaged in 1 engagement at a time.                                                                                |
| `multi_engagement_default_availability`           | String  | No       | Controls how the operator's availability status is updated during an engagement - namely `retain`, `chat` or `unavailable`.                                                                                                                   |
| `multi_engagement_max_count`                      | Integer | No       | The amount of engagements that an operator can participate in at any given time.                                                                                                                                                              |
| `multi_engagement_idle_time`                      | Integer | No       | The time (in seconds) before the operator is reminded to re-engage with the visitor on hold.                                                                                                                                                  |
| `time_zone`                                       | String  | No       | The time zone that is used for statistics and general usage. The syntax is just city to time zone mapping, e.g `Eastern Time (US & Canada)`.                                                                                                  |
| `missed_call_unavailability_enabled`              | Boolean | No       | If `true`, automatically places operators into a system unavailable status - 'Idle' when they miss a reactive engagement request. If `false`, operators still retain the availability status that they selected.                              |
| `welcome_message`                                 | String  | No       | The message that is automatically sent at the start of each engagement. It fits an unlimited number of characters.                                                                                                                            |
| `visitor_user_agent_whitelist`                    | Array   | No       | Browsers not supported by Glia which the operators are allowed to use.                                                                                                                                                                        |
| `observation_enabled`                             | Boolean | No       | If `true`, operators are able to observe visitors' browsing before an engagement. If `false`, operators are not able to observe visitor before an engagement.                                                                                 |
| `store_recording`                                 | Boolean | No       | If `true`, audio recordings of the site are stored. If `false`, audio recordings of the site are not stored.                                                                                                                                  |
| `cobrowse_permission_required`                    | Boolean | No       | If `true`, the visitor's permission to co-browse will be requested before the session in an engagement. If `false`, the operator can start co-browsing with a visitor anytime.                                                                |
| `public_visitor_custom_attribute_changes_allowed` | Boolean | No       | If `true`, it is possible for a visitor to update their custom attributes using JavaScript in the browser.                                                                                                                                    |
| `interactive_cobrowsing_enabled`                  | Boolean | No       | If `true`, the operator will be able to click on the visitor's website elements, fill in forms, and more during co-browsing. If `false`, the operator will not be able to interact with the visitor's website during co-browsing.             |
| `allowed_login_ips`                               | Array   | No       | Allows login to Glia only from the IP addresses defined. Supports only IPv4 and range in CIDR notation.                                                                                                                                       |
| `allowed_file_content_types`                      | Array   | No       | Array of file MIME types that are allowed to be sent.                                                                                                                                                                                         |
| `video_in_call_visualizer`                        | String  | No       | Controls if and how video can be used in call visualizer - namely "two-way", "one-way" or "off".                                                                                                                                              |
| `store_file_attachments`                          | Boolean | No       | If `true`, chat file attachments would be stored. If `false`, the file attachments will be deleted 24 hours after the engagement ends and the files' metadata will remain in the chat transcript.                                             |
| `custom_code`                                     | String  | No       | Custom JavaScript that will be executed on the site’s web pages along with Glia integration script.                                                                                                                                           |
| `interpret_document_mode_as_ie_version`           | Boolean | No       | If `true`, detects visitor’s Internet Explorer version using the `document.documentMode` property. If `false`, it does not detect visitor's Internet Explorer version.                                                                        |
| `operator_console_omnibrowse`                     | Boolean | No       | If `true` then it enables Call Visualizer in the Glia Hub. If `false` then it disables Call Visualizer in the Glia Hub.                                                                                                                       |
| `reactive_tab`                                    | Object  | No       | Customize the reactive bubble's aesthetics.                                                                                                                                                                                                   |
| `visitor_page_adaption`                           | String  | No       | Define the visitor's engagement mode, namely - `iframe`, `div`, `style`.                                                                                                                                                                      |
| `salemove_enabled`                                | Boolean | No       | If `true` then it enables Glia for the site, if `false` it disables Glia for the site. When Glia is enabled the Glia integration is delivered otherwise a `204` `No-Content` is delivered.                                                    |
| `map`                                             | Object  | No       | An object with three possible attributes `latitude`, `longitude`, `zoom`. Describes the platform console map center coordinate and the zoom level.                                                                                            |
| `store_data`                                      | Boolean | No       | If `true`, engagement chat transcripts of the site are stored. If `false`, engagement chat transcripts of the site are not stored.                                                                                                            |
| `allowed_file_senders`                            | Object  | No       | Allows sending file attachments in the chat from visitor to operator and/or operator to visitor. E.g. `{operator: true, visitor: true}`.                                                                                                      |
| `addresses`                                       | Array   | Yes      | A list of Site’s addresses that are being get. Addresses must be without protocol prefixes and ports. Can be a domain name (`www.example.com`) to let Glia run on all sites, or include path to restrict the access (`www.example.com/home`). |
| `visitor_app_phone_extension_enabled`             | Boolean | No       | If `true` then phone extension input is shown alongside phone number input in Visitor App.                                                                                                                                                    |
| `boot_delay_ms`                                   | Integer | No       | Delays the bootstrapping of Glia Visitor App by the given milliseconds. Delay may be useful on very heavy sites.                                                                                                                              |
| `shortcuts_enabled`                               | Boolean | No       | If `true`, keyboard shortcuts are enabled in the Glia Hub.                                                                                                                                                                                    |
| `phone_number_default_country`                    | String  | No       | The country code that will be displayed by default when visitors enter their phone number.                                                                                                                                                    |

<!--- UPDATE SITE -->

{% api-method method="put" host="https://api.salemove.com" path="/sites/{id}" %}

{% api-method-summary %}

Update Site

{% endapi-method-summary %}

{% api-method-description %} This request updates the site with the ID of `id`.
The user must have the `super_manager` role on the site to be updated.
{% endapi-method-description %}

{% api-method-spec %}

{% api-method-request %}

{% api-method-body-parameters %}

{% api-method-parameter name="href" type="string" required=yes %}

The URL of requested site.

{% endapi-method-parameter %}

{% api-method-parameter name="id" type="string" required=true %} The site `id`
that is being updated. {% endapi-method-parameter %}

{% api-method-parameter name="name" type="string" required=false %} The site
`name` that is being updated. {% endapi-method-parameter %}

{% api-method-parameter name="hostname" type="array" required=true %}

**DEPRECATED**. An array of client's allowed sites. Used as the same purpose for
`addresses` but kept for backward compatibility.

{% endapi-method-parameter %}

{% api-method-parameter name="logo" type="string" required=false %} The site's
logo in base64 format. If `null` then the picture is deleted.
{% endapi-method-parameter %}

{% api-method-parameter name="default_operator_picture" type="string" required=false %}
The site's default operator picture in base64 format. If `null` then the picture
is deleted. {% endapi-method-parameter %}

{% api-method-parameter name="always_use_default_operator_picture" type="boolean" required=false %}

Always use default operator picture instead of operator profile picture.

{% endapi-method-parameter %}

{% api-method-parameter name="widget_mode" type="boolean" required=false %}

If `true`, the visitor's engagement panel detaches and is movable. If `false`,
the visitor's engagement panel remains intact to the edge of the window.

{% endapi-method-parameter %}

{% api-method-parameter name="reactive_enabled" type="boolean" required=false %}
If `true` then the reactive tab is shown to the visitor. If `false` then the
reactive tab is hidden from the visitor. {% endapi-method-parameter %}

{% api-method-parameter name="reactive_call_timeout" type="integer" required=false %}

The time (in seconds) that operators have to answer an incoming call before the
call is re-tried or marked as declined.

{% endapi-method-parameter %}

{% api-method-parameter name="proactive_enabled" type="boolean" required=false %}

If `true`, the operator is able to call the visitor. If `false`, the operator
can only wait for the visitor to call.

{% endapi-method-parameter %}

{% api-method-parameter name="proactive_call_timeout" type="integer" required=false %}

The time (in seconds) that visitors have to answer an incoming call before the
call is re-tried or marked as declined.

{% endapi-method-parameter %}

{% api-method-parameter name="multi_engagement_enabled" type="boolean" required=false %}

If `true`, the operator is able to conduct multiple engagements simultaneously.
If `false`, the operator is only able to be engaged in 1 engagement at a time.

{% endapi-method-parameter %}

{% api-method-parameter name="multi_engagement_default_availability" type="string" required=false %}

Controls how the operator's availability status is updated during an
engagement - namely `retain`, `chat` or `unavailable`.

{% endapi-method-parameter %}

{% api-method-parameter name="multi_engagement_max_count" type="integer" required=false %}

The amount of engagements that an operator can participate in at any given time.

{% endapi-method-parameter %}

{% api-method-parameter name="multi_engagement_idle_time" type="integer" required=false %}

The time (in seconds) before the operator is reminded to re-engage with the
visitor on hold.

{% endapi-method-parameter %}

{% api-method-parameter name="time_zone" type="string" required=false %}

The time zone that is used for statistics and general usage. The syntax is just
city to time zone mapping, e.g `Eastern Time (US & Canada)`.

{% endapi-method-parameter %}

{% api-method-parameter name="missed_call_unavailability_enabled" type="boolean" required=false %}

If `true`, automatically places operators into a system unavailable status -
'Idle' when they miss a reactive engagement request. If `false`, operators still
retain the availability status that they selected.

{% endapi-method-parameter %}

{% api-method-parameter name="welcome_message" type="string" required=false %}

The message that is automatically sent at the start of each engagement. It fits
an unlimited number of characters.

{% endapi-method-parameter %}

{% api-method-parameter name="visitor_user_agent_whitelist" type="array" required=false %}

Browsers not supported by Glia which the operators are allowed to use.

{% endapi-method-parameter %}

{% api-method-parameter name="observation_enabled" type="boolean" required=false %}

If `true`, operators are able to observe visitors' browsing before an
engagement. If `false`, operators are not able to observe visitor before an
engagement.

{% endapi-method-parameter %}

{% api-method-parameter name="store_recording" type="boolean" required=false %}

If `true`, audio recordings of the site are stored. If `false`, audio recordings
of the site are not stored.

{% endapi-method-parameter %}

{% api-method-parameter name="cobrowse_permission_required" type="boolean" required=false %}

If `true`, the visitor's permission to co-browse will be requested before the
session in an engagement. If `false`, the operator can start co-browsing with a
visitor anytime.

{% endapi-method-parameter %}

{% api-method-parameter name="public_visitor_custom_attribute_changes_allowed" type="boolean" required=false %}

If `true`, it is possible for a visitor to update their custom attributes using
JavaScript in the browser.

{% endapi-method-parameter %}

{% api-method-parameter name="interactive_cobrowsing_enabled" type="boolean" required=false %}

If `true`, the operator will be able to click on the visitor's website elements,
fill in forms, and more during co-browsing. If `false`, the operator will not be
able to interact with the visitor's website during co-browsing.

{% endapi-method-parameter %}

{% api-method-parameter name="allowed_login_ips" type="array" required=false %}

Allows login to Glia only from the IP addresses defined. Supports only IPv4 and
range in CIDR notation.

{% endapi-method-parameter %}

{% api-method-parameter name="allowed_file_content_types" type="array" required=false %}

Array of file MIME types that are allowed to be sent.

{% endapi-method-parameter %}

{% api-method-parameter name="video_in_call_visualizer" type="string" required=false %}

Controls if and how video can be used in call visualizer - namely "two-way",
"one-way" or "off".

{% endapi-method-parameter %}

{% api-method-parameter name="store_file_attachments" type="boolean" required=false %}

If `true`, chat file attachments would be stored. If `false`, the file
attachments will be deleted 24 hours after the engagement ends and the files'
metadata will remain in the chat transcript.

{% endapi-method-parameter %}

{% api-method-parameter name="custom_code" type="string" required=false %}

Custom JavaScript that will be executed on the site’s web pages along with Glia
integration script.

{% endapi-method-parameter %}

{% api-method-parameter name="interpret_document_mode_as_ie_version" type="boolean" required=false %}

If `true`, detects visitor’s Internet Explorer version using the
`document.documentMode` property. If `false`, it does not detect visitor's
Internet Explorer version.

{% endapi-method-parameter %}

{% api-method-parameter name="operator_console_omnibrowse" type="boolean" required=false %}

If `true` then it enables Call Visualizer in the Glia Hub. If `false` then it
disables Call Visualizer in the Glia Hub.

{% endapi-method-parameter %}

{% api-method-parameter name="reactive_tab" type="object" required=false %}

Customize the reactive bubble's aesthetics.

{% endapi-method-parameter %}

{% api-method-parameter name="visitor_page_adaption" type="string" required=false %}

Define the visitor's engagement mode, namely - `iframe`, `div`, `style`.

{% endapi-method-parameter %}

{% api-method-parameter name="salemove_enabled" type="boolean" required=false %}

If `true` then it enables Glia for the Site, if `false` it disables Glia for the
Site. When Glia is enabled the Glia integration is delivered otherwise a `204`
`No-Content` is delivered.

{% endapi-method-parameter %}

{% api-method-parameter name="map" type="object" required=false %}

An object with three possible attributes `latitude`, `longitude`, `zoom`.
Describes the platform console map center coordinate and the zoom level.

{% endapi-method-parameter %}

{% api-method-parameter name="store_data" type="boolean" required=false %}

If `true`, engagement chat transcripts of the site are stored. If `false`,
engagement chat transcripts of the site are not stored.

{% endapi-method-parameter %}

{% api-method-parameter name="allowed_file_senders" type="object" required=false %}

Allows sending file attachments in the chat from visitor to operator and/or
operator to visitor. E.g. `{operator: true, visitor: true}`.

{% endapi-method-parameter %}

{% api-method-parameter name="addresses" type="array" required=false %}

A list of Site’s addresses that are being updated. Addresses must be without
protocol prefixes and ports. Can be a domain name (`www.example.com`) to let
Glia run on all sites, or include path to restrict the access
(`www.example.com/home`).

{% endapi-method-parameter %}

{% api-method-parameter name="visitor_app_phone_extension_enabled" type="boolean" required=false %}

If `true` then phone extension input is shown alongside phone number input in
Visitor App.

{% endapi-method-parameter %}

{% api-method-parameter name="boot_delay_ms" type="integer" required=false %}

Delays the bootstrapping of Glia Visitor App by the given milliseconds. Delay
may be useful on very heavy sites.

{% endapi-method-parameter %}

{% api-method-parameter name="shortcuts_enabled" type="boolean" required=false %}

If `true`, keyboard shortcuts are enabled in the Glia Hub.

{% endapi-method-parameter %}

{% api-method-parameter name="phone_number_default_country" type="string" required=false %}

The country code that will be displayed by default when visitors enter their
phone number.

{% endapi-method-parameter %}

{% endapi-method-body-parameters %}

{% endapi-method-request %}

{% api-method-response %}

{% api-method-response-example httpCode=200 %}

```json
{
  "href": "https://api.local.dev/sites/24c9802c-3b95-4a15-b366-342b0a8289f7",
  "id": "24c9802c-3b95-4a15-b366-342b0a8289f7",
  "name": "example",
  "hostnames": [
    "example.local.dev",
    "example-eu.local.dev",
    "example-us.local.dev"
  ],
  "logo": {
    "url": "https://uploads.salemove.com/user_assets/site-3a5c1497-a0f8-470c-af10-c5c2b8fe88cc/site_logo-1539074994.png"
  },
  "default_operator_picture": {
    "url": "https://uploads.salemove.com/user_assets/site-3a5c1497-a0f8-470c-af10-c5c2b8fe88cc/site_default_operator_picture-1538999078.png"
  },
  "always_use_default_operator_picture": false,
  "widget_mode": true,
  "reactive_enabled": true,
  "reactive_call_timeout": 15,
  "proactive_enabled": true,
  "proactive_call_timeout": 15,
  "multi_engagement_enabled": true,
  "multi_engagement_default_availability": "retain",
  "multi_engagement_max_count": 5,
  "multi_engagement_idle_time": 20,
  "time_zone": "Europe/Tallinn",
  "missed_call_unavailability_enabled": true,
  "welcome_message": "Hello, how may I help you?",
  "visitor_user_agent_whitelist": ["user agent 1", "user agent 2"],
  "observation_enabled": true,
  "store_recording": true,
  "cobrowse_permission_required": true,
  "public_visitor_custom_attribute_changes_allowed": true,
  "interactive_cobrowsing_enabled": true,
  "allowed_login_ips": [
    {"address": "198.51.100.0/24"},
    {"address": "194.126.122.227"}
  ],
  "allowed_file_content_types": ["application/pdf", "image/png"],
  "video_in_call_visualizer": null,
  "store_file_attachments": true,
  "custom_code": "",
  "interpret_document_mode_as_ie_version": true,
  "operator_console_omnibrowse": true,
  "reactive_tab": {
    "contactWhenUnstaffed": true,
    "showUnavailable": true,
    "visibleOperatorCount": 3
  },
  "visitor_page_adaption": "div",
  "salemove_enabled": true,
  "map": {
    "latitude": 25.0,
    "longitude": 5.0,
    "zoom": 3
  },
  "store_data": true,
  "allowed_file_senders": {
    "operator": false,
    "visitor": false
  },
  "addresses": [
    "example.local.dev",
    "example-eu.local.dev",
    "example-us.local.dev"
  ],
  "visitor_app_phone_extension_enabled": false,
  "boot_delay_ms": 5,
  "shortcuts_enabled": true,
  "phone_number_default_country": "us"
}
```

{% endapi-method-response-example %}

{% endapi-method-response %}

{% endapi-method-spec %}

{% endapi-method %}

{% code-tabs %}

{% code-tabs-item title="cURL" %}

```bash
curl --request PUT \
    --header "Authorization: Bearer $access_token" \
    --header "Content-Type: application/json" \
    --header "Accept: application/vnd.salemove.v1+json" \
    --data-binary '{
      "salemove_enabled": true,
      "addresses": ["institution.com", "login.institution.com", "m.institution.com"],
      "default_operator_picture": "data:image/png;base64,iVBORw0KGgoAAA+Mg7SGKOzewAAAABJRU5ErkJggg==",
      "logo": "data:image/png;base64,iVBORw0KGgoAAA+Mg7SGKOzewAAAABJRU5ErkJggg==",
      "map": {
        "zoom": 3
      }
    }' \
    "https://api.salemove.com/sites/$site_id"
```

{% endcode-tabs-item %}

{% code-tabs-item title=undefined %}

```javascript
var XMLHttpRequest = require('xmlhttprequest').XMLHttpRequest;

var xhr = new XMLHttpRequest();

xhr.open('PUT', 'https://api.salemove.com/sites/$site_id', false);

xhr.setRequestHeader('authorization', `Bearer ${accessToken}`);
xhr.setRequestHeader('content-type', 'application/json');
xhr.setRequestHeader('accept', 'application/vnd.salemove.v1+json');

var data = {
  salemove_enabled: false,
  addresses: ['institution.com', 'login.institution.com', 'm.institution.com'],
  default_operator_picture:
    'data:image/png;base64,iVBORw0KGgoAAA+Mg7SGKOzewAAAABJRU5ErkJggg==',
  logo: 'data:image/png;base64,iVBORw0KGgoAAA+Mg7SGKOzewAAAABJRU5ErkJggg==',
  map: {
    zoom: 3
  }
};

var query = JSON.stringify(data);

xhr.send(query);

var response = JSON.parse(xhr.responseText);

console.log(response);
```

{% endcode-tabs-item %}

{% code-tabs-item title=undefined %}

```ruby
require 'httparty'

ENDPOINT = "https://api.salemove.com/sites"

token = ARGV[0].strip
site_id = ARGV[1].strip

headers = {
  :authorization => "Bearer #{access_token}",
  :content_type => "application/json",
  :accept => "application/vnd.salemove.v1+json"
}

options = {
  headers: headers,
  query: {
    "addresses": ["institution.com", "login.institution.com", "m.institution.com"],
    "default_operator_picture": "data:image/png;base64,iVBORw0KGgoAAA+Mg7SGKOzewAAAABJRU5ErkJggg==",
    "logo": "data:image/png;base64,iVBORw0KGgoAAA+Mg7SGKOzewAAAABJRU5ErkJggg==",
    "salemove_enabled": true,
    "map": {
      "zoom": 3
    }
  }
}

raw_response = HTTParty.put(
  "#{ENDPOINT}/#{site_id}",
  options
)

response = JSON.parse raw_response.body

puts response
```

{% endcode-tabs-item %}

{% endcode-tabs %}

## POST Create Site Application Token

{% code-tabs %}

{% code-tabs-item title="cURL" %}

```bash
curl --request POST \
     --header "Authorization: Bearer $access_token" \
     --header "Content-Type: application/json" \
     --header "Accept: application/vnd.salemove.v1+json" \
     --data-binary '{
       "site_id": "$site_id",
       "acls": ["omnibrowse:start_session"]
     }' \
     "https://api.salemove.com/application_tokens"
```

{% endcode-tabs-item %}

{% code-tabs-item title=undefined %}

```javascript
var XMLHttpRequest = require('xmlhttprequest').XMLHttpRequest;

var xhr = new XMLHttpRequest();

xhr.open('POST', 'https://api.salemove.com/application_tokens', false);

xhr.setRequestHeader('authorization', `Bearer ${accessToken}`);
xhr.setRequestHeader('content-type', 'application/json');
xhr.setRequestHeader('accept', 'application/vnd.salemove.v1+json');

var data = {
  site_id: site_id,
  acls: ['omnibrowse:start_session']
};

var query = JSON.stringify(data);

xhr.send(query);

var response = JSON.parse(xhr.responseText);

console.log(response);
```

{% endcode-tabs-item %}

{% code-tabs-item title=undefined %}

```ruby
require 'httparty'

token = ARGV[0].strip
site_id = ARGV[1].strip

raw_response = HTTParty.post(
  "https://api.salemove.com/application_tokens",
  headers: {
    'Authorization' => "Bearer #{access_token}",
    'Accept' => 'application/vnd.salemove.v1+json',
    'Content-Type' => 'application/json'
  },
  query: {
    "site_id": site_id,
    "acls": ["omnibrowse:start_session"]
  }
)

puts = JSON.parse(raw_response.body)
```

{% endcode-tabs-item %}

{% endcode-tabs %}

> Generates the output

```json
{
  "id": "2e56b224-6708-4755-b6c9-35f9889e42dd",
  "site_id": "275ba146-6053-41ef-bfc3-d7ae8d3d6494",
  "acls": ["omnibrowse:start_session"],
  "token": "38omYbnTZJL1Ugvn"
}
```

**Action:** `POST /application_tokens`

This request creates an application token for a site. Application tokens are
useful for integrating an external application with Glia. It allows creating new
site visitors, starting Call Visualizer sessions, etc. The user whose bearer
access token is used to send the request must have `super_manager` role on the
site.

| Parameter | Type   | Required | Description                                                 |
| :-------- | :----- | :------- | :---------------------------------------------------------- |
| `site_id` | String | Yes      | The site ID.                                                |
| `acls`    | Array  | Yes      | A list of access controls granted to the application token. |

**Access Control List:**

| Name                       | Description                                                                       |
| :------------------------- | :-------------------------------------------------------------------------------- |
| `visitors:create`          | Allows creating [new visitors](site_visitor.md#post-create-visitor) for the site. |
| `omnibrowse:start_session` | Allows starting a new [Call Visualizer](omnibrowse.md) session                    |
