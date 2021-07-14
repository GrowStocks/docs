---
description: >-
  The items API allows you to fetch item data directly from our up-to-date
  database.
---

# Items

{% api-method method="get" host="https://api.growstocks.org" path="/v1/items/:id" %}
{% api-method-summary %}
Get Items
{% endapi-method-summary %}

{% api-method-description %}
This endpoint will return a list of all Growtopia items including their data.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" %}
If you wish to fetch data for a specific item, you may specify its ID as a parameter in the path. 
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-query-parameters %}
{% api-method-parameter name="relationships" type="boolean" required=false %}
If you wish to include relationships \(prices, offers, etc...\) in the response, you may pass this key as a query parameter. This only works if you're fetching all items.
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Item data successfully retrieved.
{% endapi-method-response-example-description %}

```
[
  {
    "id": 2,
    "name": "Dirt",
    "description": "Yep, it's dirt.",
    "is_trending": 0,
    "is_daily_quest": 0,
    "daily_quest_quantity": 0,
    "category": "item",
    "type": null,
    "clothing_type": null,
    "is_hidden": 0,
    "is_locked": 0,
    "added_on": "2021-07-03 19:37:00",
    "prices": [],
    "offers": []
  }
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

You can search, filter and sort items through the endpoint mentioned above. You may pass the properties and their values as query parameters. Search and filter parameters **are mutually inclusive**.

**Search: `name`, `description`, `added_on`**

**Filter: `is_trending`, `is_daily_quest`, `category`, `type`, `clothing_type`, `is_hidden`, `is_locked`**

### **Sorting**

You may also sort the results by passing the **`sort_field`** and **`sort_direction`** query parameters.

**Field: `id`, `name`, `length(name)`, `added_on`**

**Direction: `asc`, `desc`**

### Relationships

By default, relationships are always enabled when getting one item, but always disabled when getting or searching all items.

You may request all or part of the relationships as follows:

* To request all relationships, pass the **`relationships`** query parameter without any value
* To request specific relationships, pass the **`relationships`** query parameter with a comma separated list of accepted relationships \(**`prices`**, **`offers`**\).

