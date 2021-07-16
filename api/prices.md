---
description: >-
  The prices API allows you to fetch price data directly from our up-to-date
  database.
---

# Prices

{% api-method method="get" host="https://api.growstocks.org" path="/v1/prices/:id" %}
{% api-method-summary %}
Get prices
{% endapi-method-summary %}

{% api-method-description %}
This endpoint will return a list of all prices. For security reasons, fetching all items through this endpoint is restricted to specific API tokens.
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

{% api-method method="post" host="https://api.growstocks.org" path="/v1/prices" %}
{% api-method-summary %}
Create price
{% endapi-method-summary %}

{% api-method-description %}
This endpoint will create a new price.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="item\_id" type="integer" required=true %}
The ID of the item you are creating a price for.
{% endapi-method-parameter %}

{% api-method-parameter name="quantity" type="integer" required=true %}
The quantity of the item being traded.
{% endapi-method-parameter %}

{% api-method-parameter name="price" type="integer" required=true %}
The amount of World Locks the item is being sold for.
{% endapi-method-parameter %}

{% api-method-parameter name="price\_status" type="integer" required=true %}
The item's price status.
{% endapi-method-parameter %}

{% api-method-parameter name="demand\_status" type="integer" required=true %}
The item's demand status.
{% endapi-method-parameter %}

{% api-method-parameter name="source\_world\_name" type="string" required=true %}
The world name where the trade has been spotted.
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=201 %}
{% api-method-response-example-description %}
Price successfully created.
{% endapi-method-response-example-description %}

```
{
    "id": 401,
    "item_id": 165,
    "quantity": 201,
    "price": 792,
    "price_status": 2,
    "demand_status": 1,
    "editor_id": 100,
    "is_approved": 0,
    "is_suggestion": 0,
    "is_daily_quest": 0,
    "counted_as": 1,
    "source_world_name": "BUYAWESOME",
    "inspector_id": null,
    "created_at": "2021-07-16T19:34:08.000000Z",
    "updated_at": "2021-07-16T19:34:08.000000Z"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %}
Price couldn't be created.
{% endapi-method-response-example-description %}

```
{
    "message": "The given data was invalid.",
    "errors": {
        "item_id": [
            "The selected item id is invalid."
        ],
        ...
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="put" host="https://api.growstocks.org" path="/v1/prices/:id" %}
{% api-method-summary %}
Update price
{% endapi-method-summary %}

{% api-method-description %}
This endpoint will update the information corresponding to the price associated to the given ID. For security reasons, this endpoint is disabled and cannot be used by anyone.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The ID of the price you wish to update.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-form-data-parameters %}
{% api-method-parameter name="item\_id" type="integer" required=false %}
The item's ID.
{% endapi-method-parameter %}

{% api-method-parameter name="quantity" type="integer" required=false %}
The quantity of the item being traded.
{% endapi-method-parameter %}

{% api-method-parameter name="price" type="integer" required=false %}
The amount of World Locks the item is being sold for.
{% endapi-method-parameter %}

{% api-method-parameter name="price\_status" type="integer" required=false %}
The item's price status.
{% endapi-method-parameter %}

{% api-method-parameter name="demand\_status" type="integer" required=false %}
The item's demand status.
{% endapi-method-parameter %}

{% api-method-parameter name="source\_world\_name" type="string" required=false %}
The world name where the trade has been spotted.
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Price successfully updated.
{% endapi-method-response-example-description %}

```
{
    "id": 401,
    "item_id": 165,
    "quantity": 201,
    "price": 792,
    "price_status": 2,
    "demand_status": 1,
    "editor_id": 100,
    "is_approved": 0,
    "is_suggestion": 0,
    "is_daily_quest": 0,
    "counted_as": 1,
    "source_world_name": "BUYAWESOME",
    "inspector_id": null,
    "created_at": "2021-07-16T19:34:08.000000Z",
    "updated_at": "2021-07-16T19:34:08.000000Z"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Could not find a price matching this query.
{% endapi-method-response-example-description %}

```
{
  "message": "No query results for model [App\\Models\\Price] :id"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %}
Price couldn't be updated.
{% endapi-method-response-example-description %}

```
{
    "message": "The given data was invalid.",
    "errors": {
        "quantity": [
            "The quantity should be an integer, bigger than 1."
        ],
        ...
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="patch" host="https://api.growstocks.org" path="/v1/items/:item/approved/:action" %}
{% api-method-summary %}
Update approval status
{% endapi-method-summary %}

{% api-method-description %}
This endpoint will update the approval status of the price corresponding to the given ID.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The ID of the price you with to approve.
{% endapi-method-parameter %}

{% api-method-parameter name="action" type="string" required=true %}
The action to perform \(make/remove\).
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}
Approval status successfully updated.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Could not find a price matching this query.
{% endapi-method-response-example-description %}

```
{
  "message": "No query results for model [App\\Models\\Price] :id"
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
This endpoint will delete the price corresponding to the given ID.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The ID of the price you wish to delete.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}
Price successfully deleted.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Could not find a price matching this query.
{% endapi-method-response-example-description %}

```
{
  "message": "No query results for model [App\\Models\\Price] :id"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
## **Zoom on statuses**

Below, you'll find the string description corresponding to the integer associated to each status type.

### Price status

```text
1 - STABLE
2 - SEMI-STABLE
3 - UNSTABLE
```

### Demand status

```text
1 - STABLE
2 - SEMI-STABLE
3 - IN-DEMAND
4 - LOW-DEMAND
```
{% endhint %}

