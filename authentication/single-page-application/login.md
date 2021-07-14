---
description: Authenticating users through the GrowStocks API is simple and quick.
---

# Login

To authenticate users through the GrowStocks API, you will first have to request their email address and password through the SPA frontend.

{% hint style="info" %}
You can find the Laravel Sanctum SPA authentication docs [here](https://laravel.site/docs/8.x/sanctum#spa-authentication).
{% endhint %}

{% api-method method="post" host="https://api.growstocks.org" path="/v1/auth/login" %}
{% api-method-summary %}
Login user
{% endapi-method-summary %}

{% api-method-description %}
This endpoint will attempt to login a user with the given email and password.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="X-XSRF-TOKEN" type="string" required=true %}
The CSRF token acquired previously.
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-form-data-parameters %}
{% api-method-parameter name="email" type="string" required=true %}
The email of the user trying to authenticate.
{% endapi-method-parameter %}

{% api-method-parameter name="password" type="string" required=true %}
The password of the user trying to authenticate.
{% endapi-method-parameter %}

{% api-method-parameter name="remember" type="boolean" required=false %}
Whether or not to use the remember me feature for the user who logged in.
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
The user has been successfully logged in.
{% endapi-method-response-example-description %}

```
{
    "two_factor": false
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

In case the user has 2-Factor Authentication enabled, the API will return the following response:

```text
{
    "two_factor": true
}
```

In this case, you will have to instruct the user to enter their 6-digits TOTP token in a `name="code"` field, or one of their recovery codes in a `name=recovery_code` field.

{% api-method method="post" host="https://api.growstocks.org" path="/v1/auth/two-factor-challenge" %}
{% api-method-summary %}
Two-factor challenge
{% endapi-method-summary %}

{% api-method-description %}
This endpoint will attempt to validate the 6-digits TOTP or recovery code provided then login the user.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="code" type="string" required=true %}
The 6-digits TOTP token.
{% endapi-method-parameter %}

{% api-method-parameter name="recovery\_code" type="string" required=true %}
The user's 2-FA recovery code.
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}
The user has been successfully logged in.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %}
The user couldn't be logged in.
{% endapi-method-response-example-description %}

```
{
    "message": "The given data was invalid.",
    "errors": {
       ... 
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
You can find more information on Fortify 2-Factor Authentication in the [Laravel Fortify docs](https://laravel.com/docs/8.x/fortify#two-factor-authentication).
{% endhint %}

