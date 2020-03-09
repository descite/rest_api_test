# Site Visitor

{% api-method method="post" host="https://api.salemove.com" path="/visitors" %}

{% api-method-summary %}

Create Visitor

{% endapi-method-summary %}

{% api-method-description %}

Integrators may need to engage operators with visitors outside of the web
browser or without using the [Glia JavaScript API](js_api.md).

In this case the integrator can create a visitor entity using the REST API. The
response will contain a bearer access token which can be used for all of the
following requests related to the visitor. The bearer access token should be
renewed every 24 hours.

{% endapi-method-description %}

{% api-method-spec %}

{% api-method-request %}

{% api-method-headers %}

{% api-method-parameter name="Authorization" type="string" required=true %}

Used to authenticate the site. Must be a site application token.

{% endapi-method-parameter %}

{% api-method-parameter name="Accept" type="string" required=true %}

Must be `application/vnd.salemove.v1+json`

{% endapi-method-parameter %}

{% endapi-method-headers %}

```bash
curl --request POST \
     --header "Authorization: ApplicationToken $application_token" \
     --header "Content-Type: application/json" \
     --header "Accept: application/vnd.salemove.v1+json" \
     "https://api.salemove.com/visitors"
```

{% endapi-method-request %}

{% api-method-response %}

{% api-method-response-example httpCode=200 %}

```json
{
  "id": "5ec10423-f0b8-4f8e-8526-e52146d5cb4d",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJhcHBsaWNhdGlvbjpkMTdiOWEyNS00MjY5LTQ5M2ItOTg1ZC0wNzhmYWI3MGMxNGEiLCJyb2xlcyI6W3sidHlwZSI6InZpc2l0b3IiLCJ2aXNpdG9yX2lkIjoiMjk1OTYyYzctODg3NS00MjgwLWI5ZjMtMjM4Y2MyZDkxMTY3In0seyJ0eXBlIjoic2l0ZV92aXNpdG9yIiwic2l0ZV9pZCI6ImVhMGNhYjE3LTMwMWMtNGMzYi1iNmViLTZjZWY2ZGQ5M2I1YyJ9XSwiaXNzIjoiU2FsZU1vdmUgQVBJIiwiaWF0IjoxNTM1NDQwOTA4LCJleHAiOjE1MzY2NTA1MDh9.iL1NVrcokaajkLBPASFeK7aB8W5Ryxll4dlIK6-kuby_yShO6erINSVct-GSHukdtRu_cKD6FRJ5nk_PsYOAGQ"
}
```

{% endapi-method-response-example %}

{% endapi-method-response %}

{% endapi-method-spec %}

{% endapi-method %}

{% api-method method="post" host="https://api.salemove.com" path="/visitors/{visitor_id}/token" %}

{% api-method-summary %}

Renew Visitor Access Token

{% endapi-method-summary %}

{% api-method-description %}

Visitors created using the REST API have bearer access tokens which for security
reasons have short lifetime. These tokens should be renewed once in every 24
hours before starting a new engagement or changing visitor details.

{% endapi-method-description %}

{% api-method-spec %}

{% api-method-request %}

{% api-method-path-parameters %}

{% api-method-parameter name="visitor_id" type="string" required=true %}

Visitor ID of the visitor whose access token is renewed.

{% endapi-method-parameter %}

{% endapi-method-path-parameters %}

{% api-method-headers %}

{% api-method-parameter name="Authorization" type="string" required=true %}

Used to authenticate the site. Must be a site application token.

{% endapi-method-parameter %}

{% api-method-parameter name="Accept" type="string" required=true %}

Must be `application/vnd.salemove.v1+json`

{% endapi-method-parameter %}

{% endapi-method-headers %}

```bash
curl --request POST \
     --header "Authorization: ApplicationToken $application_token" \
     --header "Content-Type: application/json" \
     --header "Accept: application/vnd.salemove.v1+json" \
     "https://api.salemove.com/visitors/$visitor_id/token"
```

{% endapi-method-request %}

{% api-method-response %}

{% api-method-response-example httpCode=200 %}

```json
{
  "id": "5ec10423-f0b8-4f8e-8526-e52146d5cb4d",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJhcHBsaWNhdGlvbjpkMTdiOWEyNS00MjY5LTQ5M2ItOTg1ZC0wNzhmYWI3MGMxNGEiLCJyb2xlcyI6W3sidHlwZSI6InZpc2l0b3IiLCJ2aXNpdG9yX2lkIjoiMjk1OTYyYzctODg3NS00MjgwLWI5ZjMtMjM4Y2MyZDkxMTY3In0seyJ0eXBlIjoic2l0ZV92aXNpdG9yIiwic2l0ZV9pZCI6ImVhMGNhYjE3LTMwMWMtNGMzYi1iNmViLTZjZWY2ZGQ5M2I1YyJ9XSwiaXNzIjoiU2FsZU1vdmUgQVBJIiwiaWF0IjoxNTM1NDQwOTA4LCJleHAiOjE1MzY2NTA1MDh9.iL1NVrcokaajkLBPASFeK7aB8W5Ryxll4dlIK6-kuby_yShO6erINSVct-GSHukdtRu_cKD6FRJ5nk_PsYOAGQ"
}
```

