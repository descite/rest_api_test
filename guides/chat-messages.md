# Chat messages

{% api-method method="put" host="https://api.salemove.com" path="/engagements/{engagement_id}/chat_messages/{message_id}" %}

{% api-method-summary %}

Send Chat Message

{% endapi-method-summary %}

{% api-method-description %}

Sends a chat message to an engagement participant. This endpoint can be used by
either the operator or the visitor. The endpoint infers the sender from the
[authorization headers](../#authorization).

This endpoint requires a client-generated message ID in the URL. Message ID must
be a version 4 UUID. Submitting a chat message twice with the same ID does not
create duplicate messages.

See [Webhooks section](../webhooks.md) for receiving chat messages via webhook
events.

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

{% api-method-parameter name="content" type="string" required=false %}

The content the sender wishes to send to the recipient. This can only be empty
if the message contains a `files` attachment.

{% endapi-method-parameter %}

{% api-method-parameter name="target" type="string" required=false %}

Recipient of the message. Can be one of "operator", "visitor". If target is not
specified, the chat message will be sent to the other participant. Target must
be specified when the sender is not operator or visitor.

{% endapi-method-parameter %}

{% api-method-parameter name="type" type="string" required=false %}

[Chat message type](chat-messages.md#chat-message-types). Type is only used when
the target is "operator". Default value is "chat".

{% endapi-method-parameter %}

{% api-method-parameter name="attachment" type="Attachment" required=false %}

Chat message attachment \(see
[Attachments section](chat-messages.md#chat-message-attachment) for more info\).

{% endapi-method-parameter %}

{% api-method-parameter name="metadata" type="object" required=false %}

Chat Message Metadata \(see
[Chat Message Metadata section](chat-messages.md#chat-message-metadata) for more
info\).

{% endapi-method-parameter %}

{% endapi-method-query-parameters %}

{% code-tabs %}

{% code-tabs-item title="cURL" %}

```bash
curl --request PUT \
    --header "Authorization: Bearer $access_token" \
    --header "Accept: application/vnd.salemove.v1+json" \
    --header "Content-Type: application/json" \
    --data-binary '{
      "content": "Message content",
      "target": "operator",
      "type": "chat",
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
      }
    }' \
    "https://api.salemove.com/engagements/$engagement_id/chat_messages/$id"
```

{% endcode-tabs-item %}

{% endcode-tabs %}

{% endapi-method-request %}

{% api-method-response %}

{% api-method-response-example httpCode=200 %}

```json
{
  "timestamp": "2017-09-21T12:43:01Z",
  "id": "4cf0d3fe-8f2f-4aad-8e10-c2ffab8929c6",
  "engagement_id": "202a50af-8c0e-4e04-9be1-c174a3aabe1a",
  "sub_engagement_id": "29f6f027-b3f2-484e-b353-ad993462a4a5",
  "content": "Message Content",
  "target": "operator",
  "type": "chat",
  "status": "sent",
  "sender": {
    "type": "visitor"
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
  }
}
```

{% endapi-method-response-example %}

{% endapi-method-response %}

{% endapi-method-spec %}

{% endapi-method %}

## Chat Message Types

| Type         | Description                                                                                                                                                                                                                                        |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `chat`       | Regular chat message.                                                                                                                                                                                                                              |
| `event`      | A message type used to communicate that an action has been performed by the visitor. Events can only be sent by visitors. Also see [events](events.md).                                                                                            |
| `suggestion` | A suggested response to the visitor. Suggestion is visible only to operator and can then be selected and sent to the visitor. Also see [AI suggestion](../omniguide/messages/suggestion.md).                                                       |
| `prompt`     | A message that is only visible to operator. Prompts are typically used to guide the operator through an engagement. For example, a prompt might suggest offering CoBrowsing to the visitor. Also see [AI prompt](../omniguide/messages/prompt.md). |

## Chat Message Attachment

Attachments let you add more context to a message, enhancing user experience and
making it more interactive. Chat message attachment must have `type` property
that defines the behavior of attachment.

Example response to a chat message with an attachment when attachment's option
is selected

```json
{
  "message": "Choice 2",
  "created_at": "2017-09-21T12:44:01.000Z",
  "type": "user",
  "sender": {
    "href": "https://api.salemove.com/visitors/039124e6-b4e8-4a0d-b420-5b6696c7ecb4",
    "name": "Sasha Brown",
    "type": "visitor"
  },
  "attachment": {
    "type": "single_choice_response",
    "selected_option": "choice_2"
  }
}
```

### Chat Message Attachment Properties

| Parameter | Required | Type   | Description                                                                               |
| :-------- | :------- | :----- | :---------------------------------------------------------------------------------------- |
| `type`    | Yes      | String | Type of the attachment. Can be one of `single_choice`, `single_choice_response`, `files`. |

### Chat Message Attachment Supported Types

| Type                     | Description                                                                                                                                                                                                                                                                                                              |
| :----------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `single_choice`          | Single choice defines a list of options for user to make a simplified decision for the next interaction. Selected option will be sent back to the other party as a regular chat message containing [single choice response attachment](chat-messages.md#chat-message-attachment-type-single_choice_response-parameters). |
| `single_choice_response` | Response indicates a successful user interaction while passing back also the selection value.                                                                                                                                                                                                                            |
| `files`                  | A list of files such as image or PDF                                                                                                                                                                                                                                                                                     |

### Chat Message Attachment Type `single_choice_response` Parameters

| Parameter         | Required | Type   | Description                              |
| :---------------- | :------- | :----- | :--------------------------------------- |
| `selected_option` | Yes      | String | User interaction based choice selection. |

### Chat Message Attachment Type `single_choice` Parameters

| Parameter   | Required | Type                                                                              | Description                                                                           |
| :---------- | :------- | :-------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------ |
| `options`   | Yes      | Array of [single choice options](chat-messages.md#single-choice-option-structure) | Provides a list of all available choices for the user to choose from.                 |
| `image_url` | No       | String                                                                            | URL of an image displayed on top of the choices expressing clear intent of the cards. |

### **Single Choice Option Structure**

| Parameter | Required | Type   | Description                                                 |
| :-------- | :------- | :----- | :---------------------------------------------------------- |
| `text`    | Yes      | String | Text displayed to user as a choice label.                   |
| `value`   | Yes      | String | Value of the choice sent as a response on user interaction. |

### Chat Message Attachment Type `files` Parameters

| Parameter | Required | Type   | Description                                                                                             |
| :-------- | :------- | :----- | :------------------------------------------------------------------------------------------------------ |
| `files`   | Yes      | String | List of objects containing file ID's that were returned by [upload file](chat-messages.md#upload-file). |

```bash
curl --request PUT \
    --header "Authorization: Bearer $access_token" \
    --header "Accept: application/vnd.salemove.v1+json" \
    --header "Content-Type: application/json" \
    --data-binary '{
      "content": "Message content",
      "target": "operator",
      "type": "chat",
      "attachment": {
        "type": "files",
        "files": [{"id": "d0b328a4-a5f9-43d8-8ba7-725b0cfffa73"}]
      }
    }' \
    "https://api.salemove.com/engagements/$engagement_id/chat_messages/$id"
```

Generates the output

```json
{
  "timestamp": "2017-09-21T12:43:01Z",
  "id": "4cf0d3fe-8f2f-4aad-8e10-c2ffab8929c6",
  "engagement_id": "202a50af-8c0e-4e04-9be1-c174a3aabe1a",
  "sub_engagement_id": "29f6f027-b3f2-484e-b353-ad993462a4a5",
  "content": "Message content",
  "target": "operator",
  "type": "chat",
  "status": "sent",
  "sender": {
    "type": "visitor"
  },
  "attachment": {
    "type": "files",
    "files": [
      {
        "url": "https://api.salemove.com/engagements/202a50af-8c0e-4e04-9be1-c174a3aabe1a/files/4cf0d3fe-8f2f-4aad-8e10-c2ffab8929c6",
        "name": "original_file_name.png",
        "content_type": "image/png",
        "deleted": false
      }
    ]
  }
}
```

## Chat Message Metadata

Chat message metadata allows an integrator to add end to end data inside a JSON
object. This information is only relevant to the integrator and will be handled
transparently inside Glia.

Metadata can be used, for instance, to customize how a
[custom response card](../omniguide/messages/suggestion.md#suggestion-with-custom-response-card)
is rendered.

> Custom response cards workflow example:

![](../.gitbook/assets/custom-response-card-diagram.png)

### Chat Message Metadata Properties

Chat message metadata is an optional property of type JSON object specified by
the integrator. Any JSON object is allowed.

Chat message metadata examples:

```json
{
  "metadata": {
    "custom_card_type": "insurance",
    "customer_number": "C123456789",
    "age": 33
  }
}
```

```json
{
  "metadata": {
    "custom_card_type": "latest_news",
    "custom_card_language": "en-gb",
    "customer": "Harry Brown",
    "location": "London",
    "age": 45
  }
}
```

Chat message `metadata` property may contain `provider` object with `name`
property representing the name of message provider.

For example if the message is sent by the
[operator assistant](../omniguide/operator-assistants/) `name` property
represents operator assistant's name that provided suggestion.

Chat message metadata example with provider name

```json
{
  "metadata": {
    "provider": {
      "name": "Sales Bot"
    }
  }
}
```

{% api-method method="post" host="https://api.salemove.com" path="/engagements/{engagement_id}/files" %}

{% api-method-summary %}

Upload File

{% endapi-method-summary %}

{% api-method-description %}

Uploads a file that can later be sent as a part of a chat message.

The response contains a field `security_scanning_required`. If the value of this
field is true, uploader must wait for the
[FileSecurityScanResultEvent](../webhooks.md#filesecurityscanresultevent) to
arrive before they can send the file as a part of a chat message. Additionally,
the scan result must be `clean` in order to send the file.

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

The endpoint accepts `multipart/form-data` and
`application/x-www-form-urlencoded` content types.

{% endapi-method-parameter %}

{% endapi-method-headers %}

{% api-method-query-parameters %}

{% api-method-parameter name="content" type="File" required=true %}

File to be uploaded. Maximum file size is 25 MB by default and 5 MB for
SMS/WhatsApp visitors. Only files with MIME types set in site settings can be
uploaded. For more, see [`allowed_file_content_types` setting](../sites.md).

{% endapi-method-parameter %}

{% endapi-method-query-parameters %}

{% code-tabs %}

{% code-tabs-item title="cURL" %}

```bash
curl --request POST \
    --header "Authorization: Bearer $access_token" \
    --header "Accept: application/vnd.salemove.v1+json" \
    --form "content=@picture.png" \
    "https://api.salemove.com/engagements/$engagement_id/files"
```

{% endcode-tabs-item %}

{% endcode-tabs %}

{% endapi-method-request %}

{% api-method-response %}

{% api-method-response-example httpCode=200 %}

```json
{
  "file_id": "d0b328a4-a5f9-43d8-8ba7-725b0cfffa73",
  "security_scanning_required": true
}
```

{% endapi-method-response-example %}

{% endapi-method-response %}

{% endapi-method-spec %}

{% endapi-method %}

{% api-method method="get" host="https://api.salemove.com" path="/engagements/{engagement_id}/files/{file_id}" %}

{% api-method-summary %}

Download File

{% endapi-method-summary %}

{% api-method-description %}

Downloads a file that is part of an engagement (for example, the file has been
sent as part of a chat message). Returns either the contents of the file or a
download URL depending on the `Accept` header (see below).

{% endapi-method-description %}

{% api-method-spec %}

{% api-method-request %}

{% api-method-headers %}

{% api-method-parameter name="Authorization" type="string" required=true %}

Used to authenticate the user. Only `Bearer` access token is allowed.

{% endapi-method-parameter %}

{% api-method-parameter name="Accept" type="string" required=false %}

Must be one of `application/vnd.salemove.v1+json` or `*/*` (defaults to `*/*` if
not specified).

If the value is `application/vnd.salemove.v1+json`, returns a JSON response
containing `file_url`, which is a temporary file download URL that expires after
a short while. If the value is `*/*`, returns the contents of the requested
file.

{% endapi-method-parameter %}

{% endapi-method-headers %}

{% code-tabs %}

{% code-tabs-item title="cURL" %}

```bash
curl --request GET \
    --header "Authorization: Bearer $access_token" \
    --header "Accept: application/vnd.salemove.v1+json" \
    "https://api.salemove.com/engagements/$engagement_id/files/$file_id"
```

{% endcode-tabs-item %}

{% endcode-tabs %}

{% endapi-method-request %}

{% api-method-response %}

{% api-method-response-example httpCode=200 %}

```json
{
  "file_url": "https://example.com/file"
}
```

{% endapi-method-response-example %}

{% endapi-method-response %}

{% endapi-method-spec %}

{% endapi-method %}
