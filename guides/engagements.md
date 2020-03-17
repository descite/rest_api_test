# Engagements

{% api-method method="get" host="https://api.salemove.com" path="/engagements" %}

{% api-method-summary %} Engagements

{% endapi-method-summary %}

{% api-method-description %}

Adding here to line to see if Stoplight will auto-update the content.

Fetches a collection of engagements and related data. The results are paginated,
and sorted by `start_date` in descending order.<br><br>

The response payload includes `next_page` link which can be used to get next
batch of engagements. If the `next_page` is null then there are no more
engagements. This link must not be parsed as it is automatically generated and
can change at any time.

{% endapi-method-description %}

{% api-method-spec %}

{% api-method-request %}

{% api-method-headers %}

{% api-method-parameter name="Authorization" type="string" required=true %}

Used to authenticate the user. Only `Bearer` access token is allowed.

{% endapi-method-parameter %}

{% api-method-parameter name="Accept" type="string" required=true %}

Must be `application/vnd.salemove.v1+json`

{% endapi-method-parameter %}

{% endapi-method-headers %}

{% api-method-query-parameters %}

{% api-method-parameter name="site\_ids" type="array" required=true %}

A list of site IDs whose engagements are requested. The requester must be
authorized to access the provided sites.

{% endapi-method-parameter %}

{% api-method-parameter name="operator\_ids" type="array" required=false %}

A list of operator IDs whose engagements are requested. If the requester is a
`manager` on the sites, the `operator_ids` filter can be either omitted or be an
empty array to query engagements conducted by any operator. If the requester is
not a `manager`, they must specify their own ID in `operator_ids` filter.

{% endapi-method-parameter %}

{% api-method-parameter name="start\_date" type="string" required=false %}

The response will include engagements that happened from `start_date` forward in
time.

{% endapi-method-parameter %}

{% api-method-parameter name="end\_date" type="string" required=false %}

The response will include engagements that happened on or before the `end_date`
and after the `start_date`.

{% endapi-method-parameter %}

{% api-method-parameter name="per\_page" type="number" required=false %}

If pagination is used then this parameter specifies the number of engagements
per page.

{% endapi-method-parameter %}

{% api-method-parameter name="order" type="string" required=false %}

Specifies whether the results should be sorted in ascending \(`asc`\) or
descending \(`desc`\) order. By default, engagements are sorted by their start
time in descending order.

{% endapi-method-parameter %}

{% endapi-method-query-parameters %}

```bash
curl --request GET \
     --header "Authorization: Bearer $access_token" \
     --header "Accept: application/vnd.salemove.v1+json" \
     "https://api.salemove.com/engagements?operator_ids\[\]=$operator_id&site_ids\[\]=$site_id&start_date=2017-01-01T00:00:00Z"
```

{% endapi-method-request %}

{% api-method-response %}

{% api-method-response-example httpCode=200 %}

