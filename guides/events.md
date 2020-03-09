# Events

Events can be used to notify Glia about actions performed by the Visitor. Also,
see
[Glia JavaScript API](https://js-sdk-docs.salemove.com/class/Engagement.html#recordEvent-dynamic)

{% api-method method="post" host="https://api.salemove.com" path="/engagements/{engagement_id}/events" %}
{% api-method-summary %}

Send event message

{% endapi-method-summary %}

{% api-method-description %}

Allows integrators to send event messages which communicate that an action has
been performed by the visitor.

{% endapi-method-description %}

{% api-method-spec %}

{% api-method-request %}

{% api-method-headers %}

{% api-method-parameter name="Authorization" type="string" required=true %}

Used to authenticate the Visitor. Allowed token type is `Bearer`

{% endapi-method-parameter %}

{% api-method-parameter name="Accept" type="string" required=true %}

The current API version is v1. Must be `application/vnd.salemove.v1+json`

{% endapi-method-parameter %}

{% api-method-parameter name="Content-Type" type="string" required=true %}

Content type of data sent to the server. Must be `application/json`

{% endapi-method-parameter %}

{% endapi-method-headers %}

{% api-method-body-parameters %}

{% api-method-parameter name="message" type="string" required=true %}

Utterance depicting the engaged Visitor event.

{% endapi-method-parameter %}

{% endapi-method-body-parameters %}

{% endapi-method-request %}

{% api-method-response %}

{% api-method-response-example httpCode=200 %}

{% api-method-response-example-description %}

A successful request returns a newly-created event message object as a response.

{% endapi-method-response-example-description %}

{% code-tabs %}

{% code-tabs-item %}

```json
{
  "timestamp": "2019-08-28T13:55:24Z",
  "id": "0df4c3f7-f55b-4186-962d-0c5198fd2adb",
  "engagement_id": "af8c2e16-545d-4f83-9e79-7c5ebc544b1d",
  "sub_engagement_id": "339",
  "content": "Visitor navigated to insurance page",
  "status": "sent",
  "sender": {
    "type": "visitor"
  },
  "target": "operator"
}
```

{% endcode-tabs-item %}

{% endcode-tabs %}

{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}

{% api-method-response-example-description %}

Occurs when `Authorization` header is missing/invalid.

{% endapi-method-response-example-description %}

{% code-tabs %}

{% code-tabs-item title="Authorization information missing" %}

```json
{
  "message": "Authorization information missing",
  "debug_message": "Authorization header must have format 'token_type token' where token_type is SessionId or AuthToken"
}
```

{% endcode-tabs-item %}

{% code-tabs-item title="Invalid token" %}

```json
{
  "message": "Invalid token",
  "debug_message": "Authorization header must contain a valid token"
}
```

{% endcode-tabs-item %}

{% endcode-tabs %}

{% endapi-method-response-example %}

{% api-method-response-example httpCode=403 %}

{% api-method-response-example-description %}

Occurs when sender is not `visitor`.

{% endapi-method-response-example-description %}

{% code-tabs %}

{% code-tabs-item title="Sender is not visitor" %}

```json
{
  "message": "You don't have permissions to send a event message",
  "debug_message": ""
}
```

{% endcode-tabs-item %}

{% endcode-tabs %}

{% endapi-method-response-example %}

{% endapi-method-response %}

{% endapi-method-spec %}

{% endapi-method %}

### Example request

{% code-tabs %}

{% code-tabs-item title="Example event message request" %}

```bash
curl -X POST \
  https://api.salemove.com/engagements/$engagement_id/events \
  -H 'Authorization: Bearer $access_token' \
  -H 'Accept: application/vnd.salemove.v1+json' \
  -H 'Content-Type: application/json' \
  -d '{
	"message": "Visitor navigated to insurance page"
}'
```

{% endcode-tabs-item %}

{% endcode-tabs %}
