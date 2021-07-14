---
description: Protect user accounts by using the required CSRF endpoint.
---

# CSRF Protection

To protect user accounts from Cross-site request forgery attacks, the Single-page application authenticating through the GrowStocks API has to request the CSRF endpoint before attempting to do any action on behalf of the user.

{% hint style="info" %}
You only need to request CSRF protection once per session, typically before the user registers or logs in. If the user logs out, the CSRF token is automatically invalidated and you'll have to request a new one.

Moreover, if the session expires while the user is still on the website, actions you perform on the site will return a 401 or 419 HTTP error codes.

You can find more information on CSRF protection in the Laravel Sanctum docs [here](https://laravel.site/docs/8.x/sanctum#spa-authenticating).
{% endhint %}

{% api-method method="get" host="https://api.growstocks.org" path="/v1/auth/csrf-cookie" %}
{% api-method-summary %}
Set CSRF token cookie
{% endapi-method-summary %}

{% api-method-description %}
This endpoint will set a XSRF-TOKEN cookie in the user's web browser.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}
Cookie has been successfully set.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Once done, the `XSRF-TOKEN` cookie will be present in the user's browser. If you're using Axios, you don't have to worry about anything as it will automatically send the `X-XSRF-TOKEN` header with each request you make.

Otherwise, you will have to manually send the `X-XSRF-TOKEN` with every authenticated API call you make.

{% hint style="info" %}
You can find the full Sanctum SPA authentication docs by clicking [here](https://laravel.site/docs/8.x/sanctum#spa-authentication).
{% endhint %}

