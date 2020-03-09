# Update an Operator

**Action:** `POST /operators/{operator_id}`

Updates the user's settings. The caller must have at least the role `manager`.
The following parameters can be sent along with the request:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">name</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The name of the user.</td>
    </tr>
    <tr>
      <td style="text-align:left">email</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The email of the user. It must be unique.</td>
    </tr>
    <tr>
      <td style="text-align:left">audio_source</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The audio device used for audio calls. One of
        <code>computer</code> or <code>phone</code> or <code>sip_phone</code>. Default
        value is <code>computer</code>. Additional audio sources may be added in
        the future.
      </td>
    </tr>
    <tr>
      <td style="text-align:left">phone</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The phone number of the user. The supported format is
        <a href="https://js-sdk-docs.salemove.com/extra/glossary.md.html#phone-numbers">E.164</a>.
        Must be set if <code>audio_source</code> is <code>phone</code>.
      </td>
    </tr>
    <tr>
      <td style="text-align:left">phone_extension</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The phone number extension of the user. A valid
        extension contains 1-7 digits and any number of <code>,</code> characters.
        There is an initial two second delay time before the first extension
        character is processed. Each <code>,</code> character in the extension
        adds a two second wait time before the next character is processed.
        Maximum length is 25 characters. Valid only if <code>phone</code> is also
        set or was set beforehand.
      </td>
    </tr>
    <tr>
      <td style="text-align:left">sip_domain_id</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The ID of the
        <a href="../omnicall/create-sip-domain.md">SIP domain</a> used for SIP
        calls. Must be set if <code>audio_source</code> is <code>sip_phone</code>.
      </td>
    </tr>
    <tr>
      <td style="text-align:left">sip_extension</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The SIP extension of the user. Maximum
        length is 30 characters. An <a href="https://tools.ietf.org/html/rfc3261#section-25.1">RFC3261</a>
        compliant format is supported. Valid only if <code>sip_domain_id</code>
        is also set or was set beforehand. Must be set if
        <code>audio_source</code> is <code>sip_phone</code>.
      </td>
    </tr>
    <tr>
      <td style="text-align:left">enabled</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">Enables (when the value of the parameter is <code>true</code>) or disables
        (when the value of the parameter is <code>false</code>) the user&apos;s
        use of the platform.</td>
    </tr>
    <tr>
      <td style="text-align:left">available</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">Sets engagement availability. <code>true</code> indicates that the user
        is available for a new engagement. <code>false</code> indicates that the
        user is unavailable for a new engagement.</td>
    </tr>
    <tr>
      <td style="text-align:left">assignments</td>
      <td style="text-align:left">array</td>
      <td style="text-align:left">An array of user <a href="common-objects/assignment.md">Assignments</a>.
        The provided array of <a href="common-objects/assignment.md">Assignments</a> will
        replace the existing ones. Specifying an empty array returns a validation
        error as at least one Site needs to remain assigned to the user being
        updated.</td>
    </tr>
    <tr>
      <td style="text-align:left">max_engagement_count</td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">Maximum number of concurrent engagements allowed for this user. If
        omitted, minimum allowed engagement count from assigned Sites configuration
        will be used.</td>
    </tr>
    <tr>
      <td style="text-align:left">multi_engagement_default_availability</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Availability behaviour when user engages and multi-engagement is allowed.
        Allowed values are <code>unavailable</code> - user is set to be unavailable, <code>chat</code> -
        user availability is set to chat media, <code>retain</code> - previous
        availability is retained. If omitted, value from the assigned Site configuration
        will be used.</td>
    </tr>
    <tr>
      <td style="text-align:left">reactive_enabled</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">
        <p>If <code>true</code>, the operator is able to receive calls from visitors.</p>
        <p><code>true</code> by default.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">proactive_enabled</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">
        <p>If <code>true</code>, the operator is able to initiate engagements with
          visitors.</p>
        <p>Default value is<code>true</code>.</p>
        <p>If <code>false</code> then operator is still able to place outbound phone
          calls if the site configuration allows.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">observation_enabled</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">
        <p>If <code>true</code>, the operator is able to observe visitors before engagements.</p>
        <p>Default value is<code>true</code>.</p>
      </td>
    </tr>
  </tbody>