```json
{
  "next_page": "https://api.salemove.com/engagements?per_page=30&cursor=45629133",
  "engagements": [
    {
      "id": "eea868ad-9d58-4db9-a663-5fd766728980",
      "engagement_type": "proactive",
      "created_at": "2017-07-07T13:47:21.150Z",
      "duration": 10,
      "visitor_name": "Sasha Brown",
      "visitor_browser": "Chrome",
      "visitor_device_type": "mobile",
      "visitor_id": "039124e6-b4e8-4a0d-b420-5b6696c7ecb4",
      "cobrowsing_used": true,
      "video_used": true,
      "audio_used": true,
      "flagged": false,
      "queue_wait_time": 42,
      "platform": "omnicore",
      "audio_recording_urls": [
        "https://api.salemove.com/sub_engagements/1122834/recordings/XaMiTQI"
      ],
      "crm_forwarded": false,
      "summary_forwarded": false,
      "visitor": {
        "href": "https://api.salemove.com/visitors/039124e6-b4e8-4a0d-b420-5b6696c7ecb4"
      },
      "chat_transcript": {
        "href": "https://api.salemove.com/engagements/eea868ad-9d58-4db9-a663-5fd766728980/chat_transcript"
      },
      "operators": [
        {
          "href": "https://api.salemove.com/operators/f42811bc-8519-4d33-bbb1-36d4555ecb0a"
        }
      ],
      "queues": [
        {
          "id": "82af2b5d-4ea5-40c8-bab2-a87d39598a81",
          "name": "Queue name"
        }
      ]
    },
    {
      "id": "dc71edb4-9c54-4ead-9d03-4c31a69315be",
      "engagement_type": "reactive",
      "created_at": "2017-07-06T11:46:37.569Z",
      "duration": 1,
      "visitor_name": "Visitor #6",
      "visitor_browser": "Firefox",
      "visitor_device_type": "desktop",
      "visitor_id": "41fb129c-fd0c-4f8b-8ca5-657787917c4b",
      "cobrowsing_used": false,
      "video_used": false,
      "flagged": false,
      "audio_recording_urls": [
        "https://api.salemove.com/sub_engagements/1120220/twilio_recordings/4994"
      ],
      "crm_forwarded": false,
      "summary_forwarded": true,
      "queue_wait_time": 10,
      "platform": "omnicore",
      "visitor": {
        "href": "https://api.salemove.com/visitors/41fb129c-fd0c-4f8b-8ca5-657787917c4b"
      },
      "source": "tab",
      "chat_transcript": {
        "href": "https://api.salemove.com/engagements/dc71edb4-9c54-4ead-9d03-4c31a69315be/chat_transcript"
      },
      "operators": [
        {
          "href": "https://api.salemove.com/operators/c8b52f0b-ad05-4c71-8c98-5056f07c4d1a"
        }
      ],
      "queues": [
        {
          "id": "82af2b5d-4ea5-40c8-bab2-a87d39598a81",
          "name": "Queue name"
        }
      ]
    },
    {
      "id": "c0828e2e-3e29-4881-8dcc-3d96563a68fe",
      "engagement_type": "proactive",
      "created_at": "2017-07-06T11:23:54.508Z",
      "duration": 330,
      "visitor_name": "Jordan Green",
      "visitor_browser": "Chrome",
      "visitor_device_type": "mobile",
      "visitor_id": "41fb129c-fd0c-4f8b-8ca5-657787917c4b",
      "cobrowsing_used": true,
      "video_used": false,
      "audio_used": false,
      "flagged": false,
      "audio_recording_urls": [],
      "crm_forwarded": false,
      "summary_forwarded": true,
      "platform": "omnicore",
      "visitor": {
        "href": "https://api.salemove.com/visitors/41fb129c-fd0c-4f8b-8ca5-657787917c4b"
      },
      "chat_transcript": {
        "href": "https://api.salemove.com/engagements/c0828e2e-3e29-4881-8dcc-3d96563a68fe/chat_transcript"
      },
      "operators": [
        {
          "href": "https://api.salemove.com/operators/f42811bc-8519-4d33-bbb1-36d4555ecb0a"
        }
      ]
    }
  ]
}
```

{% endapi-method-response-example %}

{% endapi-method-response %}

{% endapi-method-spec %}

{% endapi-method %}

{% api-method method="get" host="https://api.salemove.com" path="/engagements/{engagement_id}" %}

{% api-method-summary %} Engagement

{% endapi-method-summary %}

{% api-method-description %}

Fetches a single engagement by `engagement_id`. The user whose credentials are
contained in the `Authorization` request header must be authorized to access the
site on which the engagement occurred. <br><br>

**Note:** Due to post-processing, audio recordings are available shortly after
an engagement ends. <br><br>

In a case where the recording URL is immediately fulfilled with recording,
requesting a URL provided by the response in `audio_recording_urls` will
generate and return a temporary URL to the recording file. The generated URL
expires in 15 minutes. <br><br>

In a case where the recording is not yet available due to post-processing, a
`GET` request for a recording URL will return `204 No Content`.

{% endapi-method-description %}

{% api-method-spec %}

{% api-method-request %}

{% api-method-headers %}

{% api-method-parameter name="Authorization" type="string" required=true %}

Used to authenticate the user. Only `Bearer` access token is allowed.

{% endapi-method-parameter %}

{% api-method-parameter name="Accept" type="string" required=true %}

Must be `application/vnd.salemove.v1+json`

{% endapi-method-parameter %}

{% endapi-method-headers %}

{% api-method-path-parameters %}

{% api-method-parameter name="engagement\_id" type="string" required=true %}
Engagement ID

