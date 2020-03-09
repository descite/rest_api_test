# Custom Commands

## Send Custom Command

**Action:** `PUT /engagements/{engagement_id}/custom_commands/{command_id}`

Provides flexibility to the user to send custom commands that the Engagement
Visitor web client can interpret and execute. This endpoint can be used only by
the Operator.

This endpoint requires a client-generated custom command ID in the URL. Custom
command ID must be a Version 4 UUID. Submitting a custom command twice with the
same ID does not execute duplicate commands.

The endpoint accepts the following parameters:

| Parameter    | Required | Type   | Description                                                                                                                          |
| :----------- | :------- | :----- | :----------------------------------------------------------------------------------------------------------------------------------- |
| `content`    | No       | String | Optional content that will be shown in the Engagement chat transcript. In case content is not provided generic message will be used. |
| `properties` | Yes      | Object | Properties can be freely defined by the user. It must be a JSON object.                                                              |

{% code-tabs %}

{% code-tabs-item title="cURL" %}

```bash
curl --request PUT \
    --header "Authorization: Bearer $access_token" \
    --header "Accept: application/vnd.salemove.v1+json" \
    --header "Content-Type: application/json" \
    --data-binary '{
      "content": "My custom command triggered",
      "properties": {"key": "value"}
    }' \
    "https://api.salemove.com/engagements/$engagement_id/custom_commands/$id"
```

{% endcode-tabs-item %}

{% code-tabs-item title=undefined %}

```javascript
var accessToken = process.argv[0];
var engagementId = process.argv[1];

var XMLHttpRequest = require('xmlhttprequest').XMLHttpRequest;
var uuidv4 = require('uuid/v4');

var messageId = uuidv4();
var url = `https://api.salemove.com/engagements/${engagementId}/custom_commands/${messageId}`;

var xhr = new XMLHttpRequest();
xhr.open('PUT', url, false);
xhr.setRequestHeader('Authorization', `Bearer ${accessToken}`);
xhr.setRequestHeader('Accept', 'application/vnd.salemove.v1+json');
xhr.setRequestHeader('Content-Type', 'application/json');

xhr.send(JSON.stringify({
  content: 'My custom command triggered',
  properties: {key: 'value'}
});

var response = JSON.parse(xhr.responseText);
console.log(response);
```

{% endcode-tabs-item %}

{% code-tabs-item title=undefined %}

```ruby
require 'httparty'
require 'securerandom'

access_token = ARGV[0].strip
engagement_id = ARGV[1].strip
message_id = SecureRandom.uuid

response = HTTParty.put(
  "https://api.salemove.com/engagements/#{engagement_id}/custom_commands/#{message_id}",
  body: {
    content: "My custom command triggered",
    properties: {key: "value"}
  },
  headers: {
    "Authorization" => "Bearer #{access_token}",
    "Accept" => "application/vnd.salemove.v1+json",
    "Content-Type" => 'application/json'
  }
)

puts response.body
```

{% endcode-tabs-item %}

{% endcode-tabs %}

> Generates the output

```json
{
  "id": "4cf0d3fe-8f2f-4aad-8e10-c2ffab8929c6",
  "engagement_id": "202a50af-8c0e-4e04-9be1-c174a3aabe1a",
  "sub_engagement_id": "29f6f027-b3f2-484e-b353-ad993462a4a5",
  "content": "My custom command triggered",
  "properties": {"key": "value"}
}
```
