---
description: Registering users through the GrowStocks API is simple and quick.
---

# Registration

{% hint style="info" %}
You can find Laravel Fortify registration docs [here](https://laravel.com/docs/8.x/fortify#registration).
{% endhint %}

{% api-method method="post" host="https://api.growstocks.org" path="/v1/auth/register" %}
{% api-method-summary %}
Register user
{% endapi-method-summary %}

{% api-method-description %}
This endpoint will attempt to register a user with the given information.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="X-XSRF-TOKEN" type="string" required=true %}
The CSRF token acquired previously.
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-form-data-parameters %}
{% api-method-parameter name="name" type="string" required=true %}
The user's username. Has to be at least 3 characters, at most 18 characters, and only contain alphanumeric characters without spaces.
{% endapi-method-parameter %}

{% api-method-parameter name="email" type="string" required=true %}
The user's email address.
{% endapi-method-parameter %}

{% api-method-parameter name="password" type="string" required=true %}
The user's password. Has to be at least 7 characters and contain at least one uppercase character, one number, and one special character.
{% endapi-method-parameter %}

{% api-method-parameter name="password\_confirmation" type="string" required=true %}
The confirmation of the password field.
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}
The user has been successfully registered.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %}
The user couldn't be registered.
{% endapi-method-response-example-description %}

```
{
    "message": "The given data was invalid.",
    "errors": {
        "password": [
            "The password must be at least 7 characters and contain at least one uppercase character, one number, and one special character."
        ],
        ...
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