{% endapi-method-parameter %}

{% endapi-method-path-parameters %}

{% code-tabs %}

{% code-tabs-item title="cURL" %}

```bash
curl --request GET \
     --header "Authorization: Bearer $access_token" \
     --header "Accept: application/vnd.salemove.v1+json" \
     "https://api.salemove.com/engagements/$engagement_id"
```

{% endcode-tabs-item %}

{% code-tabs-item title="JavaScript" %}

```javascript
var XMLHttpRequest = require('xmlhttprequest').XMLHttpRequest;

var xhr = new XMLHttpRequest();
xhr.open('GET', `https://api.salemove.com/engagements/${engagement_id}`, false);
xhr.setRequestHeader('authorization', `Bearer ${accessToken}`);
xhr.setRequestHeader('accept', 'application/vnd.salemove.v1+json');
xhr.send();

var response = JSON.parse(xhr.responseText);
console.log(response);
```

{% endcode-tabs-item %}

{% code-tabs-item title="Ruby" %}

```ruby
require 'httparty'

response = HTTParty.get(
  "https://api.salemove.com/engagements/#{engagement_id}"
  headers: {
    'Authorization' => "Bearer #{access_token}",
    'Accept' => "application/vnd.salemove.v1+json"
  }
)
puts response.body
```

{% endcode-tabs-item %}

{% endcode-tabs %}

{% endapi-method-request %}

{% api-method-response %}

{% api-method-response-example httpCode=200 %}

```json
{
  "id": "eea868ad-9d58-4db9-a663-5fd766728980",
  "engagement_type": "reactive",
  "created_at": "2017-07-07T13:47:21.150Z",
  "duration": 268,
  "visitor_name": "Sasha Brown",
  "visitor_browser": "Chrome",
  "visitor_device_type": "mobile",
  "visitor_id": "039124e6-b4e8-4a0d-b420-5b6696c7ecb4",
  "cobrowsing_used": true,
  "video_used": true,
  "audio_used": true,
  "flagged": false,
  "queue_wait_time": 42,
  "platform": "omnicore",
  "audio_recording_urls": [
    "https://api.salemove.com/sub_engagements/1122834/recordings/XaMiTQI"
  ],
  "crm_forwarded": false,
  "summary_forwarded": false,
  "visitor": {
    "href": "https://api.salemove.com/visitors/039124e6-b4e8-4a0d-b420-5b6696c7ecb4"
  },
  "chat_transcript": {
    "href": "https://api.salemove.com/engagements/eea868ad-9d58-4db9-a663-5fd766728980/chat_transcript"
  },
  "operators": [
    {
      "href": "https://api.salemove.com/operators/f42811bc-8519-4d33-bbb1-36d4555ecb0a"
    },
    {
      "href": "https://api.salemove.com/operators/0fca6673-1938-4a1f-a72e-262c19700ab6"
    }
  ],
  "queues": [
    {
      "id": "82af2b5d-4ea5-40c8-bab2-a87d39598a81",
      "name": "Queue name"
    }
  ],
  "legs": [
    {
      "id": "78cb0e78-c995-461c-8659-d2364025a33e",
      "operator": {
        "id": "f42811bc-8519-4d33-bbb1-36d4555ecb0a"
      },
      "site": {
        "id": "9dd25b48-c988-48cd-a4c3-56384d317e41"
      },
      "requested_at": "2017-07-07T13:47:10.000Z",
      "accepted_at": "2017-07-07T13:47:21.150Z",
      "request_type": "reactive",
      "request_source": "tab",
      "offered_media_type": "video",
      "accepted_media_type": "text",
      "request_queues": [
        {"id": "82af2b5d-4ea5-40c8-bab2-a87d39598a81", "name": "Queue name"}
      ],
      "duration": 109,
      "highest_visitor_media_type": "text",
      "highest_operator_media_type": "text",
      "used_cobrowsing": false,
      "ended_at": "2017-07-07T13:49:10.150Z",
      "end_reason": "transfer"
    },
    {
      "id": "6a33a95a-472b-433d-b107-b1c5426e6865",
      "operator": {
        "id": "0fca6673-1938-4a1f-a72e-262c19700ab6"
      },
      "site": {
        "id": "9dd25b48-c988-48cd-a4c3-56384d317e41"
      },
      "requested_at": "2017-07-07T13:48:55.000Z",
      "accepted_at": "2017-07-07T13:49:10.150Z",
      "request_type": "transfer",
      "request_source": null,
      "offered_media_type": "text",
      "accepted_media_type": "text",
      "request_queues": null,
      "duration": 158,
      "highest_visitor_media_type": "video",
      "highest_operator_media_type": "audio",
      "used_cobrowsing": true,
      "ended_at": "2017-07-07T13:51:48.150Z",
      "end_reason": "visitor_left"
    }
  ]
}
```

{% endapi-method-response-example %}

{% endapi-method-response %}

{% endapi-method-spec %}

{% endapi-method %}

> Output fields

| Field                  | Type    | Required | Description                                                                                                                                                                                               |
| :--------------------- | :------ | :------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                   | String  | Yes      | Engagement ID.                                                                                                                                                                                            |
| `engagement_type`      | String  | Yes      | Engagement type. Can be one of `proactive`, `reactive`.                                                                                                                                                   |
| `created_at`           | String  | Yes      | An ISO-8601 timestamp of when the engagement request was created.                                                                                                                                         |
| `duration`             | Integer | Yes      | Engagement duration in seconds.                                                                                                                                                                           |
| `visitor_name`         | String  | Yes      | Visitor's name.                                                                                                                                                                                           |
| `visitor_browser`      | String  | Yes      | Visitor's browser.                                                                                                                                                                                        |
| `visitor_device_type`  | String  | Yes      | Visitor's device type.                                                                                                                                                                                    |
| `visitor_id`           | String  | Yes      | Visitor ID.                                                                                                                                                                                               |
| `cobrowsing_used`      | Boolean | Yes      | Whether CoBrowsing was used or not.                                                                                                                                                                       |
| `video_used`           | Boolean | Yes      | Whether video was used or not.                                                                                                                                                                            |
| `audio_used`           | Boolean | Yes      | Whether audio was used or not.                                                                                                                                                                            |
| `flagged`              | Boolean | Yes      | Whether the engagement has been flagged or not.                                                                                                                                                           |
| `queue_wait_time`      | Integer | No       | The time visitor spent in queue before the engagement, in seconds. This value is present only for reactive engagements started via queueing.                                                              |
| `audio_recording_urls` | Array   | Yes      | A list of audio recordings URLs.                                                                                                                                                                          |
| `crm_forwarded`        | Boolean | Yes      | Whether the CRM Export has already occurred or not.                                                                                                                                                       |
| `summary_forwarded`    | Boolean | Yes      | Whether the summary has already been forwarded.                                                                                                                                                           |
| `platform`             | String  | Yes      | The platform where the engagement was initiated. Possible values are: `omnibrowse` - engagement was requested from Call Visualizer (either in Glia Hub or embedded in CRM), `omnicore` - all other cases. |
| `visitor`              | Object  | Yes      | See [Visitor](engagements.md#visitor).                                                                                                                                                                    |
| `chat_transcript`      | Object  | Yes      | Engagement chat transcript. See [Chat Transcript](engagements.md#chat-transcript).                                                                                                                        |
| `operators`            | Array   | Yes      | A list of engagement operators. See [Operators](engagements.md#operators).                                                                                                                                |
| `source`               | String  | No       | One of [Engagement Sources](engagements.md#engagement-sources).                                                                                                                                           |
| `queues`               | Array   | No       | A list of queues that the visitor was enqueued in before starting the engagement. This value is present only for reactive engagements started via queueing. See [Queues](engagements.md#queues).          |
| `legs`                 | Array   | Yes      | A list of engagement legs. Engagement starts with one leg. A leg is added each time the engagement is transferred. See [Engagement Leg](engagements.md#engagement-leg).                                   |

#### Visitor

| Field  | Type   | Required | Description                       |
| :----- | :----- | :------- | :-------------------------------- |
| `href` | String | Yes      | URL of the visitor's information. |

#### Chat Transcript

| Field  | Type   | Required | Description                            |
| :----- | :----- | :------- | :------------------------------------- |
| `href` | String | Yes      | URL of the engagement chat transcript. |

#### Operators

| Field  | Type   | Required | Description                        |
| :----- | :----- | :------- | :--------------------------------- |
| `href` | String | Yes      | URL of the operator's information. |

#### Engagement Sources

| Engagement source    | Engagement type | Description                                                                                                                                                                                                                 |
| :------------------- | :-------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `button_embed`       | `reactive`      | Engagement started via [Contact Operator Button](../html_css.md#contact-operator-button).                                                                                                                                   |
| `callout`            | `reactive`      | Engagement started via business rules. E.g. a business rule triggered a media selector which was then used to start the engagement.                                                                                         |
| `external_call`      | `reactive`      | \[Deprecated\]                                                                                                                                                                                                              |
| `facebook`           | `reactive`      | Visitor sent message from Facebook Messenger.                                                                                                                                                                               |
| `hotlink`            | `reactive`      | Engagement started via [hotlink](../html_css.md#hotlinks).                                                                                                                                                                  |
| `offline_phone`      | `reactive`      | Visitor called a phone number.                                                                                                                                                                                              |
| `outbound_call`      | `proactive`     | Operator called visitor's phone.                                                                                                                                                                                            |
| `outbound_text`      | `proactive`     | SMS message was sent to visitor's phone.                                                                                                                                                                                    |
| `sdk`                | `reactive`      | Engagement started using the [JS SDK](https://js-sdk-docs.salemove.com/class/Salemove.html#requestEngagement-dynamic), [Android SDK](http://android-sdk-docs.glia.com/javadoc) or [iOS SDK](https://ios-docs.glia.com/api). |
| `slack`              | `reactive`      | Engagement started via Slack.                                                                                                                                                                                               |
| `sms`                | `reactive`      | Visitor sent SMS message.                                                                                                                                                                                                   |
| `tab`                | `reactive`      | Engagement started in the browser tab (via the bubble).                                                                                                                                                                     |
| `visitor_integrator` | `reactive`      | Engagement started by [REST API](../engagement_requests.md#visitors-from-external-systems-salemove-integrators) call.                                                                                                       |
| `whatsapp`           | `reactive`      | Visitor sent message from WhatsApp.                                                                                                                                                                                         |
| `<empty>`            | `proactive`     | Engagement was requested by the operator.                                                                                                                                                                                   |

#### Engagement Leg

| Field                         | Type      | Description                                                                                                                                    |
| :---------------------------- | :-------- | :--------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                          | `string`  | Engagement leg ID.                                                                                                                             |
| `operator`                    | `object`  | Operator information.                                                                                                                          |
| `site`                        | `object`  | Site information.                                                                                                                              |
| `requested_at`                | `string`  | Engagement or transfer request ISO-8601 timestamp.                                                                                             |
| `accepted_at`                 | `string`  | Engagement or transfer accept ISO-8601 timestamp.                                                                                              |
| `request_type`                | `string`  | Request type. Possible values are `reactive`, `proactive`, and `transfer`.                                                                     |
| `request_source`              | `string`  | Request [source](../../engagements.md#engagement-sources).                                                                                     |
| `offered_media_type`          | `string`  | Engagement offered or requested media type. Possible values are `text`, `audio`, `phone` and `video`.                                          |
| `accepted_media_type`         | `string`  | Engagement accepted media type. Possible values are `text`, `audio`, `phone` and `video`.                                                      |
| `request_queues`              | `array`   | Engagement or transfer request queues. NULL if queues were not used.                                                                           |
| `duration`                    | `integer` | Engagement Leg duration in seconds.                                                                                                            |
| `highest_visitor_media_type`  | `string`  | Highest media type visitor used during this Engagement Leg. Possible values are `text`, `audio` and `video`.                                   |
| `highest_operator_media_type` | `string`  | Highest media type operator used during this Engagement Leg. Possible values are `text`, `audio` and `video`.                                  |
| `used_cobrowsing`             | `boolean` | True if cobrowsing was used during the engagement, otherwise false.                                                                            |
| `ended_at`                    | `string`  | ISO-8601 timestamp when engagement was ended or when engagement was transferred out.                                                           |
| `end_reason`                  | `string`  | Engagement Leg end reason. Possible values are `visitor_left`, `visitor_hung_up`, `operator_left`, `operator_hung_up`, `error` and `transfer`. |

#### Queues

| Field  | Type   | Required | Description |
| :----- | :----- | :------- | :---------- |
| `id`   | String | Yes      | Queue ID.   |
| `name` | String | Yes      | Queue name. |

{% api-method method="patch" host="https://api.salemove.com" path="/engagements/{engagement_id}" %}

{% api-method-summary %} End Engagement {% endapi-method-summary %}

{% api-method-description %}

Ends the engagement. Only a current participant of an engagement can _end_ it,
if the engagement was transferred then the operator prior to the transfer is not
allowed to end the engagement. If the participant application suffered an error
when starting the engagement, provide 'error' as the 'reason' for ending the
engagement to distinguish such failures from engagement ending normally.

{% endapi-method-description %}

{% api-method-spec %}

{% api-method-request %}

{% api-method-path-parameters %}

{% api-method-parameter name="engagement\_id" type="string" required=true %}
Engagement ID

{% endapi-method-parameter %}

{% endapi-method-path-parameters %}

{% api-method-headers %}

{% api-method-parameter name="Authorization" type="string" required=true %}

Used to authenticate the user. Only `Bearer` access token is allowed.

{% endapi-method-parameter %}

{% api-method-parameter name="Accept" type="string" required=true %} Must be
`application/vnd.salemove.v1+json`

{% endapi-method-parameter %}

{% api-method-parameter name="Content-Type" type="string" required=true %} Must
be `application/json`

{% endapi-method-parameter %}

{% endapi-method-headers %}

{% api-method-body-parameters %}

{% api-method-parameter name="action" type="string" required=true %} Must be
`end`.

{% endapi-method-parameter %}

{% api-method-parameter name="reason" type="string" required=false %} Must be
`error`.

{% endapi-method-parameter %}

{% endapi-method-body-parameters %}

{% code-tabs %}

{% code-tabs-item title="cURL" %}

```bash
curl --request PATCH \
     --header "Authorization: Bearer $access_token" \
     --header "Accept: application/vnd.salemove.v1+json" \
     --header "Content-Type: application/json" \
     --data-binary '{"action": "end"}' \
     "https://api.salemove.com/engagements/$engagement_id"
