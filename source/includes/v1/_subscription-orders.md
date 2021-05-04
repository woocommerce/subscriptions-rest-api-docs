# Subscription Orders #

The subscription orders API endpoints allows you to view orders related to a subscription.

## Subscription Order Properties ##

|       Attribute        |    Type   |                                                                             Description                                                                              |
|------------------------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `id`                   | integer   | Unique identifier for the resource. <i class="label label-info">read-only</i>                                                                                        |
| `parent_id`            | integer   | Parent order ID.                                                                                                                                                     |
| `status`               | string    | Order status. Default is `pending`. Options (plugins may include new status): `pending`, `processing`, `on-hold`, `completed`, `cancelled`, `refunded` and `failed`. |
| `order_key`            | string    | Order key. <i class="label label-info">read-only</i>                                                                                                                 |
| `currency`             | string    | Currency the order was created with, in ISO format, e.g `USD`. Default is the current store currency.                                                                |
| `version`              | string    | Version of WooCommerce when the order was made. <i class="label label-info">read-only</i>                                                                            |
| `prices_include_tax`   | boolean   | Shows if the prices included tax during checkout. <i class="label label-info">read-only</i>                                                                          |
| `date_created`         | date-time | The date the order was created, in the site's timezone. <i class="label label-info">read-only</i>                                                                    |
| `date_modified`        | date-time | The date the order was last modified, in the site's timezone. <i class="label label-info">read-only</i>                                                              |
| `customer_id`          | integer   | User ID who owns the order. Use `0` for guests. Default is `0`.                                                                                                      |
| `discount_total`       | string    | Total discount amount for the order. <i class="label label-info">read-only</i>                                                                                       |
| `discount_tax`         | string    | Total discount tax amount for the order. <i class="label label-info">read-only</i>                                                                                   |
| `shipping_total`       | string    | Total shipping amount for the order. <i class="label label-info">read-only</i>                                                                                       |
| `shipping_tax`         | string    | Total shipping tax amount for the order. <i class="label label-info">read-only</i>                                                                                   |
| `cart_tax`             | string    | Sum of line item taxes only. <i class="label label-info">read-only</i>                                                                                               |
| `total`                | string    | Grand total. <i class="label label-info">read-only</i>                                                                                                               |
| `total_tax`            | string    | Sum of all taxes. <i class="label label-info">read-only</i>                                                                                                          |
| `billing`              | array     | Billing address. See [Customer Billing Address properties](#billing-address-properties).                                                                             |
| `shipping`             | array     | Shipping address. See [Customer Shipping Address properties](#shipping-address-properties).                                                                          |
| `payment_method`       | string    | Payment method ID.                                                                                                                                                   |
| `payment_method_title` | string    | Payment method title.                                                                                                                                                |
| `set_paid`             | boolean   | Define if the order is paid. It will set the status to processing and reduce stock items. Default is `false`. <i class="label label-info">write-only</i>             |
| `transaction_id`       | string    | Unique transaction ID. In write-mode only is available if `set_paid` is `true`.                                                                                      |
| `customer_ip_address`  | string    | Customer's IP address. <i class="label label-info">read-only</i>                                                                                                     |
| `customer_user_agent`  | string    | User agent of the customer. <i class="label label-info">read-only</i>                                                                                                |
| `created_via`          | string    | Shows where the order was created. <i class="label label-info">read-only</i>                                                                                         |
| `customer_note`        | string    | Note left by customer during checkout.                                                                                                                               |
| `date_completed`       | date-time | The date the order was completed, in the site's timezone. <i class="label label-info">read-only</i>                                                                  |
| `date_paid`            | date-time | The date the order has been paid, in the site's timezone. <i class="label label-info">read-only</i>                                                                  |
| `cart_hash`            | string    | MD5 hash of cart items to ensure orders are not modified. <i class="label label-info">read-only</i>                                                                  |
| `line_items`           | array     | Line items data. See [Line Items properties](#line-item-properties).                                                                                                |
| `tax_lines`            | array     | Tax lines data. See [Tax Lines properties](#tax-line-properties). <i class="label label-info">read-only</i>                                                         |
| `shipping_lines`       | array     | Shipping lines data. See [Shipping Lines properties](#shipping-line-properties).                                                                                    |
| `fee_lines`            | array     | Fee lines data. See [Fee Lines Properites](#fee-line-properties).                                                                                                   |
| `coupon_lines`         | array     | Coupons line data. See [Coupon Lines properties](#coupon-line-properties).                                                                                          |

### Line item properties ###

|   Attribute    |   Type  |                                          Description                                           |
|----------------|---------|------------------------------------------------------------------------------------------------|
| `id`           | integer | Item ID. <i class="label label-info">read-only</i>                                             |
| `name`         | string  | Product name. <i class="label label-info">read-only</i>                                        |
| `sku`          | string  | Product SKU. <i class="label label-info">read-only</i>                                         |
| `product_id`   | integer | Product ID.                                                                                    |
| `variation_id` | integer | Variation ID, if applicable.                                                                   |
| `quantity`     | integer | Quantity ordered.                                                                              |
| `tax_class`    | string  | Tax class of product. <i class="label label-info">read-only</i>                                |
| `price`        | string  | Product price. <i class="label label-info">read-only</i>                                       |
| `subtotal`     | string  | Line subtotal (before discounts).                                                              |
| `subtotal_tax` | string  | Line subtotal tax (before discounts).                                                          |
| `total`        | string  | Line total (after discounts).                                                                  |
| `total_tax`    | string  | Line total tax (after discounts).                                                              |
| `taxes`        | array   | Line taxes with `id`, `total` and `subtotal`. <i class="label label-info">read-only</i>    |
| `meta`         | array   | Line item meta data with `key`, `label` and `value`. <i class="label label-info">read-only</i> |

### Tax line properties ###

|      Attribute       |   Type  |                                                             Description                                                             |
|----------------------|---------|-------------------------------------------------------------------------------------------------------------------------------------|
| `id`                 | integer | Item ID. <i class="label label-info">read-only</i>                                                                                  |
| `rate_code`          | string  | Tax rate code. <i class="label label-info">read-only</i>                                                                            |
| `rate_id`            | string  | Tax rate ID. <i class="label label-info">read-only</i>                                                                              |
| `label`              | string  | Tax rate label. <i class="label label-info">read-only</i>                                                                           |
| `compound`           | boolean | Show if is a compound tax rate. Compound tax rates are applied on top of other tax rates. <i class="label label-info">read-only</i> |
| `tax_total`          | string  | Tax total (not including shipping taxes). <i class="label label-info">read-only</i>                                                 |
| `shipping_tax_total` | string  | Shipping tax total. <i class="label label-info">read-only</i>                                                                       |

### Shipping line properties ###

|   Attribute    |   Type  |                                 Description                                 |
|----------------|---------|-----------------------------------------------------------------------------|
| `id`           | integer | Item ID. <i class="label label-info">read-only</i>                          |
| `method_title` | string  | Shipping method name.                                                       |
| `method_id`    | string  | Shipping method ID. <i class="label label-info">required</i>                |
| `total`        | string  | Line total (after discounts).                                               |
| `total_tax`    | string  | Line total tax (after discounts). <i class="label label-info">read-only</i> |
| `taxes`        | array   | Line taxes with `id` and `total`. <i class="label label-info">read-only</i> |

### Fee line properties ###

|  Attribute   |   Type  |                                       Description                                       |
|--------------|---------|-----------------------------------------------------------------------------------------|
| `id`         | integer | Item ID. <i class="label label-info">read-only</i>                                      |
| `name`       | string  | Fee name. <i class="label label-info">required</i>                                      |
| `tax_class`  | string  | Tax class. <i class="label label-info">required if the fee is taxable</i>               |
| `tax_status` | string  | Tax status of fee. Set to `taxable` if need apply taxes.                                |
| `total`      | string  | Line total (after discounts).                                                           |
| `total_tax`  | string  | Line total tax (after discounts).                                                       |
| `taxes`      | array   | Line taxes with `id`, `total` and `subtotal`. <i class="label label-info">read-only</i> |

### Coupon line properties ###

|   Attribute    |   Type  |                          Description                          |
|----------------|---------|---------------------------------------------------------------|
| `id`           | integer | Item ID. <i class="label label-info">read-only</i>            |
| `code`         | string  | Coupon code. <i class="label label-info">required</i>         |
| `discount`     | string  | Discount total. <i class="label label-info">required</i>      |
| `discount_tax` | string  | Discount total tax. <i class="label label-info">read-only</i> |

## Retrieve Subscription Orders ##

This API lets you retrieve and view related orders for a specific subscription.

### HTTP request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-get">GET</i>
		<h6>/wp-json/wc/v1/subscriptions/&lt;id&gt;/orders</h6>
	</div>
</div>

```shell
curl https://example.com/wp-json/wc/v1/subscriptions/154/orders \
	-u consumer_key:consumer_secret
```

```javascript
WooCommerce.get('subscriptions/154/orders', function(err, data, res) {
  console.log(res);
});
```

```php
<?php print_r($woocommerce->get('subscriptions/154/orders')); ?>
```

```python
print(wcapi.get("subscriptions/154/orders").json())
```

```ruby
woocommerce.get("subscriptions/154/orders").parsed_response
```

> JSON response example:

```json
[
  {
    "_links": {
      "collection": [
        {
            "href": "https://vagrant.local/wp-json/wc/v1/orders"
        }
      ], 
      "customer": [
        {
            "href": "https://vagrant.local/wp-json/wc/v1/customers/1"
        }
      ], 
      "self": [
        {
            "href": "https://vagrant.local/wp-json/wc/v1/orders/318"
        }
      ]
    }, 
    "billing": {
      "address_1": "969 Market", 
      "address_2": "", 
      "city": "San Francisco", 
      "company": "", 
      "country": "US", 
      "email": "john.doe@example.com", 
      "first_name": "John", 
      "last_name": "Doe", 
      "phone": "(555) 555-5555", 
      "postcode": "94103", 
      "state": "CA"
    }, 
    "cart_hash": "837192a02bc12d1ac767df9be65464c1", 
    "cart_tax": "4.55", 
    "coupon_lines": [], 
    "created_via": "checkout", 
    "currency": "AUD", 
    "customer_id": 1, 
    "customer_ip_address": "172.28.128.1", 
    "customer_note": "", 
    "customer_user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.84 Safari/537.36", 
    "date_completed": "2016-06-16T06:23:24", 
    "date_created": "2016-06-16T06:23:24", 
    "date_modified": "2016-06-16T06:23:24", 
    "date_paid": "", 
    "discount_tax": "0.00", 
    "discount_total": "0.00", 
    "fee_lines": [], 
    "id": 318, 
    "line_items": [
      {
        "id": 56, 
        "meta": [], 
        "name": "Simple subscription", 
        "price": "45.45", 
        "product_id": 28, 
        "quantity": 1, 
        "sku": "", 
        "subtotal": "45.45", 
        "subtotal_tax": "4.55", 
        "tax_class": "", 
        "taxes": [
          {
            "id": 1, 
            "subtotal": "4.5455", 
            "total": "4.5455"
          }, 
          {
            "id": 2, 
            "subtotal": "", 
            "total": ""
          }
        ], 
        "total": "45.45", 
        "total_tax": "4.55", 
        "variation_id": 0
      }
    ], 
    "order_key": "wc_order_576245dc19ddb", 
    "order_type": "renewal_order", 
    "parent_id": 0, 
    "payment_method": "stripe", 
    "payment_method_title": "Credit card (Stripe)", 
    "prices_include_tax": true, 
    "refunds": [], 
    "shipping": {
      "address_1": "969 Market", 
      "address_2": "", 
      "city": "San Francisco", 
      "company": "", 
      "country": "US", 
      "first_name": "John", 
      "last_name": "Doe", 
      "postcode": "94103", 
      "state": "CA"
    }, 
    "shipping_lines": [
      {
        "id": 57, 
        "method_id": "flat_rate:1", 
        "method_title": "Flat Rate", 
        "taxes": [
          {
            "id": 1, 
            "total": ""
          }, 
          {
            "id": 2, 
            "total": "7.5"
          }
        ], 
        "total": "15.00", 
        "total_tax": "7.50"
      }
    ], 
    "shipping_tax": "7.50", 
    "shipping_total": "15.00", 
    "status": "pending", 
    "tax_lines": [
      {
        "compound": false, 
        "id": 58, 
        "label": "GST", 
        "rate_code": "GST-1", 
        "rate_id": "1", 
        "shipping_tax_total": "0.00", 
        "tax_total": "4.55"
      }, 
      {
        "compound": false, 
        "id": 59, 
        "label": "Ship", 
        "rate_code": "SHIP-1", 
        "rate_id": "2", 
        "shipping_tax_total": "7.50", 
        "tax_total": "0.00"
      }
    ], 
    "total": "72.50", 
    "total_tax": "12.05", 
    "transaction_id": "", 
    "version": "2.6.0"
  }, 
  {
    "_links": {
      "collection": [
        {
          "href": "https://vagrant.local/wp-json/wc/v1/orders"
        }
      ], 
      "customer": [
        {
          "href": "https://vagrant.local/wp-json/wc/v1/customers/1"
        }
      ], 
      "self": [
        {
          "href": "https://vagrant.local/wp-json/wc/v1/orders/315"
        }
      ]
    }, 
    "billing": {
      "address_1": "969 Market", 
      "address_2": "", 
      "city": "San Francisco", 
      "company": "", 
      "country": "US", 
      "email": "john.doe@example.com", 
      "first_name": "John", 
      "last_name": "Doe", 
      "phone": "(555) 555-5555", 
      "postcode": "94103", 
      "state": "CA"
    }, 
    "cart_hash": "837192a02bc12d1ac767df9be65464c1", 
    "cart_tax": "4.55", 
    "coupon_lines": [], 
    "created_via": "checkout", 
    "currency": "AUD", 
    "customer_id": 1, 
    "customer_ip_address": "172.28.128.1", 
    "customer_note": "", 
    "customer_user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.84 Safari/537.36", 
    "date_completed": "2016-06-16T06:22:59", 
    "date_created": "2016-06-16T06:22:59", 
    "date_modified": "2016-06-16T06:22:59", 
    "date_paid": "2016-06-16 06:23:00", 
    "discount_tax": "0.00", 
    "discount_total": "0.00", 
    "fee_lines": [], 
    "id": 315, 
    "line_items": [
      {
        "id": 48, 
        "meta": [], 
        "name": "Simple subscription", 
        "price": "45.45", 
        "product_id": 28, 
        "quantity": 1, 
        "sku": "", 
        "subtotal": "45.45", 
        "subtotal_tax": "4.55", 
        "tax_class": "", 
        "taxes": [
          {
            "id": 1, 
            "subtotal": "4.5455", 
            "total": "4.5455"
          }
        ], 
        "total": "45.45", 
        "total_tax": "4.55", 
        "variation_id": 0
      }
    ], 
    "order_key": "wc_order_576245c24c91f", 
    "order_type": "parent_order", 
    "parent_id": 0, 
    "payment_method": "stripe", 
    "payment_method_title": "Credit card (Stripe)", 
    "prices_include_tax": true, 
    "refunds": [], 
    "shipping": {
      "address_1": "969 Market", 
      "address_2": "", 
      "city": "San Francisco", 
      "company": "", 
      "country": "US", 
      "first_name": "John", 
      "last_name": "Doe", 
      "postcode": "94103", 
      "state": "CA"
    }, 
    "shipping_lines": [
      {
        "id": 49, 
        "method_id": "flat_rate:1", 
        "method_title": "Flat Rate", 
        "taxes": [
          {
            "id": 2, 
            "total": "7.5"
          }
        ], 
        "total": "15.00", 
        "total_tax": "7.50"
      }
    ], 
    "shipping_tax": "7.50", 
    "shipping_total": "15.00", 
    "status": "processing", 
    "tax_lines": [
      {
        "compound": false, 
        "id": 50, 
        "label": "GST", 
        "rate_code": "GST-1", 
        "rate_id": "1", 
        "shipping_tax_total": "0.00", 
        "tax_total": "4.55"
      }, 
      {
        "compound": false, 
        "id": 51, 
        "label": "Ship", 
        "rate_code": "SHIP-1", 
        "rate_id": "2", 
        "shipping_tax_total": "7.50", 
        "tax_total": "0.00"
      }
    ], 
    "total": "72.50", 
    "total_tax": "12.05", 
    "transaction_id": "ch_18Mtu34gR1k0Sv2pht1HmNKu", 
    "version": "2.6.0"
  }
]
```