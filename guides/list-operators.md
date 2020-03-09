# List Operators

**Action:** `GET /operators`

Lists all users (`operators`, `managers`, `super_managers`) visible to the
caller given associated sites and permissions. Please note that for this
endpoint, pagination is used.

| Parameter             | Type      | Description                                                                                                                                                          |
| :-------------------- | :-------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `include_engagements` | `boolean` | If `true`, fetches data for `engagements`, `engagement_requests` and `engaged_since`. The default value is `false`.                                                  |
| `include_disabled`    | `boolean` | If `true`, includes users that have been disabled. The default value is `false`.                                                                                     |
| `include_offline`     | `boolean` | If `true`, includes users that are offline. The default value is `true`.                                                                                             |
| `include_support`     | `boolean` | If `true`, includes users from Glia support staff. The default value is `true`.                                                                                      |
| `site_ids`            | `array`   | Only users from the specified sites will be included in the response. Users from all sites available to the caller will be included if this option is not specified. |
| `team_ids`            | `array`   | Only users from the specified teams will be included in the response. Users from all teams will be included if this option is not specified.                         |

{% code-tabs %}

{% code-tabs-item title="cURL" %}

```bash
curl --request GET \
    --header "Authorization: Bearer $access_token" \
    --header "Accept: application/vnd.salemove.v1+json" \
    "https://api.salemove.com/operators?page=1"
```

{% endcode-tabs-item %}

{% code-tabs-item title=Ruby %}

```ruby
require 'httparty'

ENDPOINT = 'https://api.salemove.com/operators'

token = ARGV[0].strip

headers = {
  :authorization => "Bearer #{access_token}",
  :accept => "application/vnd.salemove.v1+json"
}

raw_response = HTTParty.get(
  ENDPOINT,
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
