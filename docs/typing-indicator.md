# Typing Indicator

{% api-method method="put" host="https://api.salemove.com" path="/engagements/{engagement\_id}/typing\_indicator" %}
{% api-method-summary %} Typing Indicator {% endapi-method-summary %}

{% api-method-description %} Updates engagement participant typing indicator.
<br><br>

Typing indicator allows engagement participant to know whether another
participant is currently typing or not. This brings a more fluid user experience
for participants while they are exchanging chat messages. <br><br>

This endpoint can be used by either the operator or the visitor. The endpoint
infers the sender from the authorization headers. <br><br>
{% endapi-method-description %}

{% api-method-spec %} {% api-method-request %} {% api-method-query-parameters %}
{% api-method-parameter name="typing" type="boolean" required=true %} Whether
participant is currently typing or not. {% endapi-method-parameter %}
{% endapi-method-query-parameters %} {% endapi-method-request %}

{% api-method-response %} {% api-method-response-example httpCode=204 %}
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %} Occurs when `Authorization` header
is missing/invalid. {% endapi-method-response-example-description %}
{% endapi-method-response-example %}

{% api-method-response-example httpCode=403 %}
{% api-method-response-example-description %} Occurs when requester is not
engagement participant. {% endapi-method-response-example-description %}
{% endapi-method-response-example %}

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %} Occurs when the input is invalid
or engagement has already ended.
{% endapi-method-response-example-description %}
{% endapi-method-response-example %}

{% endapi-method-response %} {% endapi-method-spec %} {% endapi-method %}

### Example request

{% code-tabs %} {% code-tabs-item title="cURL" %}

```bash
curl --request PUT \
     --header "Authorization: Bearer $access_token" \
     --header "Accept: application/vnd.salemove.v1+json" \
     --header "Content-Type: application/json" \
     --data-binary '{
       "typing": true
     }' \
     "https://api.salemove.com/engagements/$engagement_id/typing_indicator"
```

{% endcode-tabs-item %}

{% code-tabs-item title="JavaScript" %}

```javascript
var accessToken = process.argv[0];
var engagementId = process.argv[1];

var XMLHttpRequest = require('xmlhttprequest').XMLHttpRequest;
var uuidv4 = require('uuid/v4');

var url = `https://api.salemove.com/engagements/${engagementId}/typing_indicator`;

var xhr = new XMLHttpRequest();
xhr.open('PUT', url, false);
xhr.setRequestHeader('Authorization', `Bearer ${accessToken}`);
xhr.setRequestHeader('Accept', 'application/vnd.salemove.v1+json');
xhr.setRequestHeader('Content-Type', 'application/json');

xhr.send(JSON.stringify({
  typing: true,
});

var response = JSON.parse(xhr.responseText);
console.log(response);
```

{% endcode-tabs-item %}

{% code-tabs-item title="Ruby" %}

```ruby
require 'httparty'

token = ARGV[0].strip
engagement_id = ARGV[1].strip

response = HTTParty.post(
  "https://api.salemove.com/engagements/#{engagement_id}/typing_indicator",
  headers: {
    'Authorization' => "Bearer #{access_token}",
    'Content-Type' => "application/json",
    'Accept' => 'application/vnd.salemove.v1+json'
  }
)
puts response.body
```

{% endcode-tabs-item %} {% endcode-tabs %}

{% hint style="warning" %} Sending concurrent requests might lead to requests
being delivered to our API out of order.

Use techniques such as `throttling` and `debouncing` to avoid this.
{% endhint %}

{% hint style="warning" %} Avoid changing typing indicator too often as it
distracts engagement participants.

For example, instead of changing typing indicator to `false` every time
participant stops typing, use some heuristics, such as:

- participant has not typed for 3 seconds
- participant deleted the whole message from the chat input box

{% endhint %}
