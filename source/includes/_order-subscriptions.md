# Order Subscriptions #

The order subscriptions API endpoint enables you to view subscriptions related to a specific order.

## Query parameters ##

|    Parameter    |  Type  |                                          Description                                           |
|-----------------|--------|------------------------------------------------------------------------------------------------|
| `status`        | string | Limit result set to subscriptions assigned a specific status. Options: `pending`, `active`, `on-hold`, `cancelled`, `switched`, `expired`, `pending-cancel` and `trash`. Default is `any`. |
| `customer`      | integer | Limit result set to subscriptions assigned to a specific customer.                            |
| `orderby`       | string  | Sort collection by subscription attribute. Options: `id`, `start_date`, `trial_end_date`, `next_payment_date`, `end_date` and `status`. Default is `start_date`. |
| `order`         | string  | Order sort attribute ascending or descending. Options: `asc` and `desc`. Default is `desc`.   |
| `_fields`       | string  | Limit response to specific fields. Expects a comma-separated list of fields.                  |

## Retrieve order subscriptions ##

This API lets you retrieve and view subscriptions for a specific order.

### HTTP request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-get">GET</i>
		<h6>/wp-json/wc/v3/orders/&lt;id&gt;/subscriptions</h6>
	</div>
</div>

```shell
curl https://example.com/wp-json/wc/v3/orders/1274/subscriptions \
	-u consumer_key:consumer_secret
```

```javascript
WooCommerce.get('orders/1274/subscriptions', function(err, data, res) {
  console.log(res);
});
```

```php
<?php print_r($woocommerce->get('orders/1274/subscriptions')); ?>
```

```python
print(wcapi.get("orders/1274/subscriptions").json())
```

```ruby
woocommerce.get("orders/1274/subscriptions").parsed_response
```

> JSON response example:

```json
[
    {
        "id": 1275,
        "parent_id": 1274,
        "status": "active",
        "currency": "USD",
        "version": "5.2.0",
        "prices_include_tax": true,
        "date_created": "2021-04-19T17:20:56",
        "date_modified": "2021-04-19T17:21:00",
        "discount_total": "0.00",
        "discount_tax": "0.00",
        "shipping_total": "0.00",
        "shipping_tax": "0.00",
        "cart_tax": "2.37",
        "total": "26.09",
        "total_tax": "2.37",
        "customer_id": 1,
        "order_key": "wc_order_6fS6FmzoZohhR",
        "billing": {
            "first_name": "James",
            "last_name": "Allan",
            "company": "",
            "address_1": "1 Main Rd",
            "address_2": "",
            "city": "Brisbane",
            "state": "QLD",
            "postcode": "4000",
            "country": "AU",
            "email": "james@example.com",
            "phone": "0000000000"
        },
        "shipping": {
            "first_name": "James",
            "last_name": "Allan",
            "company": "",
            "address_1": "1 Main Rd",
            "address_2": "",
            "city": "Brisbane",
            "state": "QLD",
            "postcode": "4000",
            "country": "AU"
        },
        "payment_method": "stripe",
        "payment_method_title": "Credit Card (Stripe)",
        "customer_ip_address": "192.0.2.1",
        "customer_user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 11_2_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36",
        "created_via": "checkout",
        "customer_note": "",
        "cart_hash": "413996ccaa9ff9e1d3375a5f919a6ba3",
        "number": "1275",
        "meta_data": [
            {
                "id": 52020,
                "key": "is_vat_exempt",
                "value": "no"
            }
        ],
        "line_items": [
            {
                "id": 1605,
                "name": "Weekly",
                "product_id": 1027,
                "variation_id": 0,
                "quantity": 3,
                "tax_class": "",
                "subtotal": "23.72",
                "subtotal_tax": "2.37",
                "total": "23.72",
                "total_tax": "2.37",
                "taxes": [
                    {
                        "id": 2,
                        "total": "2.371541",
                        "subtotal": "2.371541"
                    }
                ],
                "meta_data": [],
                "sku": "",
                "price": 7.9051383333333334,
                "parent_name": null
            }
        ],
        "tax_lines": [
            {
                "id": 1606,
                "rate_code": "US-TAX-1",
                "rate_id": 2,
                "label": "TAX",
                "compound": true,
                "tax_total": "2.37",
                "shipping_tax_total": "0.00",
                "rate_percent": 10,
                "meta_data": []
            }
        ],
        "shipping_lines": [],
        "fee_lines": [],
        "coupon_lines": [],
        "date_created_gmt": "2021-04-19T07:20:56",
        "date_modified_gmt": "2021-04-19T07:21:00",
        "start_date": "2021-04-19T17:20:56",
        "trial_end_date": null,
        "next_payment_date": "2021-04-26T17:20:56",
        "end_date": null,
        "billing_period": "week",
        "billing_interval": "1",
        "_links": {
            "self": [
                {
                    "href": "https://example.com/wp-json/wc/v3/subscriptions/1275"
                }
            ],
            "collection": [
                {
                    "href": "https://example.com/wp-json/wc/v3/orders/1274/subscriptions"
                }
            ],
            "parent_order": [
                {
                    "href": "https://example.com/wp-json/wc/v3/orders/1274"
                }
            ],
            "customer": [
                {
                    "href": "https://example.com/wp-json/wc/v3/customers/1"
                }
            ]
        }
    }
]
```

