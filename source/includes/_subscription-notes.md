# Subscription Notes #

The subscription notes API allows you to create, view, and delete individual subscription notes.
Subscription notes are added by administrators and programmatically to store data about a subscription, or to record a subscription event.

## Subscription note properties ##

|      Attribute     |    Type   |                                                                    Description                                                                   |
|--------------------|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| `id`               | integer   | Unique identifier for the resource. <i class="label label-info">read-only</i>                                                                    |
| `author`           | string    | Subscription note author <i class="label label-info">read-only</i>                                                                               |
| `date_created   `  | date-time | The date the subscription note was created, in the site's timezone. <i class="label label-info">read-only</i>                                    |
| `date_created_gmt` | date-time | The date the subscription note was created, as GMT. <i class="label label-info">read-only</i>                                                    |
| `note`             | string    | Subscription note. <i class="label label-info">required</i>                                                                                      |
| `customer_note`    | boolean   | If true, the note will be shown to customers and they will be notified. If false, the note will be for admin reference only. Default is `false`. |
| `added_by_user`    | boolean   | If true, this note will be attributed to the current user. If false, the note will be attributed to the system. Default is`false`.               |

## Create a subscription note ##

This API helps you to create a new note for a subscription.

### HTTP request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-post">POST</i>
		<h6>/wp-json/wc/v3/subscriptions/&lt;id&gt;/notes</h6>
	</div>
</div>

```shell
curl -X POST https://example.com/wp-json/wc/v3/subscriptions/1275/notes \
	-u consumer_key:consumer_secret \
	-H "Content-Type: application/json" \
	-d '{
  "note": "Example subscription note."
}'
```

```javascript
var data = {
  note: 'Example subscription note.'
};

WooCommerce.post('subscriptions/1275/notes', data, function(err, data, res) {
  console.log(res);
});
```

```php
<?php
$data = [
    'note' => 'Example subscription note.'
];

print_r($woocommerce->post('subscriptions/1275/notes', $data));
?>
```

```python
data = {
    "note": "Example subscription note."
}

print(wcapi.post("subscriptions/1275/notes", data).json())
```

```ruby
data = {
  note: "Example subscription note."
}

woocommerce.post("subscriptions/1275/notes", data).parsed_response
```

> JSON response example:

```json
{
    "id": 2807,
    "author": "WooCommerce",
    "date_created": "2021-04-22T13:51:07",
    "date_created_gmt": "2021-04-22T03:51:07",
    "note": "Example subscription note.",
    "customer_note": false,
    "_links": {
        "self": [
            {
                "href": "https://example.com/wp-json/wc/v3/subscriptions/1275/notes/2807"
            }
        ],
        "collection": [
            {
                "href": "https://example.com/wp-json/wc/v3/subscriptions/1275/notes"
            }
        ],
        "up": [
            {
                "href": "https://example.com/wp-json/wc/v3/subscriptions/1275"
            }
        ]
    }
}
```

## Retrieve a subscription note ##

This API lets you retrieve and view a specific note from a subscription.

### HTTP request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-get">GET</i>
		<h6>/wp-json/wc/v3/subscriptions/&lt;id&gt;/notes/&lt;note_id&gt;</h6>
	</div>
</div>

```shell
curl https://example.com/wp-json/wc/v3/subscriptions/1275/notes/2807 \
	-u consumer_key:consumer_secret
```

```javascript
WooCommerce.get('subscriptions/1275/notes/2807', function(err, data, res) {
  console.log(res);
});
```

```php
<?php print_r($woocommerce->get('subscriptions/1275/notes/2807')); ?>
```

```python
print(wcapi.get("subscriptions/1275/notes/2807").json())
```

```ruby
woocommerce.get("subscriptions/1275/notes/2807").parsed_response
```

> JSON response example:

```json
{
    "id": 2807,
    "author": "WooCommerce",
    "date_created": "2021-04-22T13:51:07",
    "date_created_gmt": "2021-04-22T03:51:07",
    "note": "Example subscription note.",
    "customer_note": false,
    "_links": {
        "self": [
            {
                "href": "https://example.com/wp-json/wc/v3/subscriptions/1275/notes/2807"
            }
        ],
        "collection": [
            {
                "href": "https://example.com/wp-json/wc/v3/subscriptions/1275/notes"
            }
        ],
        "up": [
            {
                "href": "https://example.com/wp-json/wc/v3/subscriptions/1275"
            }
        ]
    }
}
```