```

{% endcode-tabs-item %}

{% code-tabs-item title="JavaScript" %}

```javascript
var XMLHttpRequest = require('xmlhttprequest').XMLHttpRequest;

var xhr = new XMLHttpRequest();
xhr.open(
  'PATCH',
  `https://api.salemove.com/engagements/${engagement_id}`,
  false
);
xhr.setRequestHeader('authorization', `Bearer ${accessToken}`);
xhr.setRequestHeader('accept', 'application/vnd.salemove.v1+json');
xhr.setRequestHeader('content-type', 'application/json');
xhr.send(JSON.stringify({action: 'end'}));

var response = JSON.parse(xhr.responseText);
console.log(response);
```

{% endcode-tabs-item %}

{% code-tabs-item title="Ruby" %}

```ruby
require 'httparty'

response = HTTParty.patch(
  "https://api.salemove.com/engagements/#{engagement_id}",
  headers: {
    'Authorization' => "Bearer #{access_token}",
    'Accept' => 'application/vnd.salemove.v1+json',
    'Content-Type' => 'application/json'
  },
  query: {
    action: 'end'
  }
)
puts response.body
```

{% endcode-tabs-item %}

{% endcode-tabs %}

{% endapi-method-request %}

{% api-method-response %}

{% api-method-response-example httpCode=200 %}

```json
{
  "id": "59b0d786-e59a-4c62-a064-05e4f47488a2",
  "sub_engagement_id": "aa4fe613-298b-4556-98ba-150250edf10b"
}
```

{% endapi-method-response-example %}

{% endapi-method-response %}

{% endapi-method-spec %}

{% endapi-method %}

{% api-method method="post" host="https://api.salemove.com" path="/engagements/{engagement_id}/export" %}

{% api-method-summary %} Export Engagement {% endapi-method-summary %}

{% api-method-description %}

Exports the identified engagement. The format and destination of the export are
specified by the
[configuration](https://support.salemove.com/hc/en-us/articles/235631168-Configuring-Export-Content)
of the site on which the engagement began. The user whose credentials are
contained in the `Authorization` request header must be authorized to access the
site on which the identified engagement occurred. If the engagement is
transferred to other sites, and the requesting operator does not have access to
all of them, then the export will contain only the data that belongs to the
site\(s\) for which the operator is authorized.

{% endapi-method-description %}

{% api-method-spec %}

{% api-method-request %}

{% api-method-headers %}

{% api-method-parameter name="Authorization" type="string" required=true %}

Used to authenticate the user. Only `Bearer` access token is allowed.

{% endapi-method-parameter %}

{% api-method-parameter name="Accept" type="string" required=true %}

Must be `application/vnd.salemove.v1+json`

{% endapi-method-parameter %}

{% api-method-parameter name="Content-Type" type="string" required=true %}

Must be `application/json`

{% endapi-method-parameter %}

{% endapi-method-headers %}

{% api-method-path-parameters %}

{% api-method-parameter name="engagement\_id" type="string" required=true %}
Engagement ID

{% endapi-method-parameter %}

{% endapi-method-path-parameters %}

{% code-tabs %}

{% code-tabs-item title="cURL" %}

```bash
curl --request POST \
     --header "Authorization: Bearer $access_token" \
     --header "Content-Type: application/json" \
     --header "Accept: application/vnd.salemove.v1+json" \
     "https://api.salemove.com/engagements/$engagement_id/export"
