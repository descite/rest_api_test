# Chat Transcript

## GET Chat Transcript

**Action:** `GET /engagements/{engagement_id}/chat_transcript`

Fetches the engagement's chat transcript. The user must have at least `manager`
role on the site where the engagement took place.

{% code-tabs %}

{% code-tabs-item title="cURL" %}

```bash
curl --request GET \
    --header "Authorization: Bearer $access_token" \
    --header "Accept: application/vnd.salemove.v1+json" \
    "https://api.salemove.com/engagements/$engagement_id/chat_transcript"
```

{% endcode-tabs-item %}

{% code-tabs-item title=undefined %}

```javascript
var XMLHttpRequest = require('xmlhttprequest').XMLHttpRequest;

var xhr = new XMLHttpRequest();

xhr.open(
  'GET',
  `https://api.salemove.com/engagements/${engagement_id}/chat_transcript`,
  false
);

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

ENDPOINT = 'https://api.salemove.com/engagements'

token = ARGV[0]
engagement_id = ARGV[1]

headers = {
  :authorization => "Bearer #{access_token}",
  :accept => "application/vnd.salemove.v1+json"
}

raw_response = HTTParty.get(
  "#{ENDPOINT}/#{engagement_id}/chat_transcript",
  headers: headers
)

response = JSON.parse raw_response.body

puts response
```

{% endcode-tabs-item %}

{% endcode-tabs %}

> Generates the output

```json
[
  {
    "message": "Do you do a count, or what kind of a routine do you have here?",
    "created_at": "2017-07-07T13:47:28.000Z",
    "type": "user",
    "attachment": null,
    "metadata": null,
    "sender": {
      "href": "https://api.salemove.com/visitors/039124e6-b4e8-4a0d-b420-5b6696c7ecb4",
      "name": "Sasha Brown",
      "type": "visitor"
    }
  },
  {
    "message": "Why don't I show you?",
    "created_at": "2017-07-07T13:47:29.000Z",
    "type": "suggestion",
    "attachment": null,
    "metadata": null,
    "sender": {
      "type": "omniguide",
      "name": "omniguide"
    }
  },
  {
    "message": "Why don't I show you?",
    "created_at": "2017-07-07T13:47:30.000Z",
    "type": "user",
    "sender": {
      "href": "https://api.salemove.com/operators/f42811bc-8519-4d33-bbb1-36d4555ecb0a",
      "name": "Jared Grey",
      "type": "operator"
    },
    "attachment": {
      "type": "single_choice",
      "image_url": "https://s3.amazonaws.com/hosting-elements.glia.com/Glia-OG.png",
      "options": [
        {
          "text": "Choice 1",
          "value": "choice_1"
        },
        {
          "text": "Choice 2",
          "value": "choice_2"
        },
        {
          "text": "Choice 3",
          "value": "choice_3"
        }
      ]
    },
    "metadata": {
      "customer": "Harry Brown",
      "location": "London",
      "age": 45
    }
  },
  {
    "message": "Choice 2",
    "created_at": "2017-07-07T13:47:35.000Z",
    "type": "user",
    "attachment": null,
    "metadata": null,
    "sender": {
      "href": "https://api.salemove.com/visitors/039124e6-b4e8-4a0d-b420-5b6696c7ecb4",
      "name": "Sasha Brown",
      "type": "visitor"
    },
    "attachment": {
      "type": "single_choice_response",
      "selected_option": "choice_2"
    }
  },
  {
    "message": "CoBrowsing Started",
    "created_at": "2017-07-01T13:47:37.000Z",
    "type": "user",
    "attachment": null,
    "metadata": null,
    "sender": {
      "type": "system",
      "name": "system"
    }
  },
  {
    "message": "Upgraded to One-Way Video",
    "created_at": "2017-07-01T13:48:13.000Z",
    "type": "user",
    "attachment": null,
    "metadata": null,
    "sender": {
      "type": "system",
      "name": "system"
    }
  }
]
```

### Files Attachments in Chat Transcript

When a message contains a `files` attachment, the attachment includes file name,
content type and URL. The URL requires the same authorization as fetching chat
transcript. For example:

```json
{
  "type": "files",
  "files": [
    {
      "url": "https://api.salemove.com/engagements/75a06f12-43f2-476f-a0fb-6a55b8630523/files/b9c6c3ad-fb3a-479d-aa03-8877ac1ae380",
      "name": "original_file_name.png",
      "content_type": "image/png",
      "deleted": false
    }
  ]
}
```

In case the contents of the file have been deleted, the `url` will be `null` and
`deleted` will be `true`.

```json
{
  "type": "files",
  "files": [
    {
      "url": null,
      "name": "original_file_name.png",
      "content_type": "image/png",
      "deleted": true
    }
  ]
}
```