## List all subscription notes ##

This API retrieves all the notes from a subscription.

### HTTP request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-get">GET</i>
		<h6>/wp-json/wc/v3/subscriptions/&lt;id&gt;/notes</h6>
	</div>
</div>

```shell
curl https://example.com/wp-json/wc/v3/subscriptions/1275/notes \
	-u consumer_key:consumer_secret
```

```javascript
WooCommerce.get('subscriptions/1275/notes', function(err, data, res) {
  console.log(res);
});
```

```php
<?php print_r($woocommerce->get('subscriptions/1275/notes')); ?>
```

```python
print(wcapi.get("subscriptions/1275/notes").json())
```

```ruby
woocommerce.get("subscriptions/1275/notes").parsed_response
```

> JSON response example:

```json
[
    {
        "id": 2716,
        "author": "WooCommerce",
        "date_created": "2021-04-19T17:21:00",
        "date_created_gmt": "2021-04-19T07:21:00",
        "note": "Payment status marked complete.",
        "customer_note": false,
        "_links": {
            "self": [
                {
                    "href": "https://example.com/wp-json/wc/v3/subscriptions/1275/notes/2716"
                }
            ],
            "collection": [
                {
                    "href": "https://example.com/wp-json/wc/v3/subscriptions/1275/notes"
                }
            ],
            "up": [
                {
                    "href": "https://example.com/wp-json/wc/v3/subscriptions/1275"
                }
            ]
        }
    },
    {
        "id": 2717,
        "author": "WooCommerce",
        "date_created": "2021-04-19T17:21:00",
        "date_created_gmt": "2021-04-19T07:21:00",
        "note": "Status changed from Pending to Active.",
        "customer_note": false,
        "_links": {
            "self": [
                {
                    "href": "https://example.com/wp-json/wc/v3/subscriptions/1275/notes/2717"
                }
            ],
            "collection": [
                {
                    "href": "https://example.com/wp-json/wc/v3/subscriptions/1275/notes"
                }
            ],
            "up": [
                {
                    "href": "https://example.com/wp-json/wc/v3/subscriptions/1275"
                }
            ]
        }
    }
]

```

## Delete a subscription note ##

This API deletes a subscription note.

### HTTP request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-delete">DELETE</i>
		<h6>/wp-json/wc/v3/subscriptions/&lt;id&gt;/notes/&lt;note_id&gt;</h6>
	</div>
</div>

```shell
curl -X DELETE https://example.com/wp-json/wc/v3/subscriptions/1275/notes/2716?force=true \
	-u consumer_key:consumer_secret
```

```javascript
WooCommerce.delete('subscriptions/1275/notes/2716?force=true', function(err, data, res) {
  console.log(res);
});
```

```php
<?php print_r($woocommerce->delete('subscriptions/1275/notes/2716', ['force' => true])); ?>
```

```python
print(wcapi.delete("subscriptions/1275/notes/2716?force=true").json())
```

```ruby
woocommerce.delete("subscriptions/1275/notes/2716", force: true).parsed_response
```

> JSON response example:

```json
{
    "id": 2716,
    "author": "WooCommerce",
    "date_created": "2021-04-19T17:21:00",
    "date_created_gmt": "2021-04-19T07:21:00",
    "note": "Payment status marked complete.",
    "customer_note": false,
    "_links": {
        "self": [
            {
                "href": "https://example.com/wp-json/wc/v3/subscriptions/1275/notes/2716"
            }
        ],
        "collection": [
            {
                "href": "https://example.com/wp-json/wc/v3/subscriptions/1275/notes"
            }
        ],
        "up": [
            {
                "href": "https://example.com/wp-json/wc/v3/subscriptions/1275"
            }
        ]
    }
}
```
#### Available parameters ####

| Parameter |  Type  |                            Description                            |
|-----------|--------|-------------------------------------------------------------------|
| `force`   | string | Required to be `true`, as the resource does not support trashing. |