```

{% endcode-tabs-item %}

{% code-tabs-item title="JavaScript" %}

```javascript
var XMLHttpRequest = require('xmlhttprequest').XMLHttpRequest;

var xhr = new XMLHttpRequest();
xhr.open(
  'POST',
  'https://api.salemove.com/engagements/$engagement_id/export',
  false
);
xhr.setRequestHeader('authorization', `Bearer ${accessToken}`);
xhr.setRequestHeader('content-type', 'application/json');
xhr.setRequestHeader('accept', 'application/vnd.salemove.v1+json');
xhr.send();

var response = JSON.parse(xhr.responseText);
console.log(response);
```

{% endcode-tabs-item %}

{% code-tabs-item title="Ruby" %}

```ruby
require 'httparty'

response = HTTParty.post(
  "https://api.salemove.com/engagements/#{engagement_id}/export",
  headers: {
    'Authorization' => "Bearer #{access_token}",
    'Content-Type' => "application/json",
    'Accept' => 'application/vnd.salemove.v1+json'
  }
)
puts response.body
```

{% endcode-tabs-item %}

{% endcode-tabs %}

{% endapi-method-request %}

{% api-method-response %}

{% api-method-response-example httpCode=200 %}

```json
{"success": true}
```

{% endapi-method-response-example %}

{% endapi-method-response %}

{% endapi-method-spec %}

{% endapi-method %}

{% api-method method="get" host="https://api.salemove.com" path="/engagements/queue/wait_duration" %}

{% api-method-summary %} Fetch Queue Average Wait Duration

{% endapi-method-summary %}

{% api-method-description %}

Fetches the average duration that other visitors on the same site have had to
wait in the queue. This value can be used to estimate the waiting time for the
current visitor if they were to request an engagement. The average value is
calculated from all wait times observed between now and some time in the past,
where how far back it goes is configurable per site.

{% endapi-method-description %}

{% api-method-spec %}

{% api-method-request %}

{% api-method-headers %}

{% api-method-parameter name="Authorization" type="string" required=true %}

Used to authenticate the visitor. Only `Bearer` access token is allowed.

{% endapi-method-parameter %}

{% api-method-parameter name="Accept" type="string" required=true %}

Must be `application/vnd.salemove.v1+json`

{% endapi-method-parameter %}

{% endapi-method-headers %}

{% code-tabs %}

{% code-tabs-item title="cURL" %}

```bash
curl --request GET \
     --header "Authorization: Bearer $access_token" \
     --header "Accept: application/vnd.salemove.v1+json" \
     "https://api.salemove.com/engagements/queue/wait_duration"
```

{% endcode-tabs-item %}

{% endcode-tabs %}

{% endapi-method-request %}

{% api-method-response %}

{% api-method-response-example httpCode=200 %}

```json
{
  "average_duration_in_seconds": 122
}
```

{% endapi-method-response-example %}

{% endapi-method-response %}

{% endapi-method-spec %}

{% endapi-method %}
