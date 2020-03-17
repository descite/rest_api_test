# Get Operator

{% api-method method="get" host="https://api.salemove.com" path="/operators/{operator_id}" %}

{% api-method-summary %} Operator

{% endapi-method-summary %}

{% api-method-description %}

Fetches a configuration of specific user, who may have either the role of the
`operator`, `manager`, or `super_manager`. The caller must have access to the
site the fetched user belongs to.

{% endapi-method-description %}

{% api-method-spec %}

{% api-method-request %}

{% api-method-query-parameters %}

{% api-method-parameter name="include\_engagements" type="boolean" required=false %}
If `false`, does not include data for `engagements`, `engagement_requests` and
`engaged_since`. The default value is `true`.

{% endapi-method-parameter %}

{% endapi-method-query-parameters %}

{% endapi-method-request %}

{% api-method-response %}

{% api-method-response-example httpCode=200 %}

```json
{
  "last_page": "https://api.salemove.com/operators?page=1",
  "operators":
  [
    {
      "id": "f42811bc-8519-4d33-bbb1-36d4555ecb0a",
      "href": "https://api.salemove.com/operators/f42811bc-8519-4d33-bbb1-36d4555ecb0a",
      "name": "Jared Grey",
      "email": "jared.grey@institution.com",
      "available": true,
      "enabled": true,
      "reactive_enabled":true,
      "proactive_enabled":true,
      "observation_enabled":true
      "role": "operator",
      "picture": {
        "url": "https://uploads.salemove.com/user_assets/salemove_com-salemove_models_operator-6036d2ae-6c97-4555-83a2-bc8006b9acc8-jared_grey-f42811bc-8519-4d33-bbb1-36d4555ecb0a.png"
      },
      "audio_source": "phone",
      "phone": "+19174743334",
      "phone_extension": ",,1,23",
      "available_media_types": ["video", "audio", "chat"],
      "engaged_since": "2017-02-20T00:00:00Z",
      "engagements": [{
        "id": "eea868ad-9d58-4db9-a663-5fd766728980",
        "site_id": "7d5635b0-88ed-4109-8398-dcd151754640",
        "visitor_id": "1e1315aa-630e-4a13-a64b-1cdb034d3e0e",
        "operator_id": "f42811bc-8519-4d33-bbb1-36d4555ecb0a",
        "started_at": "2017-02-20T00:00:00Z",
        "audio_used": true,
        "video_used": false
      }],
      "engagement_requests": [
        {
          "visitor_id": "02cebb3a-7f7d-4be8-9445-911daa26ac1f",
          "site_id": "7d5635b0-88ed-4109-8398-dcd151754640",
          "created_at": "2017-02-20T00:00:00Z"
        },
        {
          "visitor_id": "45b595ae-48c3-401d-ae16-89ea1ab80119",
          "site_id": "7d5635b0-88ed-4109-8398-dcd151754640",
          "created_at": "2017-02-20T00:01:00Z"
        }
      ]
    },
    {
      "id": "c8b52f0b-ad05-4c71-8c98-5056f07c4d1a",
      "href": "https://api.salemove.com/operators/c8b52f0b-ad05-4c71-8c98-5056f07c4d1a",
      "name": "Jordan Green",
      "email": "jordan.green@institution.com",
      "available": false,
      "enabled": true,
      "reactive_enabled":true,
      "proactive_enabled":true,
      "observation_enabled":true
      "role": "operator",
      "picture": {
        "url": "https://uploads.salemove.com/user_assets/salemove_com-salemove_models_operator-c4ef4812-91e3-42cf-88d2-1f5bbbf144fd-jordan_green-c8b52f0b-ad05-4c71-8c98-5056f07c4d1a.jpg"
      },
      "audio_source": "sip_phone",
      "phone": "+13236654111",
      "sip_domain_id": "48e8b1bb-6ccb-431e-b15e-685500a5a45e",
      "sip_extension": "alice",
      "unavailability_reason": "offline",
      "unavailable_since": "2017-02-20T00:00:00Z",
      "available_media_types": [],
      "engagements": [],
      "engagement_requests": []
    }
  ]
}
```

{% endapi-method-response-example %}

{% endapi-method-response %}

{% endapi-method-spec %}

{% endapi-method %}

### Example request

{% code-tabs %}

{% code-tabs-item title="cURL" %}

```bash
curl --request GET \
    --header "Authorization: Bearer $access_token" \
    --header "Accept: application/vnd.salemove.v1+json" \
    "https://api.salemove.com/operators/$operator_id"
```

{% endcode-tabs-item %}

{% code-tabs-item title="JavaScript" %}

```javascript
var XMLHttpRequest = require('xmlhttprequest').XMLHttpRequest;

function getOperator(url) {
  var xhr = new XMLHttpRequest();
  xhr.open('GET', url, false);
  xhr.setRequestHeader('authorization', `Bearer ${accessToken}`);
  xhr.setRequestHeader('accept', 'application/vnd.salemove.v1+json');
  xhr.send();

  var response = JSON.parse(xhr.responseText);
  console.log(response);
}

for (page = 1; page <= last_page; page++) {
  var url = `https://api.salemove.com/operators/${operator_id}`;
  getOperator(url);
}
```

{% endcode-tabs-item %}

{% code-tabs-item title="Ruby" %}

```ruby
require 'httparty'

