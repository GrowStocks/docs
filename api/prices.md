---
description: >-
  The prices API allows you to fetch price data directly from our up-to-date
  database.
---

# Prices

{% api-method method="get" host="https://api.growstocks.org" path="/v1/prices/:id" %}
{% api-method-summary %}
Get Prices
{% endapi-method-summary %}

{% api-method-description %}
This endpoint will return a list of all prices.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" %}
If you wish to fetch the price corresponding to the given ID, you may specify it as a parameter in the path.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Price data successfully retrieved.
{% endapi-method-response-example-description %}

```
[
  {
    "id": 1,
    "item_id": 728,
    "quantity": 4040,
    "price": 4896,
    "price_status": 2,
    "demand_status": 1,
    "editor_id": 0,
    "is_approved": 0,
    "is_suggestion": 0,
    "is_daily_quest": 1,
    "counted_as": 1,
    "source_world_name": "ZQO41OZ91B22MAQ9K3E4",
    "inspector_id": 0,
    "edited_on": "2021-07-03 19:37:01",
    "item": {},
    "editor: {
      "id": 1,
      "name": "TorBob"
    },
    "inpector": null
  },
  ...
]
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Could not find an item matching this query.
{% endapi-method-response-example-description %}

```
{
  "message": "No query results for model [App\\Models\\Item] :id"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Searching/Filtering

You can search, filter and sort prices through the endpoint mentioned above. You may pass the properties and their values as query parameters. Search and filter parameters **are mutually inclusive**.

**Search: `source_world_name`, `edited_on`**

**Filter: `quantity`, `price`, `price_status`, `demand_status`, `editor_id`, `is_approved`, `is_suggestion`, `is_daily_quest`, `counted_as`, `source_world_name`, `inspector_id`**

### **Sorting**

You may also sort the results by passing the **`sort_field`** and **`sort_direction`** query parameters.

**Field: `id`, `item_id`, `quantity`, `price`, `edited_on`**

**Direction: `asc`, `desc`**

### Relationships

By default, relationships are always enabled when getting one price, but always disabled when getting or searching all prices.

You may request all or part of the relationships as follows:

* To request all relationships, pass the **`relationships`** query parameter without any value
* To request specific relationships, pass the **`relationships`** query parameter with a comma separated list of accepted relationships \(**`item`**, **`editor`**, **`inspector`**\).

