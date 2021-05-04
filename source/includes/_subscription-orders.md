# Subscription Orders #

The subscription orders API endpoints enables you to view orders related to a subscription.

## Subscription order properties ##

|       Attribute        |    Type   |                                                                             Description                                                                              |
|------------------------|:---------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `id`                   | integer   | Unique identifier for the resource. <i class="label label-info">read-only</i>                                                                                        |
| `parent_id`            | integer   | Parent order ID.                                                                                                                                                     |
| `status`               | string    | Order status. Default is `pending`. Options (plugins may include new status): `pending`, `processing`, `on-hold`, `completed`, `cancelled`, `refunded` and `failed`. |
| `currency`             | string    | Currency the order was created with, in ISO format, e.g `USD`. Default is the current store currency.                                                                |
| `version`              | string    | Version of WooCommerce when the order was made. <i class="label label-info">read-only</i>                                                                            |
| `prices_include_tax`   | boolean   | Shows if the prices included tax during checkout. <i class="label label-info">read-only</i>                                                                          |
| `date_created`         | date-time | The date the order was created, in the site's timezone. <i class="label label-info">read-only</i>                                                                    |
| `date_modified`        | date-time | The date the order was last modified, in the site's timezone. <i class="label label-info">read-only</i>                                                              |
| `date_completed`       | date-time | The date the order was completed, in the site's timezone. <i class="label label-info">read-only</i>                                                                  |
| `date_paid`            | date-time | The date the order has been paid, in the site's timezone. <i class="label label-info">read-only</i>                                                                  |
| `date_created_gmt`     | data-time | The date the order was created, as GMT.                                                                                                                              |
| `date_modified_gmt`    | data-time | The date the order was modified, as GMT.                                                                                                                             |
| `date_completed_gmt`   | data-time | The date the order was completed, as GMT.                                                                                                                            |
| `date_paid_gmt`        | data-time | The date the order was paid, as GMT.                                                                                                                                 |
| `discount_total`       | string    | Total discount amount for the order. <i class="label label-info">read-only</i>                                                                                       |
| `discount_tax`         | string    | Total discount tax amount for the order. <i class="label label-info">read-only</i>                                                                                   |
| `shipping_total`       | string    | Total shipping amount for the order. <i class="label label-info">read-only</i>                                                                                       |
| `shipping_tax`         | string    | Total shipping tax amount for the order. <i class="label label-info">read-only</i>                                                                                   |
| `cart_tax`             | string    | Sum of line item taxes only. <i class="label label-info">read-only</i>                                                                                               |
| `total`                | string    | Grand total. <i class="label label-info">read-only</i>                                                                                                               |
| `total_tax`            | string    | Sum of all taxes. <i class="label label-info">read-only</i>                                                                                                          |
| `customer_id`          | integer   | User ID who owns the order. Use `0` for guests. Default is `0`.                                                                                                      |
| `order_key`            | string    | Order key. <i class="label label-info">read-only</i>                                                                                                                 |
| `billing`              | array     | Billing address. See [customer billing address properties](#billing-address-properties).                                                                             |
| `shipping`             | array     | Shipping address. See [customer shipping address properties](#shipping-address-properties).                                                                          |
| `payment_method`       | string    | Payment method ID.                                                                                                                                                   |
| `payment_method_title` | string    | Payment method title.                                                                                                                                                |
| `transaction_id`       | string    | Unique transaction ID. In write-mode only is available if `set_paid` is `true`.                                                                                      |
| `customer_ip_address`  | string    | Customer's IP address. <i class="label label-info">read-only</i>                                                                                                     |
| `customer_user_agent`  | string    | User agent of the customer. <i class="label label-info">read-only</i>                                                                                                |
| `created_via`          | string    | Shows where the order was created. <i class="label label-info">read-only</i>                                                                                         |
| `customer_note`        | string    | Note left by customer during checkout.                                                                                                                               |
| `cart_hash`            | string    | MD5 hash of cart items to ensure orders are not modified. <i class="label label-info">read-only</i>                                                                  |
| `number`               | string    | The order's number.                                                                                                                                           |
| `meta_data`            | array     | Meta data. See [meta data properties](#meta-data-properties).                                                                                                        |
| `line_items`           | array     | Line items data. See [order line items properties](#order-line-item-properties).                                                                                     |
| `tax_lines`            | array     | Tax lines data. See [order tax lines properties](#order-tax-line-item-properties). <i class="label label-info">read-only</i>                                         |
| `shipping_lines`       | array     | Shipping lines data. See [order shipping lines properties](#order-shipping-line-item-properties).                                                                    |
| `fee_lines`            | array     | Fee lines data. See [order fee lines properites](#order-fee-lines-properties).                                                                                       |
| `coupon_lines`         | array     | Coupons line data. See [order coupon lines properties](#order-coupon-line-properties).                                                                               |
| `order_type`           | string    | The order's relationship type to the subscription. Can be `'parent'`, `'renewal'`, or `'switch'` <i class="label label-info">read-only</i>                           |

### Billing address properties ###

|   Attribute    |   Type  |                                          Description                                           |
|----------------|---------|------------------------------------------------------------------------------------------------|
| `first_name`   | string  | First name.                                                                                    |
| `last_name`    | string  | Last name.                                                                                     |
| `company`      | string  | Company name.                                                                                  |
| `address_1`    | string  | Address line 1.                                                                                |
| `address_2`    | string  | Address line 2.                                                                                |
| `city`         | string  | City name.                                                                                     |
| `state`        | string  | ISO code or name of the state, province or district.                                           |
| `postcode`     | string  | Postal code.                                                                                   |
| `country`      | string  | Country code in ISO 3166-1 alpha-2 format.                                                     |
| `email`        | string  | Email address.                                                                                 |
| `phone`        | string  | Phone number.                                                                                  |

### Shipping address properties ###

|   Attribute    |   Type  |                                          Description                                           |
|----------------|---------|------------------------------------------------------------------------------------------------|
| `first_name`   | string  | First name.                                                                                    |
| `last_name`    | string  | Last name.                                                                                     |
| `company`      | string  | Company name.                                                                                  |
| `address_1`    | string  | Address line 1.                                                                                |
| `address_2`    | string  | Address line 2.                                                                                |
| `city`         | string  | City name.                                                                                     |
| `state`        | string  | ISO code or name of the state, province or district.                                           |
| `postcode`     | string  | Postal code.                                                                                   |
| `country`      | string  | Country code in ISO 3166-1 alpha-2 format.                                                     |

### Meta data properties ###

|   Attribute    |   Type  |                                          Description                                           |
|----------------|---------|------------------------------------------------------------------------------------------------|
| `id`           | integer | Meta ID. <i class="label label-info">read-only</i>                                             |
| `key`          | string  | Meta key.                                                                                      |
| `value`        | string  | Meta value.                                                                                    |

### Order line item properties ###

|   Attribute    |   Type  |                                                       Description                                                          |
|----------------|---------|----------------------------------------------------------------------------------------------------------------------------|
| `id`           | integer | Item ID. <i class="label label-info">read-only</i>                                                                         |
| `name`         | string  | Product name. <i class="label label-info">read-only</i>                                                                    |
| `product_id`   | integer | Product ID.                                                                                                                |
| `variation_id` | integer | Variation ID, if applicable.                                                                                               |
| `quantity`     | integer | Quantity ordered.                                                                                                          |
| `tax_class`    | string  | Slug of the tax class of product.                                                                                          |
| `subtotal`     | string  | Line subtotal (before discounts).                                                                                          |
| `subtotal_tax` | string  | Line subtotal tax (before discounts). <i class="label label-info">read-only</i>                                            |
| `total`        | string  | Line total (after discounts).                                                                                              |
| `total_tax`    | string  | Line total tax (after discounts). <i class="label label-info">read-only</i>                                                |
| `taxes`        | array   | Line taxes. See [order item taxes properties](#order-item-taxes-properties) <i class="label label-info">read-only</i>      |
| `meta_data`    | array   | Meta data. See [order item meta data properties](#order-item-meta-data-properties)                                         |
| `sku`          | string  | Product SKU. <i class="label label-info">read-only</i>                                                                     |
| `price`        | integer | Product price. <i class="label label-info">read-only</i>                                                                   |
| `parent_name`  | string  | Parent product name if the product is a variation.                                                                         |

### Order item taxes properties ###

|   Attribute    |   Type  |                                          Description                                            |
|----------------|---------|-------------------------------------------------------------------------------------------------|
| `id`           | integer | Tax rate ID.                                                                                    |
| `total`        | string  | Tax total.                                                                                      |
| `subtotal`     | string  | Tax subtotal.                                                                                   |

### Order item meta data properties ###

|    Attribute    |   Type  |                                          Description                                            |
|-----------------|---------|-------------------------------------------------------------------------------------------------|
| `id`            | integer | Meta ID.                                                                                        |
| `key`           | string  | Meta key.                                                                                       |
| `value`         | string  | Meta value.                                                                                     |
| `display_key`   | string  | Meta key for UI display.                                                                        |
| `display_value` | string  | Meta value for UI display.                                                                      |

### Order tax line item properties ###

|      Attribute       |   Type  |                                                             Description                                                             |
|----------------------|---------|-------------------------------------------------------------------------------------------------------------------------------------|
| `id`                 | integer | Item ID. <i class="label label-info">read-only</i>                                                                                  |
| `rate_code`          | string  | Tax rate code. <i class="label label-info">read-only</i>                                                                            |
| `rate_id`            | string  | Tax rate ID. <i class="label label-info">read-only</i>                                                                              |
| `label`              | string  | Tax rate label. <i class="label label-info">read-only</i>                                                                           |
| `compound`           | boolean | Show if is a compound tax rate. Compound tax rates are applied on top of other tax rates. <i class="label label-info">read-only</i> |
| `tax_total`          | string  | Tax total (not including shipping taxes). <i class="label label-info">read-only</i>                                                 |
| `shipping_tax_total` | string  | Shipping tax total. <i class="label label-info">read-only</i>                                                                       |
| `rate_percent`       | integer | The tax % rate.                                                                                                                     |
| `meta_data`          | array   | Meta data. See [order item meta data properties](#order-item-meta-data-properties)                                                  |

### Order shipping line item properties ###

|   Attribute    |   Type  |                                                     Description                                                       |
|----------------|---------|-----------------------------------------------------------------------------------------------------------------------|
| `id`           | integer | Item ID. <i class="label label-info">read-only</i>                                                                    |
| `method_title` | string  | Shipping method name.                                                                                                 |
| `method_id`    | string  | Shipping method ID. <i class="label label-info">required</i>                                                          |
| `instance_id`  | string  | Shipping instance ID.                                                                                                 |
| `total`        | string  | Line total (after discounts).                                                                                         |
| `total_tax`    | string  | Line total tax (after discounts). <i class="label label-info">read-only</i>                                           |
| `taxes`        | array   | Line taxes. See [order item taxes properties](#order-item-taxes-properties) <i class="label label-info">read-only</i> |
| `meta_data`    | array   | Meta data. See [order item meta data properties](#order-item-meta-data-properties)                                    |

### Order fee lines properties ###

|  Attribute   |   Type  |                                           Description                                                                 |
|--------------|---------|-----------------------------------------------------------------------------------------------------------------------|
| `id`         | integer | Item ID. <i class="label label-info">read-only</i>                                                                    |
| `name`       | string  | Fee name. <i class="label label-info">required</i>                                                                    |
| `tax_class`  | string  | Tax class. <i class="label label-info">required if the fee is taxable</i>                                             |
| `tax_status` | string  | Tax status of fee. Set to `taxable` if need apply taxes.                                                              |
| `amount`     | string  | Fee amount.                                                                                                           |
| `total`      | string  | Line total (after discounts).                                                                                         |
| `total_tax`  | string  | Line total tax (after discounts).                                                                                     |
| `taxes`      | array   | Line taxes. See [order item taxes properties](#order-item-taxes-properties) <i class="label label-info">read-only</i> |
| `meta_data`  | array   | Meta data. See [order item meta data properties](#order-item-meta-data-properties)                                    |

### Coupon line properties ###

|   Attribute    |   Type  |                                    Description                                     |
|----------------|---------|------------------------------------------------------------------------------------|
| `id`           | integer | Item ID. <i class="label label-info">read-only</i>                                 |
| `code`         | string  | Coupon code. <i class="label label-info">required</i>                              |
| `discount`     | string  | Discount total. <i class="label label-info">required</i>                           |
| `discount_tax` | string  | Discount total tax. <i class="label label-info">read-only</i>                      |
| `meta_data`    | array   | Meta data. See [order item meta data properties](#order-item-meta-data-properties) |

## Retrieve subscription orders ##

This API lets you retrieve and view related orders for a specific subscription.

### HTTP request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-get">GET</i>
		<h6>/wp-json/wc/v3/subscriptions/&lt;id&gt;/orders</h6>
	</div>
</div>

```shell
curl https://example.com/wp-json/wc/v3/subscriptions/1275/orders \
	-u consumer_key:consumer_secret
```

```javascript
WooCommerce.get('subscriptions/1275/orders', function(err, data, res) {
  console.log(res);
});
```

```php
<?php print_r($woocommerce->get('subscriptions/1275/orders')); ?>
```

```python
print(wcapi.get("subscriptions/1275/orders").json())
```

```ruby
woocommerce.get("subscriptions/1275/orders").parsed_response
```

> JSON response example:

```json
[
    {
        "id": 1274,
        "parent_id": 0,
        "status": "processing",
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
            "first_name": "",
            "last_name": "",
            "company": "",
            "address_1": "",
            "address_2": "",
            "city": "",
            "state": "",
            "postcode": "",
            "country": ""
        },
        "payment_method": "stripe",
        "payment_method_title": "Credit Card (Stripe)",
        "transaction_id": "ch_xxxxxx",
        "customer_ip_address": "192.0.2.1",
        "customer_user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 11_2_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36",
        "created_via": "checkout",
        "customer_note": "",
        "date_completed": null,
        "date_paid": "2021-04-19T17:21:00",
        "cart_hash": "413996ccaa9ff9e1d3375a5f919a6ba3",
        "number": "1274",
        "meta_data": [
            {
                "id": 52020,
                "key": "is_vat_exempt",
                "value": "no"
            },
            {
                "id": 52076,
                "key": "_stripe_customer_id",
                "value": "cus_xxxxxx"
            },
            {
                "id": 52077,
                "key": "_stripe_source_id",
                "value": "src_xxxxxx"
            },
            {
                "id": 52080,
                "key": "_stripe_intent_id",
                "value": "pi_xxxxxx"
            },
            {
                "id": 52081,
                "key": "_stripe_charge_captured",
                "value": "yes"
            },
            {
                "id": 52082,
                "key": "_stripe_fee",
                "value": "1.25"
            },
            {
                "id": 52083,
                "key": "_stripe_net",
                "value": "31.89"
            },
            {
                "id": 52084,
                "key": "_stripe_currency",
                "value": "AUD"
            },
            {
                "id": 52093,
                "key": "_new_order_email_sent",
                "value": "true"
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
        "date_completed_gmt": null,
        "date_paid_gmt": "2021-04-19T07:21:00",
        "order_type": "parent_order",
        "_links": {
            "self": [
                {
                    "href": "https://example.com/wp-json/wc/v3/orders/1274"
                }
            ],
            "collection": [
                {
                    "href": "https://example.com/wp-json/wc/v3/subscriptions"
                }
            ],
            "customer": [
                {
                    "href": "https://example.com/wp-json/wc/v3/customers/1"
                }
            ]
        }
    },
    {
        "id": 1276,
        "parent_id": 0,
        "status": "pending",
        "currency": "USD",
        "version": "5.2.0",
        "prices_include_tax": true,
        "date_created": "2021-04-19T17:22:49",
        "date_modified": "2021-04-19T17:22:49",
        "discount_total": "0.00",
        "discount_tax": "0.00",
        "shipping_total": "0.00",
        "shipping_tax": "0.00",
        "cart_tax": "2.00",
        "total": "22.00",
        "total_tax": "2.00",
        "customer_id": 1,
        "order_key": "wc_order_sUN1l8hwKB83y",
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
            "first_name": "",
            "last_name": "",
            "company": "",
            "address_1": "",
            "address_2": "",
            "city": "",
            "state": "",
            "postcode": "",
            "country": ""
        },
        "payment_method": "stripe",
        "payment_method_title": "Credit Card (Stripe)",
        "transaction_id": "",
        "customer_ip_address": "127.0.0.1",
        "customer_user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 11_2_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36",
        "created_via": "subscription",
        "customer_note": "",
        "date_completed": null,
        "date_paid": null,
        "cart_hash": "",
        "number": "1276",
        "meta_data": [
            {
                "id": 52113,
                "key": "is_vat_exempt",
                "value": "no"
            },
            {
                "id": 52114,
                "key": "_stripe_customer_id",
                "value": "cus_xxxxxx"
            },
            {
                "id": 52115,
                "key": "_stripe_source_id",
                "value": "src_xxxxxx"
            },
            {
                "id": 52125,
                "key": "_subscription_renewal",
                "value": "1275"
            }
        ],
        "line_items": [
            {
                "id": 1609,
                "name": "Weekly",
                "product_id": 1027,
                "variation_id": 0,
                "quantity": 3,
                "tax_class": "",
                "subtotal": "20.00",
                "subtotal_tax": "2.00",
                "total": "20.00",
                "total_tax": "2.00",
                "taxes": [
                    {
                        "id": 2,
                        "total": "2",
                        "subtotal": "2"
                    }
                ],
                "meta_data": [
                    {
                        "id": 12995,
                        "key": "_subtracted_base_location_taxes",
                        "value": {
                            "3": 0.66666680722222238,
                            "4": 1.1000001475833334
                        },
                        "display_key": "_subtracted_base_location_taxes",
                        "display_value": {
                            "3": 0.66666680722222238,
                            "4": 1.1000001475833334
                        }
                    },
                    {
                        "id": 12996,
                        "key": "_subtracted_base_location_rates",
                        "value": {
                            "3": {
                                "rate": 10,
                                "label": "GST",
                                "shipping": "yes",
                                "compound": "yes"
                            },
                            "4": {
                                "rate": 15,
                                "label": "Tax",
                                "shipping": "yes",
                                "compound": "yes"
                            }
                        },
                        "display_key": "_subtracted_base_location_rates",
                        "display_value": {
                            "3": {
                                "rate": 10,
                                "label": "GST",
                                "shipping": "yes",
                                "compound": "yes"
                            },
                            "4": {
                                "rate": 15,
                                "label": "Tax",
                                "shipping": "yes",
                                "compound": "yes"
                            }
                        }
                    }
                ],
                "sku": "",
                "price": 6.666666666666667,
                "parent_name": null
            }
        ],
        "tax_lines": [
            {
                "id": 1610,
                "rate_code": "US-TAX-1",
                "rate_id": 2,
                "label": "TAX",
                "compound": true,
                "tax_total": "2.00",
                "shipping_tax_total": "0.00",
                "rate_percent": 10,
                "meta_data": []
            }
        ],
        "shipping_lines": [],
        "fee_lines": [],
        "coupon_lines": [],
        "date_created_gmt": "2021-04-19T07:22:49",
        "date_modified_gmt": "2021-04-19T07:22:49",
        "date_completed_gmt": null,
        "date_paid_gmt": null,
        "order_type": "renewal_order",
        "_links": {
            "self": [
                {
                    "href": "https://example.com/wp-json/wc/v3/orders/1276"
                }
            ],
            "collection": [
                {
                    "href": "https://example.com/wp-json/wc/v3/subscriptions"
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