{% endapi-method-response-example %}

{% endapi-method-response %}

{% endapi-method-spec %}

{% endapi-method %}

{% api-method method="get" host="https://api.salemove.com" path="/sites/{site_id}/visitors/{visitor_id}" %}

{% api-method-summary %}

Visitor Information

{% endapi-method-summary %}

{% api-method-description %}

This fetches the visitor's information for a visitor that has an ID of
`visitor_id` for the site with ID `site_id`. If visitor is authenticated, the
response will include the attributes and tokens fetched from the
[authentication provider](authentication-providers.md).

{% endapi-method-description %}

{% api-method-spec %}

{% api-method-request %}

{% api-method-path-parameters %}

{% api-method-parameter name="site_id" type="string" required=true %}

ID of the site for which visitor information is retrieved.

{% endapi-method-parameter %}

{% api-method-parameter name="visitor_id" type="string" required=true %}

ID of the visitor whose information is retrieved.

{% endapi-method-parameter %}

{% endapi-method-path-parameters %}

{% api-method-headers %}

{% api-method-parameter name="Authorization" type="string" required=true %}

Used to authenticate the operator. The operator whose bearer access token is
used for making this request must have access to the site.

{% endapi-method-parameter %}

{% api-method-parameter name="Accept" type="string" required=true %}

Must be `application/vnd.salemove.v1+json`.

{% endapi-method-parameter %}

{% endapi-method-headers %}

```bash
curl --request PATCH \
     --header "Authorization: Bearer $access_token" \
     --header "Content-Type: application/json" \
     --header "Accept: application/vnd.salemove.v1+json" \
     --data-binary '{
       "name": "Mark White",
       "email": "mark.white@lawoffice.com",
       "phone": "+12024561111",
       "note": "bought insurance previously; considering upgrade.",
       "note_update_method": "append",
       "custom_attributes": {
         "home_address": "Washington, DC",
         "vip": "true",
         "profession": "attorney"
       }
     }' \
     "https://api.salemove.com/sites/$site_id/visitors/$visitor_id"
```

{% endapi-method-request %}

{% api-method-response %}

{% api-method-response-example httpCode=200 %}

```json
{
  "href": "https://api.salemove.com/sites/2e56b224-6708-4755-b6c9-35f9889e42dd/visitors/41fb129c-fd0c-4f8b-8ca5-657787917c4b",
  "name": "Mark White",
  "email": "mark.white@lawoffice.com",
  "phone": "12024561111",
  "note": "Moved to bind.\nbought insurance previously; considering upgrade",
  "custom_attributes": {
    "home_address": "Washington, DC",
    "vip": "true",
    "profession": "attorney"
  },
  "id": "41fb129c-fd0c-4f8b-8ca5-657787917c4b",
  "banned": false,
  "authenticated_attributes": {}
}
```

{% endapi-method-response-example %}

{% endapi-method-response %}

{% endapi-method-spec %}

{% endapi-method %}

{% api-method method="patch" host="https://api.salemove.com" path="/sites/{site_id}/visitors/{visitor_id}" %}

{% api-method-summary %}

Update Visitor Information

{% endapi-method-summary %}

{% api-method-description %}

Updates the visitor's information for a specific `visitor_id` and matching the
site with a matching `site_id`.

{% endapi-method-description %}

{% api-method-spec %}

{% api-method-request %}

{% api-method-path-parameters %}

{% api-method-parameter name="site_id" type="string" required=true %}

ID of the site for which visitor information is updated.

{% endapi-method-parameter %}

{% endapi-method-path-parameters %}

{% api-method-path-parameters %}

{% api-method-parameter name="visitor_id" type="string" required=true %}

ID of the visitor whose information is updated.

{% endapi-method-parameter %}

{% endapi-method-path-parameters %}

{% api-method-headers %}

{% api-method-parameter name="Authorization" type="string" required=true %}

Used to authenticate the operator. The operator whose bearer access token is
used for making this request must have access to the site.

{% endapi-method-parameter %}

{% api-method-parameter name="Accept" type="string" required=true %}

Must be `application/vnd.salemove.v1+json`.

{% endapi-method-parameter %}

{% endapi-method-headers %}

