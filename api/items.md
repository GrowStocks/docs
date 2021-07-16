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

{% api-method method="post" host="https://api.growstocks.org" path="/v1/items/:id" %}
{% api-method-summary %}
Create item
{% endapi-method-summary %}

{% api-method-description %}
This endpoint will create a new item.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
The item's ID
{% endapi-method-parameter %}

{% api-method-parameter name="name" type="integer" required=true %}
The item's name.
{% endapi-method-parameter %}

{% api-method-parameter name="rarity" type="string" required=false %}
The item's rarity.
{% endapi-method-parameter %}

{% api-method-parameter name="description" type="string" required=false %}
The item's description.
{% endapi-method-parameter %}

{% api-method-parameter name="category" type="string" required=false %}
The item's category \(item/iotm\)
{% endapi-method-parameter %}

{% api-method-parameter name="type" type="integer" required=false %}
The item's type.
{% endapi-method-parameter %}

{% api-method-parameter name="clothing\_type" type="integer" required=false %}
The item's clothing type.
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=201 %}
{% api-method-response-example-description %}
Item successfully created.
{% endapi-method-response-example-description %}

```
{
    "id": 606,
    "name": "Product",
    "description": "Try to quantify the PNG bus, maybe it will back up the multi-byte driver!",
    "is_trending": 0,
    "is_daily_quest": 0,
    "daily_quest_quantity": 0,
    "rarity": 999,
    "category": "item",
    "type": null,
    "clothing_type": null,
    "is_hidden": 0,
    "is_locked": 0,
    "added_on": "2021-07-15T23:07:32.000000Z"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %}
Item couldn't be created.
{% endapi-method-response-example-description %}

```
{
    "message": "The given data was invalid.",
    "errors": {
        "name": [
            "The name field is required."
        ],
        ...
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="put" host="https://api.growstocks.org" path="/v1/items/:id" %}
{% api-method-summary %}
Update item
{% endapi-method-summary %}

{% api-method-description %}
This endpoint will update the information corresponding to the item associated to the given ID. Only pass the fields you wish to update.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The item's ID.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-form-data-parameters %}
{% api-method-parameter name="id" type="integer" required=false %}
The item's ID.
{% endapi-method-parameter %}

{% api-method-parameter name="name" type="string" required=false %}
The item's name.
{% endapi-method-parameter %}

{% api-method-parameter name="rarity" type="integer" required=false %}
The item's rarity.
{% endapi-method-parameter %}

{% api-method-parameter name="description" type="string" required=false %}
The item's description.
{% endapi-method-parameter %}

{% api-method-parameter name="category" type="string" required=false %}
The item's category \(item/iotm\).
{% endapi-method-parameter %}

{% api-method-parameter name="type" type="string" required=false %}
The item's type.
{% endapi-method-parameter %}

{% api-method-parameter name="clothing\_type" type="string" required=false %}
The item's clothing type.
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Item successfully updated.
{% endapi-method-response-example-description %}

```
{
    "id": 606,
    "name": "Product",
    "description": "Try to quantify the PNG bus, maybe it will back up the multi-byte driver!",
    "is_trending": 0,
    "is_daily_quest": 0,
    "daily_quest_quantity": 0,
    "rarity": 999,
    "category": "item",
    "type": null,
    "clothing_type": null,
    "is_hidden": 0,
    "is_locked": 0,
    "added_on": "2021-07-15T23:07:32.000000Z"
}
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

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %}
Item couldn't be updated.
{% endapi-method-response-example-description %}

```
{
    "message": "The given data was invalid.",
    "errors": {
        "rarity": [
            "The rarity should be a number, between 1 and 999."
        ],
        ...
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="patch" host="https://api.growstocks.org" path="/v1/items/:id/trending/:action" %}
{% api-method-summary %}
Update trending status
{% endapi-method-summary %}

{% api-method-description %}
This endpoint will update the trending status for the item corresponding to the given ID.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The item's ID.
{% endapi-method-parameter %}

{% api-method-parameter name="action" type="string" required=true %}
The action to perform \(make/remove\).
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}
Trending status successfully updated.
{% endapi-method-response-example-description %}

```

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

{% api-method method="patch" host="https://api.growstocks.org" path="/v1/items/:id/daily-quest/:action" %}
{% api-method-summary %}
Update daily quest status
{% endapi-method-summary %}

{% api-method-description %}
This endpoint will update the daily quest status for the item corresponding to the given ID.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The item's ID.
{% endapi-method-parameter %}

{% api-method-parameter name="action" type="string" required=true %}
The action to perform \(make/remove\).
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-form-data-parameters %}
{% api-method-parameter name="daily\_quest\_quantity" type="integer" required=true %}
The amount needed for the daily quest. Only required when using the "make" action.
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Daily quest status successfully updated.
{% endapi-method-response-example-description %}

```

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

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %}
Daily quest status couldn't be updated.
{% endapi-method-response-example-description %}

```
{
    "message": "The given data was invalid.",
    "errors": {
        "daily_quest_quantity": [
            "The daily quest quantity should be a number, bigger than 1."
        ],
        ...
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="patch" host="https://api.growstocks.org" path="/v1/items/:id/hidden/:action" %}
{% api-method-summary %}
Update hidden status
{% endapi-method-summary %}

{% api-method-description %}
This endpoint will update the hidden status for the item corresponding to the given ID.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The item's ID.
{% endapi-method-parameter %}

{% api-method-parameter name="action" type="string" required=true %}
The action to perform \(make/remove\).
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}
Hidden status successfully updated.
{% endapi-method-response-example-description %}

```

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

{% api-method method="patch" host="https://api.growstocks.org" path="/v1/items/:id/locked/:action" %}
{% api-method-summary %}
Update locked status
{% endapi-method-summary %}

{% api-method-description %}
This endpoint will update the locked status for the item corresponding to the given ID.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The item's ID.
{% endapi-method-parameter %}

{% api-method-parameter name="action" type="string" required=true %}
The action to perform \(make/remove\).
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}
Locked status successfully updated.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Could not find an item marching this query.
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

{% api-method method="delete" host="https://api.growstocks.org" path="/v1/items/:id" %}
{% api-method-summary %}
Delete item
{% endapi-method-summary %}

{% api-method-description %}
This endpoint will delete the item corresponding to the given ID.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The item's ID.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}
Item successfully deleted.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Item does not exist.
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

