# Media Upgrade Requests

## Create Media Upgrade Request

**Action:** `POST /engagements/{engagement_id}/media_upgrade_requests`

Creates a media upgrade request to an Engagement participant. This endpoint can
be used by either the Operator or the Visitor. The endpoint infers the sender
from the [authorization headers](../#authorization).

When Operator makes the request, the `audio_type` and `phone_number` are not
shared with the Visitor. When Engagement participant creates a new request
before the previous request was accepted/declined then the previous request is
canceled.

See [Webhooks section](../webhooks.md) for receiving media upgrade requests via
webhook events.

The endpoint accepts the following parameters:

| Parameter         | Required | Type   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| :---------------- | :------- | :----- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `audio`           | Yes      | String | One of [Media directions](media-upgrade-requests.md#media-directions) or null if audio must not be used                                                                                                                                                                                                                                                                                                                                        |
| `video`           | Yes      | String | One of [Media directions](media-upgrade-requests.md#media-directions) or null if video must not be used                                                                                                                                                                                                                                                                                                                                        |
| `audio_type`      | No       | String | One of [Audio types](media-upgrade-requests.md#audio-types). Required if `audio` is not `null` and Visitor makes the request. For Operators, this parameter is retrieved from their settings.                                                                                                                                                                                                                                                  |
| `phone_number`    | No       | String | Phone number that the requester will use for audio if `audio_type` is `phone`. Must be in [E.164 format](https://js-sdk-docs.salemove.com/extra/glossary.md.html#phone-numbers). For Operators, this parameter is retrieved from their settings.                                                                                                                                                                                               |
| `phone_extension` | No       | String | Phone number extension that is used when calling `phone_number`. A valid extension contains 1-7 digits and any number of `,` characters. There is an initial two second delay time before the first extension character is processed. Each `,` character in the extension adds a two second wait time before the next character is processed. Maximum length is 25 characters. For Operators, this parameter is retrieved from their settings. |

{% code-tabs %}

{% code-tabs-item title="cURL" %}

```bash
curl --request POST \
    --header "Authorization: Bearer $access_token" \
    --header "Accept: application/vnd.salemove.v1+json" \
    --header "Content-Type: application/json" \
    --data-binary '{
      "audio": "two_way",
      "video": "one_way",
      "audio_type": "phone",
      "phone_number": "+15550100123",
      "phone_extension": ",,1,23"
    }' \
    "https://api.salemove.com/engagements/$engagement_id/media_upgrade_requests"
```

{% endcode-tabs-item %}

{% code-tabs-item title=undefined %}

```javascript
var accessToken = process.argv[0];
var engagementId = process.argv[1];

var XMLHttpRequest = require('xmlhttprequest').XMLHttpRequest;
var uuidv4 = require('uuid/v4');

var url = `https://api.salemove.com/engagements/${engagementId}/media_upgrade_requests`;

var xhr = new XMLHttpRequest();
xhr.open('POST', url, false);
xhr.setRequestHeader('Authorization', `Bearer ${accessToken}`);
xhr.setRequestHeader('Accept', 'application/vnd.salemove.v1+json');
xhr.setRequestHeader('Content-Type', 'application/json');

xhr.send(JSON.stringify({
  audio: 'two_way',
  video: 'one_way',
  audio_type: 'phone',
  phone_number: '+15550100123',
  phone_extension: ',,1,23'
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

response = HTTParty.post(
  "https://api.salemove.com/engagements/#{engagement_id}/media_upgrade_requests",
  body: {
    audio: 'two_way',
    video: 'one_way',
    audio_type: 'phone',
    phone_number: '+15550100123',
    phone_extension: ',,1,23'
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

### Successful response

```json
{
  "id": "4cf0d3fe-8f2f-4aad-8e10-c2ffab8929c6"
}
```

### Error response

Includes one of the
[error response codes](media-upgrade-requests.md#error-response-codes).

## Accept Media Upgrade Request

**Action:**
`PATCH /engagements/{engagement_id}/media_upgrade_requests/{media_upgrade_request_id}`
with `action: "accept"`

Accepts a pending media upgrade request. This endpoint can be used by either the
Operator or the Visitor. The endpoint infers the sender from the
[authorization headers](./#authorization).

When Operator makes the accept request, the `audio_type` and `phone_number` are
not shared with the Visitor.

The endpoint accepts the following parameters:

| Parameter         | Required | Type   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| :---------------- | :------- | :----- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `audio_type`      | No       | String | One of [Audio types](media-upgrade-requests.md#audio-types). Required if `audio` was requested and Visitor accepts the request. For Operators, this parameter is retrieved from their settings.                                                                                                                                                                                                                                                |
| `phone_number`    | No       | String | Phone number that the requester will use for audio if `audio_type` is `phone`. Must be in [E.164 format](https://js-sdk-docs.salemove.com/extra/glossary.md.html#phone-numbers). For Operators, this parameter is retrieved from their settings.                                                                                                                                                                                               |
| `phone_extension` | No       | String | Phone number extension that is used when calling `phone_number`. A valid extension contains 1-7 digits and any number of `,` characters. There is an initial two second delay time before the first extension character is processed. Each `,` character in the extension adds a two second wait time before the next character is processed. Maximum length is 25 characters. For Operators, this parameter is retrieved from their settings. |

{% code-tabs %}

{% code-tabs-item title="cURL" %}

```bash
curl --request PATCH \
    --header "Authorization: Bearer $access_token" \
    --header "Accept: application/vnd.salemove.v1+json" \
    --header "Content-Type: application/json" \
    --data-binary '{
      "action": "accept",
      "audio_type": "phone",
      "phone_number": "+12569020165",
      "phone_extension": ",,1,23"
    }' \
    "https://api.salemove.com/engagements/$engagement_id/media_upgrade_requests/$media_upgrade_request_id"
```

{% endcode-tabs-item %}

{% code-tabs-item title=undefined %}

```javascript
var accessToken = process.argv[0];
var engagementId = process.argv[1];
var mediaUpgradeRequestId = process.argv[2];

var XMLHttpRequest = require('xmlhttprequest').XMLHttpRequest;
var uuidv4 = require('uuid/v4');

var url = `https://api.salemove.com/engagements/${engagementId}/media_upgrade_requests/${mediaUpgradeRequestId}`;

var xhr = new XMLHttpRequest();
xhr.open('PATCH', url, false);
xhr.setRequestHeader('Authorization', `Bearer ${accessToken}`);
xhr.setRequestHeader('Accept', 'application/vnd.salemove.v1+json');
xhr.setRequestHeader('Content-Type', 'application/json');

xhr.send(JSON.stringify({
  action: 'accept',
  audio_type: 'phone',
  phone_number: '+12569020165',
  phone_extension: ',,1,23'
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
media_upgrade_request_id = SecureRandom.uuid

response = HTTParty.patch(
  "https://api.salemove.com/engagements/#{engagement_id}/media_upgrade_requests/#{media_upgrade_request_id}",
  body: {
    action: 'accept',
    audio_type: 'phone',
    phone_number: '+12569020165',
    phone_extension: ',,1,23'
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

### Successful response

Has status code `200`.

### Error response

Includes one of the
[error response codes](media-upgrade-requests.md#error-response-codes).

## Decline Media Upgrade Request

**Action:**
`PATCH /engagements/{engagement_id}/media_upgrade_requests/{media_upgrade_request_id}`
with `action: "decline"`

Declines a pending media upgrade request. This endpoint can be used by either
the Operator or the Visitor. The endpoint infers the sender from the
[authorization headers](./#authorization).

{% code-tabs %}

{% code-tabs-item title="cURL" %}

```bash
curl --request PATCH \
    --header "Authorization: Bearer $access_token" \
    --header "Accept: application/vnd.salemove.v1+json" \
    --header "Content-Type: application/json" \
    --data-binary '{
      "action": "decline"
    }' \
    "https://api.salemove.com/engagements/$engagement_id/media_upgrade_requests/$media_upgrade_request_id"
```

{% endcode-tabs-item %}

{% code-tabs-item title=undefined %}

```javascript
var accessToken = process.argv[0];
var engagementId = process.argv[1];
var mediaUpgradeRequestId = process.argv[2];

var XMLHttpRequest = require('xmlhttprequest').XMLHttpRequest;
var uuidv4 = require('uuid/v4');

var url = `https://api.salemove.com/engagements/${engagementId}/media_upgrade_requests/${mediaUpgradeRequestId}`;

var xhr = new XMLHttpRequest();
xhr.open('PATCH', url, false);
xhr.setRequestHeader('Authorization', `Bearer ${accessToken}`);
xhr.setRequestHeader('Accept', 'application/vnd.salemove.v1+json');
xhr.setRequestHeader('Content-Type', 'application/json');

xhr.send(JSON.stringify({
  action: 'decline'
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
media_upgrade_request_id = SecureRandom.uuid

response = HTTParty.patch(
  "https://api.salemove.com/engagements/#{engagement_id}/media_upgrade_requests/#{media_upgrade_request_id}",
  body: {
    action: 'decline'
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

### Successful response

Has status code `200`.

### Error response

Includes one of the
[error response codes](media-upgrade-requests.md#error-response-codes).

## Media directions

| Value     | Description                                         |
| :-------- | :-------------------------------------------------- |
| `one_way` | Operator media is shared to Visitor.                |
| `two_way` | Operator and Visitor media is shared to each other. |

## Audio types

| Value     | Description                                                               |
| :-------- | :------------------------------------------------------------------------ |
| `browser` | Operator or Visitor wants to use browser for recording and sharing audio. |
| `phone`   | Operator or Visitor wants to use phone call to share audio.               |

## Error response codes

| Code  | Description                                                          |
| :---- | :------------------------------------------------------------------- |
| `401` | When requester is not authenticated or the access token has expired. |
| `403` | When requester is not engagement participant.                        |
| `422` | When input is invalid.                                               |
| `500` | When internal error happened.                                        |
| `503` | When service is unavailable.                                         |
