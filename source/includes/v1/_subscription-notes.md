# Subscription Notes #

The subscription notes API allows you to create, view, and delete individual subscription notes on a subscription.
Subscription notes are added by administrators and programmatically to store data about a subscription, or subscription events.

## Subscription Note Properties ##

|    Attribute    |    Type   |                                                     Description                                                     |
|-----------------|-----------|---------------------------------------------------------------------------------------------------------------------|
| `id`            | integer   | Unique identifier for the resource. <i class="label label-info">read-only</i>                                       |
| `date_created`  | date-time | The date the subscription note was created, in the site's timezone. <i class="label label-info">read-only</i>              |
| `note`          | string    | Subscription note. <i class="label label-info">required</i>                                                                |
| `customer_note` | boolean   | Shows/define if the note is only for reference or for the customer (the user will be notified). Default is `false`. |

## Create a Subscription Note ##

This API helps you to create a new note for a subscription.

### HTTP request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-post">POST</i>
		<h6>/wp-json/wc/v1/subscriptions/&lt;id&gt;/notes</h6>
	</div>
</div>

```shell
curl -X POST https://example.com/wp-json/wc/v1/subscriptions/645/notes \
	-u consumer_key:consumer_secret \
	-H "Content-Type: application/json" \
	-d '{
  "note": "Subscription ok!!!"
}'
```

```javascript
var data = {
  note: 'Subscription ok!!!'
};

WooCommerce.post('subscriptions/645/notes', data, function(err, data, res) {
  console.log(res);
});
```

```php
<?php
$data = [
    'note' => 'Subscription ok!!!'
];

print_r($woocommerce->post('subscriptions/645/notes', $data));
?>
```

```python
data = {
    "note": "Subscription ok!!!"
}

print(wcapi.post("subscriptions/645/notes", data).json())
```

```ruby
data = {
  note: "Subscription ok!!!"
}

woocommerce.post("subscriptions/645/notes", data).parsed_response
```

> JSON response example:

```json
{
  "id": 51,
  "date_created": "2016-05-13T20:51:55",
  "note": "Subscription ok!!!",
  "customer_note": false,
  "_links": {
    "self": [
      {
        "href": "https://example.com/wp-json/wc/v1/subscriptions/118/notes/51"
      }
    ],
    "collection": [
      {
        "href": "https://example.com/wp-json/wc/v1/subscriptions/118/notes"
      }
    ],
    "up": [
      {
        "href": "https://example.com/wp-json/wc/v1/subscriptions/118"
      }
    ]
  }
}
```

## Retrieve a Subscription Note ##

This API lets you retrieve and view a specific note from a subscription.

### HTTP request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-get">GET</i>
		<h6>/wp-json/wc/v1/subscriptions/&lt;id&gt;/notes/&lt;note_id&gt;</h6>
	</div>
</div>

```shell
curl https://example.com/wp-json/wc/v1/subscriptions/645/notes/51 \
	-u consumer_key:consumer_secret
```

```javascript
WooCommerce.get('subscriptions/645/notes/51', function(err, data, res) {
  console.log(res);
});
```

```php
<?php print_r($woocommerce->get('subscriptions/645/notes/51')); ?>
```

```python
print(wcapi.get("subscriptions/645/notes/51").json())
```

```ruby
woocommerce.get("subscriptions/645/notes/51").parsed_response
```

> JSON response example:

```json
{
  "id": 51,
  "date_created": "2016-05-13T20:51:55",
  "note": "Subscription ok!!!",
  "customer_note": false,
  "_links": {
    "self": [
      {
        "href": "https://example.com/wp-json/wc/v1/subscriptions/118/notes/51"
      }
    ],
    "collection": [
      {
        "href": "https://example.com/wp-json/wc/v1/subscriptions/118/notes"
      }
    ],
    "up": [
      {
        "href": "https://example.com/wp-json/wc/v1/subscriptions/118"
      }
    ]
  }
}
```

## List all Subscription Notes ##

This API helps you to view all the notes from a subscription.

### HTTP request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-get">GET</i>
		<h6>/wp-json/wc/v1/subscriptions/&lt;id&gt;/notes</h6>
	</div>
</div>

```shell
curl https://example.com/wp-json/wc/v1/subscriptions/645/notes \
	-u consumer_key:consumer_secret
```

```javascript
WooCommerce.get('subscriptions/645/notes', function(err, data, res) {
  console.log(res);
});
```

```php
<?php print_r($woocommerce->get('subscriptions/645/notes')); ?>
```

```python
print(wcapi.get("subscriptions/645/notes").json())
```

```ruby
woocommerce.get("subscriptions/645/notes").parsed_response
```

> JSON response example:

```json
[
  {
    "id": 51,
    "date_created": "2016-05-13T20:51:55",
    "note": "Subscription ok!!!",
    "customer_note": false,
    "_links": {
      "self": [
        {
          "href": "https://example.com/wp-json/wc/v1/subscriptions/118/notes/51"
        }
      ],
      "collection": [
        {
          "href": "https://example.com/wp-json/wc/v1/subscriptions/118/notes"
        }
      ],
      "up": [
        {
          "href": "https://example.com/wp-json/wc/v1/subscriptions/118"
        }
      ]
    }
  },
  {
    "id": 46,
    "date_created": "2016-05-03T18:10:43",
    "note": "Subscription status changed from On-hold to Active.",
    "customer_note": false,
    "_links": {
      "self": [
        {
          "href": "https://example.com/wp-json/wc/v1/subscriptions/118/notes/46"
        }
      ],
      "collection": [
        {
          "href": "https://example.com/wp-json/wc/v1/subscriptions/118/notes"
        }
      ],
      "up": [
        {
          "href": "https://example.com/wp-json/wc/v1/subscriptions/118"
        }
      ]
    }
  }
]
```

## Delete a Subscription Note ##

This API helps you delete a subscription note.

### HTTP request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-delete">DELETE</i>
		<h6>/wp-json/wc/v1/subscriptions/&lt;id&gt;/notes/&lt;note_id&gt;</h6>
	</div>
</div>

```shell
curl -X DELETE https://example.com/wp-json/wc/v1/subscriptions/645/notes/51?force=true \
	-u consumer_key:consumer_secret
```

```javascript
WooCommerce.delete('subscriptions/645/notes/51?force=true', function(err, data, res) {
  console.log(res);
});
```

```php
<?php print_r($woocommerce->delete('subscriptions/645/notes/51', ['force' => true])); ?>
```

```python
print(wcapi.delete("subscriptions/645/notes/51?force=true").json())
```

```ruby
woocommerce.delete("subscriptions/645/notes/51", force: true).parsed_response
```

> JSON response example:

```json
{
  "id": 51,
  "date_created": "2016-05-13T20:51:55",
  "note": "Subscription ok!!!",
  "customer_note": false,
  "_links": {
    "self": [
      {
        "href": "https://example.com/wp-json/wc/v1/subscriptions/118/notes/51"
      }
    ],
    "collection": [
      {
        "href": "https://example.com/wp-json/wc/v1/subscriptions/118/notes"
      }
    ],
    "up": [
      {
        "href": "https://example.com/wp-json/wc/v1/subscriptions/118"
      }
    ]
  }
}
```
#### Available parameters ####

| Parameter |  Type  |                          Description                          |
|-----------|--------|---------------------------------------------------------------|
| `force`   | string | Required to be `true`, as resource does not support trashing. |