</table>

{% code-tabs %}

{% code-tabs-item title="cURL" %}

```bash
curl --request POST \
    --header "Authorization: Bearer $access_token" \
    --header "Content-Type: application/json" \
    --header "Accept: application/vnd.salemove.v1+json" \
    --data-binary '{
      "name": "Jared H. Grey",
      "role": "manager",
      "assignments": [
        {
          "site_id": "$site_id",
          "team_ids": ["$team_id"]
        }
      ]
    }' \
    "https://api.salemove.com/operators/$operator_id"
```

{% endcode-tabs-item %}

{% code-tabs-item title=undefined %}

```javascript
var XMLHttpRequest = require('xmlhttprequest').XMLHttpRequest;

var xhr = new XMLHttpRequest();

xhr.open('POST', 'https://api.salemove.com/operators/' + operator_id, false);

xhr.setRequestHeader('authorization', 'Bearer ' + accessToken);
xhr.setRequestHeader('content-type', 'application/json');
xhr.setRequestHeader('accept', 'application/vnd.salemove.v1+json');

var data = {
  name: 'Jared H. Grey',
  role: 'manager',
  assignments: [
    {
      site_id: site_id,
      team_ids: [team_id]
    }
  ]
};

var query = JSON.stringify(data);

xhr.send(query);

var response = xhr.responseText;

console.log(response);
```

{% endcode-tabs-item %}

{% code-tabs-item title=undefined %}

```ruby
require 'httparty'

ENDPOINT = 'https://api.salemove.com/operators'

token = ARGV[0].strip
operator_id = ARGV[1].strip
team_id = ARGV[2].strip
values = {
  "name": "Jared H. Grey",
  "role": "manager",
  "assignments": [
    {
      "site_id": site_id,
      "team_ids": [team_id]
    }
  ]
}

headers = {
  :authorization => "Bearer #{access_token}",
  :content_type => "application/json",
  :accept => "application/vnd.salemove.v1+json"
}

options = {
  headers: headers,
  query: values
}

raw_response = HTTParty.post(
  "#{ENDPOINT}/#{operator_id}",
  options
)

response = JSON.parse raw_response.body

puts response
```

{% endcode-tabs-item %}

{% endcode-tabs %}

> Generates the Output

```json
{
  "href": "https://api.salemove.com/operators/f42811bc-8519-4d33-bbb1-36d4555ecb0a",
  "id": "f42811bc-8519-4d33-bbb1-36d4555ecb0a",
  "name": "Jared H. Grey",
  "email": "jared.grey@institution.com",
  "available": true,
  "enabled": true,
  "reactive_enabled":true,
  "proactive_enabled":true,
  "observation_enabled":true
  "available_media_types": [],
  "max_engagement_count": null,
  "multi_engagement_default_availability": null,
  "visible_in_operator_editor": true,
  "engagements": [],
  "engagement_requests": [],
  "role": "manager",
  "picture":
  {
    "url": "https://uploads.salemove.com/user_assets/salemove_com-salemove_models_operator-6036d2ae-6c97-4555-83a2-bc8006b9acc8-jared_grey-f42811bc-8519-4d33-bbb1-36d4555ecb0a.png"
  },
  "audio_source": "phone",
  "phone": "+19174743334",
  "phone_extension": ",,1,23",
  "teams": [
    {"id": "00535468-76d2-438b-bea7-ed9f91c234dc", "name": "General", "site_id": "7d5635b0-88ed-4109-8398-dcd151754640"}
  ],
  "assignments": [
    {"site_id": "7d5635b0-88ed-4109-8398-dcd151754640", "team_ids": ["00535468-76d2-438b-bea7-ed9f91c234dc"]}
  ]
}
```
