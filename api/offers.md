---
description: >-
  The prices API allows you to fetch marketplace data directly from our
  up-to-date database.
---

# Offers

{% api-method method="get" host="https://api.growstocks.org" path="/v1/offers/:id" %}
{% api-method-summary %}
Get Offers
{% endapi-method-summary %}

{% api-method-description %}
This endpoint will return a list of all marketplace offers.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" %}
If you wish to fetch the offer corresponding to the specified ID, you may specify it as a path parameter.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Marketplace data successfully retrieved.
{% endapi-method-response-example-description %}

```
[
  {
    "id": 1,
    "growid": "q773pj561j",
    "guest_id": 86,
    "item_id": 770,
    "quantity": 4152,
    "price": 6133,
    "world_name": "SL7RNK84H4X7564EA5G1",
    "type": 0,
    "is_approved": 0,
    "created_at": "2021-07-03T19:37:04.000000Z",
    "updated_at": "2021-07-03T19:37:04.000000Z",
    "item": {}
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
  "message": "No query results for model [App\\Models\\Item] :item_name"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Searching/Filtering

You can search, filter and sort items through the endpoint mentioned above. You may pass the properties and their values as query parameters. Search and filter parameters **are mutually inclusive**.

**Search: `growid`, `world_name`, `created_at`, `updated_at`**

**Filter: `guest_id`, `item_id`, `quantity`, `price`, `world_name`, `type`, `is_approved`**

### **Sorting**

You may also sort the results by passing the **`sort_field`** and **`sort_direction`** query parameters.

**Field: `id`, `growid`, `length(growid)`, `item_id`, `quantity`, `price`, `world_name`, `length(world_name)`, `created_at`, `updated_at`**

**Direction: `asc`, `desc`**

### Relationships

By default, relationships are always enabled when getting one offer, but always disabled when getting or searching all offers.

You may request all or part of the relationships as follows:

* To request all relationships, pass the **`relationships`** query parameter without any value
* To request specific relationships, pass the **`relationships`** query parameter with a comma separated list of accepted relationships \(**`item`**, **`guest`**\).

{% api-method method="post" host="https://api.growstocks.org" path="/v1/offers" %}
{% api-method-summary %}
Create Offer
{% endapi-method-summary %}

{% api-method-description %}
This endpoint will create a marketplace offer for the specified item.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="item\_name" type="string" required=true %}
The name of the item which offer will be created.
{% endapi-method-parameter %}

{% api-method-parameter name="growid" type="string" required=true %}
The GrowID of the user creating the advertisement. Must be 3 to 18 characters in length, exclusively containing alphanumeric characters.
{% endapi-method-parameter %}

{% api-method-parameter name="quantity" type="integer" required=true %}
The quantity of the advertised item. Must be greater than 1.
{% endapi-method-parameter %}

{% api-method-parameter name="price" type="integer" required=true %}
The price of the advertised item. Must be greater than 1.
{% endapi-method-parameter %}

{% api-method-parameter name="world\_name" type="string" required=true %}
The world name where the item is being bought or sold. Must be 1 to 24 characters in length, exclusively alphanumeric characters.
{% endapi-method-parameter %}

{% api-method-parameter name="type" type="integer" required=true %}
Whether the user is buying \(0\) or selling \(1\) the advertised item.
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=201 %}
{% api-method-response-example-description %}
Marketplace offer successfully created.
{% endapi-method-response-example-description %}

```
{
  "id": 1,
  "growid": "q773pj561j",
  "guest_id": 86,
  "item_id": 770,
  "quantity": 4152,
  "price": 6133,
  "world_name": "SL7RNK84H4X7564EA5G1",
  "type": 0,
  "is_approved": 0,
  "created_at": "2021-07-03T19:37:04.000000Z",
  "updated_at": "2021-07-03T19:37:04.000000Z",
  "item": {}
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %}
Marketplace offer couldn't be created.
{% endapi-method-response-example-description %}

```
{
    "message": "The given data was invalid.",
    "errors": {
        "item_name": [
            "The selected item name is invalid."
        ],
        ...
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="delete" host="https://api.growstocks.org" path="/v1/offers/:id" %}
{% api-method-summary %}
Delete Offer
{% endapi-method-summary %}

{% api-method-description %}
This endpoint will delete the offer corresponding to the given ID.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
The ID of the offer you wish to delete.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}
Marketplace offer successfully deleted.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Marketplace offer does not exist.
{% endapi-method-response-example-description %}

```
{
  "message": "No query results for model [App\\Models\\Offer] 550"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