```bash
curl --request PATCH \
     --header "Authorization: Bearer $access_token" \
     --header "Content-Type: application/json" \
     --header "Accept: application/vnd.salemove.v1+json" \
     --data-binary '{
       "name": "Mark White",
       "email": "mark.white@lawoffice.com",
       "phone": "+12024561111",
       "note": "bought insurance previously; considering upgrade.",
       "note_update_method": "append",
       "custom_attributes": {
         "home_address": "Washington, DC",
         "vip": "true",
         "profession": "attorney"
       }
     }' \
     "https://api.salemove.com/sites/$site_id/visitors/$visitor_id"
```

{% endapi-method-request %}

{% api-method-response %}

{% api-method-response-example httpCode=200 %}

```json
{
  "href": "https://api.salemove.com/sites/2e56b224-6708-4755-b6c9-35f9889e42dd/visitors/41fb129c-fd0c-4f8b-8ca5-657787917c4b",
  "name": "Mark White",
  "email": "mark.white@lawoffice.com",
  "phone": "12024561111",
  "note": "Moved to bind.\nbought insurance previously; considering upgrade",
  "custom_attributes": {
    "home_address": "Washington, DC",
    "vip": "true",
    "profession": "attorney"
  },
  "id": "41fb129c-fd0c-4f8b-8ca5-657787917c4b",
  "banned": false,
  "authenticated_attributes": {}
}
```

{% endapi-method-response-example %}

{% endapi-method-response %}

{% endapi-method-spec %}

{% endapi-method %}

In case of updating the visitor's information from the browser it is **strongly
recommended** to use the
[Glia JS API](http://js-sdk-docs.salemove.com/class/Salemove.html#updateInformation-dynamic).

Custom attributes can be updated by sending them as key-value pairs in the
request. All keys and values must be submitted as strings. \(They are also
returned as strings\). Nested key-value pairs are not supported. The parameter
with name `note_update_method` can take two values: `replace`, which replaces
existing notes; and `append`, which adds the new note to existing notes. _If
this field is omitted, the value will default to_ `replace`_._

| Parameter                         | Type   | Required | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| :-------------------------------- | :----- | :------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `site_id`                         | String | Yes      | The site where the visitor's information will be updated.                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `visitor_id`                      | String | Yes      | The visitor whose information will be updated                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `name`                            | String | No       | The visitor's name.                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `email`                           | String | No       | The visitor's email.                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `phone`                           | String | No       | The visitor's phone.                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `note`                            | String | No       | The visitor's notes.                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `note_updated_method`             | String | No       | Specifies a method for updating the visitor's note. The default value is `replace`. Available values are `replace` and `append`. If the method is `replace` then the notes for the visitor will be overwritten by the field `note` in the request. If the method is `append` then the field `note` in the request will append to the existing visitor's notes.                                                                                                              |
| `custom_attributes`               | Object | No       | An object with custom key-value pairs to be assigned to the visitor. The server treats all keys and values as strings and also returns them as strings. Nested key-value pairs are not supported.                                                                                                                                                                                                                                                                           |
| `custom_attributes_update_method` | String | No       | Specifies the method for updating custom attributes. The default value is `replace`. Allowed values are `replace` and `merge`. If the method is `replace`, then all custom attributes for the visitor will be overwritten by the field `custom_attributes` in the request. If the method is `merge`, only custom attributes present in the request will be added or updated. In case of `merge` it is possible to remove a custom attribute by setting its value to `null`. |
| `context`                         | Object | No       | An object with visitor's browser context. The `context` and `custom_attributes` are needed to trigger `visitor_custom_attributes_changed` business rule event. Content for this can be obtained from (Visitor JS SDK)[https://js-sdk-docs.salemove.com/class/Salemove.html#getBrowserContext-dynamic].                                                                                                                                                                      |

# Example: Merge Visitor Custom Attributes

The following example illustrates how to update the visitor custom attribute
`vip` to `true` and remove attribute `profession` without changing the value of
attribute `home_address`.

Visitor information before change:

```json
{
  "name": "James Cook",
  "email": "james@example",
  "phone": "+12345678910",
  "note": "No comments.",
  "custom_attributes": {
    "profession": "doctor",
    "vip": "false",
    "home_address": "Washington, DC"
  },
  "generated_name": "Visitor #7401",
  "banned": false,
  "authenticated_attributes": {}
}
```

Request:

```bash
curl --request PATCH \
     --header "Authorization: Bearer $access_token" \
     --header "Content-Type: application/json" \
     --header "Accept: application/vnd.salemove.v1+json" \
     --data-binary '{
         "custom_attributes_update_method": "merge",
         "custom_attributes": {
           "vip": "true",
           "profession": null
         }
      }' \
     "https://api.salemove.com/sites/$site_id/visitors/$visitor_id"
```

Visitor information after change:

```json
{
  "name": "James Cook",
  "email": "james@example",
  "phone": "+12345678910",
  "note": "No comments.",
  "custom_attributes": {
    "vip": "true",
    "home_address": "Washington, DC"
  },
  "generated_name": "Visitor #7401",
  "banned": false,
  "authenticated_attributes": {}
}
```
