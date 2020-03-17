# Delete an Operator

**Action:** `DELETE /operators/{operator_id}`

Disables a specific user. At least the role `manager` is needed to disable a
user.

{% code-tabs %}

{% code-tabs-item title="cURL" %}

```bash
curl --request DELETE \
    --header "Authorization: Bearer $access_token" \
    --header "Accept: application/vnd.salemove.v1+json" \
    "https://api.salemove.com/operators/$operator_id"
```

{% endcode-tabs-item %}

{% code-tabs-item title=undefined %}

```javascript
var XMLHttpRequest = require('xmlhttprequest').XMLHttpRequest;

var xhr = new XMLHttpRequest();

xhr.open('DELETE', `https://api.salemove.com/operators/${operator_id}`, false);

xhr.setRequestHeader('authorization', `Bearer ${accessToken}`);
xhr.setRequestHeader('accept', 'application/vnd.salemove.v1+json');

xhr.send();

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

headers = {
  :authorization => "Bearer #{access_token}",
  :accept => "application/vnd.salemove.v1+json"
}

raw_response = HTTParty.delete(
  "#{ENDPOINT}/#{operator_id}",
  headers: headers
)

response = JSON.parse raw_response.body

puts response
```

{% endcode-tabs-item %}

{% endcode-tabs %}

> Generates the Output

```json

```