access_token = ARGV[0].strip
operator_id = ARGV[1].strip

headers = {
  :authorization => "Bearer #{access_token}",
  :accept => "application/vnd.salemove.v1+json"
}

raw_response = HTTParty.get(
  "https://api.salemove.com/operators/#{operator_id}",
  headers: headers
)

response = JSON.parse raw_response.body

puts response
```

{% endcode-tabs-item %}

{% endcode-tabs %}

### Output

<table>
  <thead>
    <tr>
      <th style="text-align:left">Field</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Required</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>id</code>
      </td>
      <td style="text-align:left"><code>string</code>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">ID or the user to be fetched (known as operator ID).</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>href</code>
      </td>
      <td style="text-align:left"><code>string</code>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">URI for the user.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>name</code>
      </td>
      <td style="text-align:left"><code>string</code>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">User's name.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>email</code>
      </td>
      <td style="text-align:left"><code>string</code>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">User's email.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>available</code>
      </td>
      <td style="text-align:left"><code>boolean</code>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">Whether the user is available or not.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>enabled</code>
      </td>
      <td style="text-align:left"><code>boolean</code>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left"><code>true</code>, if the user is not disabled.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>reactive_enabled</code></td>
      <td style="text-align:left"><code>boolean</code>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left"><code>true</code>, if the user is able to receive calls from visitors.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>proactive_enabled</code></td>
      <td style="text-align:left"><code>boolean</code>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">
        <p><code>true</code>, if the user is able to initiate engagements with
          visitors.</p>
        <p>If <code>false</code> then the user is still able to place outbound
          phone calls if the site configuration allows.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>observation_enabled</code></td>
      <td style="text-align:left"><code>boolean</code>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">If <code>true</code>, the user is able to observe visitors before engagements.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>role</code>
      </td>
      <td style="text-align:left"><code>string</code>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">User's role. Can be one of <code>operator</code>, <code>manager</code>, <code>super_manager</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>picture</code>
      </td>
      <td style="text-align:left"><code>object</code>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">User's picture. See <a href="picture.md">Picture</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>audio_source</code></td>
      <td style="text-align:left"><code>string</code></td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">The audio device used for audio calls. One of
        <code>computer</code> or <code>phone</code> or <code>sip_phone</code>. Default
        value is <code>computer</code>. Additional audio sources may be added in
        the future.
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>phone</code>
      </td>
      <td style="text-align:left"><code>string</code>
      </td>
      <td style="text-align:left">Yes if <code>audio_source</code> is
        <code>phone</code>.
      </td>
      <td style="text-align:left">User's phone number.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>phone_extension</code>
      </td>
      <td style="text-align:left"><code>string</code>
      </td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">User's phone number extension.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>sip_domain_id</code></td>
      <td style="text-align:left"><code>string</code></td>
      <td style="text-align:left">Yes if <code>audio_source</code> is
        <code>sip_phone</code>.
      </td>
      <td style="text-align:left">The ID of the
        <a href="../../omnicall/create-sip-domain.md">SIP domain</a> used for
        SIP calls.
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>sip_extension</code></td>
      <td style="text-align:left"><code>string</code></td>
      <td style="text-align:left">Yes if <code>audio_source</code> is
        <code>sip_phone</code>.
      </td>
      <td style="text-align:left">The SIP extension of the user.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>unavailability_reason</code>
      </td>
      <td style="text-align:left"><code>string</code>
      </td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">User's unavailability reason.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>unavailable_since</code>
      </td>
      <td style="text-align:left"><code>string</code>
      </td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">An ISO-8601 timestamp of when the user first went unavailable. Changing
        the unavailable status from one to another does not reset this.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>available_media_types</code>
      </td>
      <td style="text-align:left"><code>array</code>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">A list of media types the user is available for. Can contain <code>video</code>, <code>audio</code>, <code>chat</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>engaged_since</code>
      </td>
      <td style="text-align:left"><code>string</code>
      </td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">An ISO-8601 timestamp of when the user first started an engagement.
        In case of multiple engagements, this is the start time of the first engagement
        even if the first engagement has ended. When the user is not engaged, this
        field will not be present.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>engagements</code>
      </td>
      <td style="text-align:left"><code>array</code>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">A list of ongoing engagements. See <a href="engagements/engagements.md">Engagements</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>engagement_requests</code>
      </td>
      <td style="text-align:left"><code>array</code>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">A list of ongoing engagement requests. See <a href="engagement-requests.md">Engagement Request</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>max_engagement_count</code>
      </td>
      <td style="text-align:left"><code>integer</code>
      </td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">Maximum concurrent engagement count allowed for the user.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>multi_engagement_default_availability</code>
      </td>
      <td style="text-align:left"><code>string</code>
      </td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">Availability behaviour when user has multi-engagement enabled.</td>
    </tr>
  </tbody>
</table>
