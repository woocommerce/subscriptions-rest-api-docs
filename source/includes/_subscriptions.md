# Subscriptions #

The Subscriptions API allows you to create, view, update, and delete individual, or a batch, of subscriptions.

## Subscription Properties ##

|       Attribute        |    Type   |                                                                             Description                                                                              |
|------------------------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `id`                   | integer   | Unique identifier for the resource. <i class="label label-info">read-only</i>                                                                                        |
| `parent_id`            | integer   | Parent/initial order ID for the subscription.                                                                                                                        |
| `status`               | string    | Subscription status. Default is `pending`. Options (plugins may include new status): `pending`, `active`, `on-hold`, `expired`, `cancelled` and `pending-cancel`.    |
| `billing_period`       | string    | Billing period for the subscription. Options: `day`, `week`, `month`and `year`.                                                                                      |
| `billing_interval`     | integer   | The number of billing periods between subscription renewals.                                                                                                         |
| `start_date`           | date-time | The subscriptions start date in UTC. Defaults to the current time. Must be the format `YYYY-mm-dd H:i:s`.                                                            |
| `trial_end_date`       | date-time | The subscriptions trial end date in UTC. Must be the format `YYYY-mm-dd H:i:s`.                                                                                      |
| `next_payment_date`    | date-time | The subscriptions next payment date in UTC. Must be the format `YYYY-mm-dd H:i:s`.                                                                                   |
| `end_date`             | date-time | The subscriptions end date in UTC. Must be the format `YYYY-mm-dd H:i:s`.                                                                                            |
| `order_key`            | string    | Order key. <i class="label label-info">read-only</i>                                                                                                                 |
| `currency`             | string    | Currency the order was created with, in ISO format, e.g `USD`. Default is the current store currency.                                                                |
| `version`              | string    | Version of WooCommerce when the order was made. <i class="label label-info">read-only</i>                                                                            |
| `prices_include_tax`   | boolean   | Shows if the prices included tax during checkout. <i class="label label-info">read-only</i>                                                                          |
| `date_created`         | date-time | The date the order was created, in the site's timezone. <i class="label label-info">read-only</i>                                                                    |
| `date_modified`        | date-time | The date the order was last modified, in the site's timezone. <i class="label label-info">read-only</i>                                                              |
| `customer_id`          | integer   | User ID who owns the order.                                                                                                                                          |
| `discount_total`       | string    | Total discount amount for the order. <i class="label label-info">read-only</i>                                                                                       |
| `discount_tax`         | string    | Total discount tax amount for the order. <i class="label label-info">read-only</i>                                                                                   |
| `shipping_total`       | string    | Total shipping amount for the order. <i class="label label-info">read-only</i>                                                                                       |
| `shipping_tax`         | string    | Total shipping tax amount for the order. <i class="label label-info">read-only</i>                                                                                   |
| `cart_tax`             | string    | Sum of line item taxes only. <i class="label label-info">read-only</i>                                                                                               |
| `total`                | string    | Grand total. <i class="label label-info">read-only</i>                                                                                                               |
| `total_tax`            | string    | Sum of all taxes. <i class="label label-info">read-only</i>                                                                                                          |
| `order_total`          | string    | Subscription renewing total. This value can be used to override the value calculated by `$subscription->calculate_totals()`.                                         |
| `billing`              | array     | Billing address. See [Customer Billing Address properties](#billing-address-properties).                                                                             |
| `shipping`             | array     | Shipping address. See [Customer Shipping Address properties](#shipping-address-properties).                                                                          |
| `payment_method`       | string    | Payment method ID.                                                                                                                                                   |
| `payment_method_title` | string    | Payment method title.                                                                                                                                                |
| `payment_details`      | array     | Payment method data. See [Payment Method properties](#payment-method-properties). <i class="label label-info">edit-only</i>                                                                                                                                                 |
| `set_paid`             | boolean   | Define if the order is paid. It will set the status to processing and reduce stock items. Default is `false`. <i class="label label-info">write-only</i>             |
| `transaction_id`       | string    | Unique transaction ID. In write-mode only is available if `set_paid` is `true`.                                                                                      |
| `customer_ip_address`  | string    | Customer's IP address. <i class="label label-info">read-only</i>                                                                                                     |
| `customer_user_agent`  | string    | User agent of the customer. <i class="label label-info">read-only</i>                                                                                                |
| `created_via`          | string    | Shows where the order was created. <i class="label label-info">read-only</i>                                                                                         |
| `customer_note`        | string    | Note left by customer during checkout.                                                                                                                               |
| `date_completed`       | date-time | The date the order was completed, in the site's timezone. <i class="label label-info">read-only</i>                                                                  |
| `date_paid`            | date-time | The date the order has been paid, in the site's timezone. <i class="label label-info">read-only</i>                                                                  |
| `cart_hash`            | string    | MD5 hash of cart items to ensure orders are not modified. <i class="label label-info">read-only</i>                                                                  |
| `line_items`           | array     | Line items data. See [Line Items properties](#line-item-properties).                                                                                                 |
| `tax_lines`            | array     | Tax lines data. See [Tax Lines properties](#tax-line-properties). <i class="label label-info">read-only</i>                                                          |
| `shipping_lines`       | array     | Shipping lines data. See [Shipping Lines properties](#shipping-line-properties).                                                                                     |
| `fee_lines`            | array     | Fee lines data. See [Fee Lines Properties](#fee-line-properties).                                                                                                    |
| `coupon_lines`         | array     | Coupons line data. See [Coupon Lines properties](#coupon-line-properties).                                                                                           |

### Payment method properties ###

|  Attribute  | Type  |                                          Description                                           |
|-------------|-------|------------------------------------------------------------------------------------------------|
| `post_meta` | array | Payment meta stored as post meta on the subscription `array( '_meta_key' => 'meta_value' )`    |
| `user_meta` | array | Payment meta stored as user meta on the customer `array( '_meta_key' => 'meta_value' )`        |

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

## Create a Subscription ##

This API helps you to create a new subscription.

### HTTP request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-post">POST</i>
		<h6>/wp-json/wc/v1/subscriptions</h6>
	</div>
</div>

> Example of creating an active stripe subscription:

```shell
curl -X POST https://example.com/wp-json/wc/v1/subscriptions \
  -u consumer_key:consumer_secret \
  -H "Content-Type: application/json" \
  -d '{
  "customer_id": 1,
  "status": "active",
  "billing_period": "month",
  "billing_interval": 1,
  "start_date": "2016-04-04 10:45:00",
  "next_payment_date":"2017-01-01 10:45:00",
  "payment_method": "stripe",
  "payment_details":{
    "post_meta": {
      "_stripe_customer_id":"cus_484hfj3m4fm3",
      "_stripe_source_id":"src_5n4fndsn0"
    }
  },
  "billing": {
    "first_name": "John",
    "last_name": "Doe",
    "address_1": "969 Market",
    "address_2": "",
    "city": "San Francisco",
    "state": "CA",
    "postcode": "94103",
    "country": "US",
    "email": "john.doe@example.com",
    "phone": "(555) 555-5555"
  },
  "shipping": {
    "first_name": "John",
    "last_name": "Doe",
    "address_1": "969 Market",
    "address_2": "",
    "city": "San Francisco",
    "state": "CA",
    "postcode": "94103",
    "country": "US"
  },
  "line_items": [
    {
      "product_id": 93,
      "quantity": 2
    },
    {
      "product_id": 22,
      "variation_id": 23,
      "quantity": 1
    }
  ],
  "shipping_lines": [
    {
      "method_id": "flat_rate",
      "method_title": "Flat Rate",
      "total": 10
    }
  ]
}'
```

```javascript
var data = {
  customer_id: 1,
  status: 'active',
  billing_period: 'month',
  billing_interval: 1,
  start_date: '2016-04-04 10:45:00',
  next_payment_date: '2017-01-01 10:45:00',
  payment_method: 'stripe',
  payment_details: {
    post_meta: {
      _stripe_customer_id: 'cus_484hfj3m4fm3',
      _stripe_source_id: 'scr_5n4fndsn0'
    }
  },
  billing: {
    first_name: 'John',
    last_name: 'Doe',
    address_1: '969 Market',
    address_2: '',
    city: 'San Francisco',
    state: 'CA',
    postcode: '94103',
    country: 'US',
    email: 'john.doe@example.com',
    phone: '(555) 555-5555'
  },
  shipping: {
    first_name: 'John',
    last_name: 'Doe',
    address_1: '969 Market',
    address_2: '',
    city: 'San Francisco',
    state: 'CA',
    postcode: '94103',
    country: 'US'
  },
  line_items: [
    {
      product_id: 93,
      quantity: 2
    },
    {
      product_id: 22,
      variation_id: 23,
      quantity: 1
    }
  ],
  shipping_lines: [
    {
      method_id: 'flat_rate',
      method_title: 'Flat Rate',
      total: 10
    }
  ]
};

WooCommerce.post('subscriptions', data, function(err, data, res) {
  console.log(res);
});
```

```php
<?php
$data = [
    'customer_id' => 1
    'status' => 'active',
    'billing_period' => 'month',
    'billing_interval' => 1,
    'start_date' => '2016-04-04 10:45:00',
    'next_payment_date' => '2017-01-01 10:45:00',
    'payment_method' => 'stripe',
    'payment_details' => [
      'post_meta' => [
        "_stripe_customer_id" => "cus_484hfj3m4fm3",
        "_stripe_source_id" => "src_5n4fndsn0"
      ]
    ],
    'billing' => [
        'first_name' => 'John',
        'last_name' => 'Doe',
        'address_1' => '969 Market',
        'address_2' => '',
        'city' => 'San Francisco',
        'state' => 'CA',
        'postcode' => '94103',
        'country' => 'US',
        'email' => 'john.doe@example.com',
        'phone' => '(555) 555-5555'
    ],
    'shipping' => [
        'first_name' => 'John',
        'last_name' => 'Doe',
        'address_1' => '969 Market',
        'address_2' => '',
        'city' => 'San Francisco',
        'state' => 'CA',
        'postcode' => '94103',
        'country' => 'US'
    ],
    'line_items' => [
        [
            'product_id' => 93,
            'quantity' => 2
        ],
        [
            'product_id' => 22,
            'variation_id' => 23,
            'quantity' => 1
        ]
    ],
    'shipping_lines' => [
        [
            'method_id' => 'flat_rate',
            'method_title' => 'Flat Rate',
            'total' => 10
        ]
    ]
];

print_r($woocommerce->post('subscriptions', $data));
?>
```

```python
data = {
    "customer_id": 1,
    "status": "active",
    "billing_period": "month",
    "billing_interval": 1,
    "start_date": "2016-04-04 10:45:00",
    "next_payment_date":"2017-01-01 10:45:00",
    "payment_method": "stripe",
    "payment_details":{
      "post_meta": {
        "_stripe_customer_id":"cus_484hfj3m4fm3",
        "_stripe_source_id":"src_5n4fndsn0"
      }
    },
    "billing": {
        "first_name": "John",
        "last_name": "Doe",
        "address_1": "969 Market",
        "address_2": "",
        "city": "San Francisco",
        "state": "CA",
        "postcode": "94103",
        "country": "US",
        "email": "john.doe@example.com",
        "phone": "(555) 555-5555"
    },
    "shipping": {
        "first_name": "John",
        "last_name": "Doe",
        "address_1": "969 Market",
        "address_2": "",
        "city": "San Francisco",
        "state": "CA",
        "postcode": "94103",
        "country": "US"
    },
    "line_items": [
        {
            "product_id": 93,
            "quantity": 2
        },
        {
            "product_id": 22,
            "variation_id": 23,
            "quantity": 1
        }
    ],
    "shipping_lines": [
        {
            "method_id": "flat_rate",
            "method_title": "Flat Rate",
            "total": 10
        }
    ]
}

print(wcapi.post("subscriptions", data).json())
```

```ruby
data = {
  customer_id: 1,
  status: "active",
  billing_period: "month",
  billing_interval: 1,
  start_date: "2016-04-04 10:45:00",
  next_payment_date:"2017-01-01 10:45:00",
  payment_method: "stripe",
  payment_details: {
    post_meta: {
      _stripe_customer_id:"cus_484hfj3m4fm3",
      _stripe_source_id:"src_5n4fndsn0"
    }
  },
  billing: {
    first_name: "John",
    last_name: "Doe",
    address_1: "969 Market",
    address_2: "",
    city: "San Francisco",
    state: "CA",
    postcode: "94103",
    country: "US",
    email: "john.doe@example.com",
    phone: "(555) 555-5555"
  },
  shipping: {
    first_name: "John",
    last_name: "Doe",
    address_1: "969 Market",
    address_2: "",
    city: "San Francisco",
    state: "CA",
    postcode: "94103",
    country: "US"
  },
  line_items: [
    {
      product_id: 93,
      quantity: 2
    },
    {
      product_id: 22,
      variation_id: 23,
      quantity: 1
    }
  ],
  shipping_lines: [
    {
      method_id: "flat_rate",
      method_title: "Flat Rate",
      total: 10
    }
  ]
}

woocommerce.post("subscriptions", data).parsed_response
```

> JSON response example:

```json
{
  "id": 311,
  "parent_id": 0,
  "status": "active",
  "order_key": "wc_order_575fd4665d2cc",
  "currency": "AUD",
  "version": "2.6.0",
  "prices_include_tax": true,
  "date_created": "2016-06-14T09:54:46",
  "date_modified": "2016-06-14T09:54:46",
  "customer_id": 1,
  "discount_total": "0.00",
  "discount_tax": "0.00",
  "shipping_total": "0.00",
  "shipping_tax": "0.00",
  "cart_tax": "0.00",
  "total": "17.99",
  "total_tax": "0.00",
  "billing": {
    "first_name": "John",
    "last_name": "Doe",
    "company": "",
    "address_1": "969 Market",
    "address_2": "",
    "city": "San Francisco",
    "state": "CA",
    "postcode": "94103",
    "country": "US",
    "email": "john.doe@example.com",
    "phone": "(555) 555-5555"
  },
  "shipping": {
    "first_name": "John",
    "last_name": "Doe",
    "company": "",
    "address_1": "969 Market",
    "address_2": "",
    "city": "San Francisco",
    "state": "CA",
    "postcode": "94103",
    "country": "US"
  },
  "payment_method": "stripe",
  "payment_method_title": "Credit card (Stripe)",
  "transaction_id": "",
  "customer_ip_address": "",
  "customer_user_agent": "",
  "created_via": "rest-api",
  "customer_note": "",
  "date_completed": "2016-06-14T09:54:46",
  "date_paid": "",
  "cart_hash": "",
  "line_items": [
    {
      "id": 18,
      "name": "Woo Single #1",
      "sku": "",
      "product_id": 93,
      "variation_id": 0,
      "quantity": 2,
      "tax_class": "",
      "price": "3.00",
      "subtotal": "6.00",
      "subtotal_tax": "0.45",
      "total": "6.00",
      "total_tax": "0.45",
      "taxes": [
        {
          "id": 75,
          "total": 0.45,
          "subtotal": 0.45
        }
      ],
      "meta": []
    },
    {
      "id": 19,
      "name": "Ship Your Idea",
      "sku": "",
      "product_id": 22,
      "variation_id": 23,
      "quantity": 1,
      "tax_class": "",
      "price": "20.00",
      "subtotal": "20.00",
      "subtotal_tax": "1.50",
      "total": "20.00",
      "total_tax": "1.50",
      "taxes": [
        {
          "id": 75,
          "total": 1.5,
          "subtotal": 1.5
        }
      ],
      "meta": [
        {
          "key": "pa_color",
          "label": "Color",
          "value": "Black"
        }
      ]
    }
  ],
  "tax_lines":[],
  "shipping_lines":[],
  "fee_lines":[],
  "coupon_lines":[],
  "refunds":[],
  "billing_period": "month",
  "billing_interval": "2",
  "start_date": "2016-06-14T09:54:46",
  "trial_end_date": "",
  "next_payment_date": "2017-05-05T08:08:08",
  "end_date": ""
  "_links": {
    "self": [
      {
        "href": "https://vagrant.local/wp-json/wc/v1/subscriptions/311"
      }
    ],
    "collection": [
      {
        "href": "https://vagrant.local/wp-json/wc/v1/subscriptions"
      }
    ],
    "customer": [
      {
        "href": "https://vagrant.local/wp-json/wc/v1/customers/1"
      }
    ]
  }
}
```

## Retrieve a Subscription ##

This API lets you retrieve and view a specific subscription.

### HTTP request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-get">GET</i>
		<h6>/wp-json/wc/v1/subscriptions/&lt;id&gt;</h6>
	</div>
</div>

```shell
curl https://example.com/wp-json/wc/v1/subscriptions/251 \
	-u consumer_key:consumer_secret
```

```javascript
WooCommerce.get('subscriptions/251', function(err, data, res) {
  console.log(res);
});
```

```php
<?php print_r($woocommerce->get('subscriptions/251')); ?>
```

```python
print(wcapi.get("subscriptions/251").json())
```

```ruby
woocommerce.get("subscriptions/251").parsed_response
```

> JSON response example:

```json
{  
  "id":251,
  "parent_id":250,
  "status":"trash",
  "order_key":"wc_order_57305d2c7e948",
  "currency":"AUD",
  "version":"2.6.0",
  "prices_include_tax":true,
  "date_created":"2016-05-09T09:49:32",
  "date_modified":"2016-06-07T05:27:28",
  "customer_id":1,
  "discount_total":"0.00",
  "discount_tax":"0.00",
  "shipping_total":"15.00",
  "shipping_tax":"7.50",
  "cart_tax":"4.55",
  "total":"72.50",
  "total_tax":"12.05",
  "billing":{  
    "first_name":"Matt",
    "last_name":"Allan",
    "company":"",
    "address_1":"123 Fake Street",
    "address_2":"",
    "city":"Brisbane",
    "state":"QLD",
    "postcode":"4101",
    "country":"AU",
    "email":"matt@prospress.com",
    "phone":"55555555"
  },
  "shipping":{  
    "first_name":"Matt",
    "last_name":"Allan",
    "company":"",
    "address_1":"123 Fake Street",
    "address_2":"",
    "city":"Brisbane",
    "state":"QLD",
    "postcode":"4101",
    "country":"AU"
  },
  "payment_method":"",
  "payment_method_title":"",
  "transaction_id":"",
  "customer_ip_address":"172.28.128.1",
  "customer_user_agent":"Mozilla\/5.0 (Macintosh; Intel Mac OS X 10_11_4) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/50.0.2661.86 Safari\/537.36",
  "created_via":"checkout",
  "customer_note":"true",
  "date_completed":"2016-06-07T05:27:28",
  "date_paid":"",
  "cart_hash":"922a1c36fd92a2259a0c1621cf13fdf8",
  "line_items":[  
    {  
      "id":28,
      "name":"Simple subscription",
      "sku":"",
      "product_id":28,
      "variation_id":0,
      "quantity":1,
      "tax_class":"",
      "price":"45.45",
      "subtotal":"45.45",
      "subtotal_tax":"4.55",
      "total":"45.45",
      "total_tax":"4.55",
      "taxes":[  
        {  
          "id":1,
          "total":"4.5455",
          "subtotal":"4.5455"
        },
        {  
          "id":2,
          "total":"",
          "subtotal":""
        }
      ],
      "meta":[  

      ]
    }
  ],
  "tax_lines":[  
    {  
      "id":30,
      "rate_code":"GST-1",
      "rate_id":"1",
      "label":"GST",
      "compound":false,
      "tax_total":"4.55",
      "shipping_tax_total":"0.00"
    },
    {  
      "id":31,
      "rate_code":"SHIP-1",
      "rate_id":"2",
      "label":"Ship",
      "compound":false,
      "tax_total":"0.00",
      "shipping_tax_total":"7.50"
    }
  ],
  "shipping_lines":[  
    {  
      "id":29,
      "method_title":"Flat Rate",
      "method_id":"flat_rate:1",
      "total":"15.00",
      "total_tax":"7.50",
      "taxes":[  
        {  
          "id":1,
          "total":""
        },
        {  
          "id":2,
          "total":"7.5"
        }
      ]
    }
  ],
  "fee_lines":[  

  ],
  "coupon_lines":[  

  ],
  "refunds":[  

  ],
  "billing_period":"month",
  "billing_interval":"1",
  "start_date":"2016-05-09T09:49:32",
  "trial_end_date":"",
  "next_payment_date":"",
  "end_date":"2016-06-07T04:15:23"
  "_links":{  
    "self":[  
      {  
        "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/subscriptions\/251"
      }
    ],
    "collection":[  
      {  
        "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/subscriptions"
      }
    ],
    "customer":[  
      {  
        "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/customers\/1"
      }
    ],
    "up":[  
      {  
        "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/orders\/250"
      }
    ]
  }
}
```

#### Available parameters ####

| Parameter |  Type  |                    Description                    |
|-----------|--------|---------------------------------------------------|
| `dp`      | string | Number of decimal points to use in each resource. |

## List all Subscriptions ##

This API helps you to view all the subscriptions.

### HTTP request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-get">GET</i>
		<h6>/wp-json/wc/v1/subscriptions</h6>
	</div>
</div>

```shell
curl https://example.com/wp-json/wc/v1/subscriptions \
	-u consumer_key:consumer_secret
```

```javascript
WooCommerce.get('subscriptions', function(err, data, res) {
  console.log(res);
});
```

```php
<?php print_r($woocommerce->get('subscriptions')); ?>
```

```python
print(wcapi.get("subscriptions").json())
```

```ruby
woocommerce.get("subscriptions").parsed_response
```

> JSON response example:

```json
[  
  {  
    "id":316,
    "parent_id":315,
    "status":"on-hold",
    "order_key":"wc_order_576245c257a1f",
    "currency":"AUD",
    "version":"2.6.0",
    "prices_include_tax":true,
    "date_created":"2016-06-16T06:22:58",
    "date_modified":"2016-06-16T06:23:23",
    "customer_id":1,
    "discount_total":"0.00",
    "discount_tax":"0.00",
    "shipping_total":"15.00",
    "shipping_tax":"7.50",
    "cart_tax":"4.55",
    "total":"72.50",
    "total_tax":"12.05",
    "billing":{  
      "first_name":"John",
      "last_name":"Doe",
      "company":"",
      "address_1":"969 Market",
      "address_2":"",
      "city":"San Francisco",
      "state":"CA",
      "postcode":"94103",
      "country":"US",
      "email":"john.doe@example.com",
      "phone":"(555) 555-5555"
    },
    "shipping":{  
      "first_name":"John",
      "last_name":"Doe",
      "company":"",
      "address_1":"969 Market",
      "address_2":"",
      "city":"San Francisco",
      "state":"CA",
      "postcode":"94103",
      "country":"US"
    },
    "payment_method":"stripe",
    "payment_method_title":"Credit card (Stripe)",
    "transaction_id":"",
    "customer_ip_address":"172.28.128.1",
    "customer_user_agent":"Mozilla\/5.0 (Macintosh; Intel Mac OS X 10_11_4) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/51.0.2704.84 Safari\/537.36",
    "created_via":"checkout",
    "customer_note":"",
    "date_completed":"2016-06-16T06:23:23",
    "date_paid":"",
    "cart_hash":"837192a02bc12d1ac767df9be65464c1",
    "line_items":[  
      {  
        "id":52,
        "name":"Simple subscription",
        "sku":"",
        "product_id":28,
        "variation_id":0,
        "quantity":1,
        "tax_class":"",
        "price":"45.45",
        "subtotal":"45.45",
        "subtotal_tax":"4.55",
        "total":"45.45",
        "total_tax":"4.55",
        "taxes":[  
          {  
            "id":1,
            "total":"4.5455",
            "subtotal":"4.5455"
          },
          {  
            "id":2,
            "total":"",
            "subtotal":""
          }
        ],
        "meta":[  

        ]
      }
    ],
    "tax_lines":[  
      {  
        "id":54,
        "rate_code":"GST-1",
        "rate_id":"1",
        "label":"GST",
        "compound":false,
        "tax_total":"4.55",
        "shipping_tax_total":"0.00"
      },
      {  
        "id":55,
        "rate_code":"SHIP-1",
        "rate_id":"2",
        "label":"Ship",
        "compound":false,
        "tax_total":"0.00",
        "shipping_tax_total":"7.50"
      }
    ],
    "shipping_lines":[  
      {  
        "id":53,
        "method_title":"Flat Rate",
        "method_id":"flat_rate:1",
        "total":"15.00",
        "total_tax":"7.50",
        "taxes":[  
          {  
            "id":1,
            "total":""
          },
          {  
            "id":2,
            "total":"7.5"
          }
        ]
      }
    ],
    "fee_lines":[  

    ],
    "coupon_lines":[  

    ],
    "refunds":[  

    ],
    "billing_period":"month",
    "billing_interval":"1",
    "start_date":"2016-06-16T06:22:58",
    "trial_end_date":"",
    "next_payment_date":"2016-07-16T06:22:58",
    "end_date":""
    "_links":{  
      "self":[  
        {  
          "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/subscriptions\/316"
        }
      ],
      "collection":[  
        {  
          "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/subscriptions"
        }
      ],
      "customer":[  
        {  
          "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/customers\/1"
        }
      ],
      "up":[  
        {  
          "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/orders\/315"
        }
      ]
    }
  },
  {  
    "id":311,
    "parent_id":0,
    "status":"active",
    "order_key":"wc_order_575fd4665d2cc",
    "currency":"AUD",
    "version":"2.6.0",
    "prices_include_tax":true,
    "date_created":"2016-06-14T09:54:46",
    "date_modified":"2016-06-14T09:54:46",
    "customer_id":1,
    "discount_total":"0.00",
    "discount_tax":"0.00",
    "shipping_total":"0.00",
    "shipping_tax":"0.00",
    "cart_tax":"0.00",
    "total":"17.99",
    "total_tax":"0.00",
    "billing":{  
      "first_name":"",
      "last_name":"",
      "company":"",
      "address_1":"",
      "address_2":"",
      "city":"",
      "state":"",
      "postcode":"",
      "country":"",
      "email":"admin@example.com",
      "phone":""
    },
    "shipping":{  
      "first_name":"",
      "last_name":"",
      "company":"",
      "address_1":"",
      "address_2":"",
      "city":"",
      "state":"",
      "postcode":"",
      "country":""
    },
    "payment_method":"stripe",
    "payment_method_title":"Credit card (Stripe)",
    "transaction_id":"",
    "customer_ip_address":"",
    "customer_user_agent":"",
    "created_via":"rest-api",
    "customer_note":"",
    "date_completed":"2016-06-14T09:54:46",
    "date_paid":"",
    "cart_hash":"",
    "line_items":[  

    ],
    "tax_lines":[  

    ],
    "shipping_lines":[  

    ],
    "fee_lines":[  

    ],
    "coupon_lines":[  

    ],
    "refunds":[  

    ],
    "billing_period":"month",
    "billing_interval":"2",
    "start_date":"2016-06-14T09:54:46",
    "trial_end_date":"",
    "next_payment_date":"2017-05-05T08:08:08",
    "end_date":""
    "_links":{  
      "self":[  
        {  
          "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/subscriptions\/311"
        }
      ],
      "collection":[  
        {  
          "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/subscriptions"
        }
      ],
      "customer":[  
        {  
          "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/customers\/1"
        }
      ]
    }
  }
]
```

#### Available parameters ####

| Parameter  |   Type  |                                                                                                 Description                                                                                                  |
|------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `context`  | string  | Scope under which the request is made; determines fields present in response. Options: `view` and `edit`.                                                                                                    |
| `page`     | integer | Current page of the collection.                                                                                                                                                                              |
| `per_page` | integer | Maximum number of items to be returned in result set.                                                                                                                                                        |
| `search`   | string  | Limit results to those matching a string.                                                                                                                                                                    |
| `after`    | string  | Limit response to resources published after a given ISO8601 compliant date.                                                                                                                                  |
| `before`   | string  | Limit response to resources published before a given ISO8601 compliant date.                                                                                                                                 |
| `exclude`  | string  | Ensure result set excludes specific ids.                                                                                                                                                                     |
| `include`  | string  | Limit result set to specific ids.                                                                                                                                                                            |
| `offset`   | integer | Offset the result set by a specific number of items.                                                                                                                                                         |
| `order`    | string  | Order sort attribute ascending or descending. Default is `asc`. Options: `asc` and `desc`.                                                                                                                   |
| `orderby`  | string  | Sort collection by object attribute. Default is `date`, Options: `date`, `id`, `include`, `title` and `slug`.                                                                                                |
| `filter`   | string  | Use WP Query arguments to modify the response; private query vars require appropriate authorization.                                                                                                         |
| `status`   | string  | Limit result set to subscriptions assigned a specific status. Default is `any`. Options (plugins may add new status): `any`, `pending`, `on-hold`, `active`, `cancelled`, `pending-cancel` and `expired`.    |
| `customer` | string  | Limit result set to subscriptions assigned a specific customer.                                                                                                                                              |
| `product`  | string  | Limit result set to subscriptions assigned a specific product.                                                                                                                                               |
| `dp`       | string  | Number of decimal points to use in each resource.                                                                                                                                                            |

## Update a Subscription ##

This API lets you make changes to a subscription.

### HTTP Request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-put">PUT</i>
		<h6>/wp-json/wc/v1/subscriptions/&lt;id&gt;</h6>
	</div>
</div>

```shell
curl -X PUT https://example.com/wp-json/wc/v1/subscriptions/30 \
	-u consumer_key:consumer_secret \
	-H "Content-Type: application/json" \
	-d '{
  "status": "on-hold"
}'
```

```javascript
var data = {
  status: 'on-hold'
};

WooCommerce.put('subscriptions/30', data, function(err, data, res) {
  console.log(res);
});
```

```php
<?php
$data = [
    'status' => 'on-hold'
];

print_r($woocommerce->put('subscriptions/30', $data));
?>
```

```python
data = {
    "status": "on-hold"
}

print(wcapi.put("subscriptions/30", data).json())
```

```ruby
data = {
  status: "on-hold"
}

woocommerce.put("subscriptions/30", data).parsed_response
```

> JSON response example:

```json
{  
  "id":30,
  "parent_id":29,
  "status":"on-hold",
  "order_key":"wc_order_572ff79932a09",
  "currency":"AUD",
  "version":"2.6.0",
  "prices_include_tax":true,
  "date_created":"2016-05-09T02:36:09",
  "date_modified":"2016-06-21T07:11:46",
  "customer_id":1,
  "discount_total":"0.00",
  "discount_tax":"0.00",
  "shipping_total":"10.00",
  "shipping_tax":"1.00",
  "cart_tax":"4.55",
  "total":"61.00",
  "total_tax":"5.55",
  "billing":{  
    "first_name":"Matt",
    "last_name":"Allan",
    "company":"",
    "address_1":"123 Fake Street",
    "address_2":"",
    "city":"Brisbane",
    "state":"QLD",
    "postcode":"4101",
    "country":"AU",
    "email":"matt@prospress.com",
    "phone":"55555555"
  },
  "shipping":{  
    "first_name":"Matt",
    "last_name":"Allan",
    "company":"",
    "address_1":"123 Fake Street",
    "address_2":"",
    "city":"Brisbane",
    "state":"QLD",
    "postcode":"4101",
    "country":"AU"
  },
  "payment_method":"",
  "payment_method_title":"",
  "transaction_id":"",
  "customer_ip_address":"172.28.128.1",
  "customer_user_agent":"Mozilla\/5.0 (Macintosh; Intel Mac OS X 10_11_4) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/50.0.2661.86 Safari\/537.36",
  "created_via":"checkout",
  "customer_note":"",
  "date_completed":"2016-06-21T07:11:46",
  "date_paid":"",
  "cart_hash":"",
  "line_items":[  
    {  
      "id":12,
      "name":"Simple subscription",
      "sku":"",
      "product_id":28,
      "variation_id":0,
      "quantity":1,
      "tax_class":"",
      "price":"45.45",
      "subtotal":"45.45",
      "subtotal_tax":"4.55",
      "total":"45.45",
      "total_tax":"4.55",
      "taxes":[  
        {  
          "id":1,
          "total":"4.5455",
          "subtotal":"4.5455"
        }
      ],
      "meta":[  

      ]
    }
  ],
  "tax_lines":[  
    {  
      "id":14,
      "rate_code":"GST-1",
      "rate_id":"1",
      "label":"GST",
      "compound":false,
      "tax_total":"4.55",
      "shipping_tax_total":"1.00"
    }
  ],
  "shipping_lines":[  
    {  
      "id":13,
      "method_title":"Flat Rate",
      "method_id":"flat_rate",
      "total":"10.00",
      "total_tax":"1.00",
      "taxes":[  
        {  
          "id":1,
          "total":"1"
        }
      ]
    }
  ],
  "fee_lines":[  

  ],
  "coupon_lines":[  

  ],
  "refunds":[  

  ],
  "billing_period":"month",
  "billing_interval":"1",
  "start_date":"2016-05-09T02:36:09",
  "trial_end_date":"",
  "next_payment_date":"2016-07-09T02:36:09",
  "end_date":""
  "_links":{  
    "self":[  
      {  
        "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/subscriptions\/30"
      }
    ],
    "collection":[  
      {  
        "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/subscriptions"
      }
    ],
    "customer":[  
      {  
        "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/customers\/1"
      }
    ],
    "up":[  
      {  
        "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/orders\/29"
      }
    ]
  }
}
```

## Delete a Subscription ##

This API helps you delete a subscription.

### HTTP request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-delete">DELETE</i>
		<h6>/wp-json/wc/v1/subscriptions/&lt;id&gt;</h6>
	</div>
</div>

```shell
curl -X DELETE https://example.com/wp-json/wc/v1/subscriptions/22?force=true \
	-u consumer_key:consumer_secret
```

```javascript
WooCommerce.delete('subscriptions/22?force=true', function(err, data, res) {
  console.log(res);
});
```

```php
<?php print_r($woocommerce->delete('subscriptions/22', ['force' => true])); ?>
```

```python
print(wcapi.delete("subscriptions/22?force=true").json())
```

```ruby
woocommerce.delete("subscriptions/22", force: true).parsed_response
```

> JSON response example:

```json
{  
  "id":19,
  "parent_id":18,
  "status":"active",
  "order_key":"wc_order_572c3907068d1",
  "currency":"AUD",
  "version":"2.5.5",
  "prices_include_tax":false,
  "date_created":"2016-05-06T06:26:14",
  "date_modified":"2016-06-03T03:31:56",
  "customer_id":1,
  "discount_total":"0.00",
  "discount_tax":"0.00",
  "shipping_total":"10.00",
  "shipping_tax":"0.00",
  "cart_tax":"0.00",
  "total":"60.00",
  "total_tax":"0.00",
  "billing":{  
    "first_name":"Matt",
    "last_name":"Allan",
    "company":"",
    "address_1":"123 Fake Street",
    "address_2":"",
    "city":"Brisbane",
    "state":"QLD",
    "postcode":"4101",
    "country":"AU",
    "email":"matt@prospress.com",
    "phone":"55555555"
  },
  "shipping":{  
    "first_name":"Matt",
    "last_name":"Allan",
    "company":"",
    "address_1":"123 Fake Street",
    "address_2":"",
    "city":"Brisbane",
    "state":"QLD",
    "postcode":"4101",
    "country":"AU"
  },
  "payment_method":"stripe",
  "payment_method_title":"Credit card (Stripe)",
  "transaction_id":"",
  "customer_ip_address":"172.28.128.1",
  "customer_user_agent":"Mozilla\/5.0 (Macintosh; Intel Mac OS X 10_11_4) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/50.0.2661.86 Safari\/537.36",
  "created_via":"checkout",
  "customer_note":"",
  "date_completed":"2016-06-03T03:31:56",
  "date_paid":"",
  "cart_hash":"",
  "line_items":[  
    {  
      "id":2,
      "name":"Synced Simple Subscription",
      "sku":"",
      "product_id":12,
      "variation_id":0,
      "quantity":1,
      "tax_class":"",
      "price":"50.00",
      "subtotal":"50.00",
      "subtotal_tax":"0.00",
      "total":"50.00",
      "total_tax":"0.00",
      "taxes":[  

      ],
      "meta":[  

      ]
    }
  ],
  "tax_lines":[  

  ],
  "shipping_lines":[  
    {  
      "id":3,
      "method_title":"Flat Rate",
      "method_id":"flat_rate",
      "total":"10.00",
      "total_tax":"0.00",
      "taxes":[  

      ]
    }
  ],
  "fee_lines":[  

  ],
  "coupon_lines":[  

  ],
  "refunds":[  

  ],
  "billing_period":"month",
  "billing_interval":"1",
  "start_date":"2016-05-06T06:26:14",
  "trial_end_date":"",
  "next_payment_date":"2016-07-03T03:00:00",
  "end_date":""
  "_links":{  
    "self":[  
      {  
        "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/subscriptions\/19"
      }
    ],
    "collection":[  
      {  
        "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/subscriptions"
      }
    ],
    "customer":[  
      {  
        "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/customers\/1"
      }
    ],
    "up":[  
      {  
        "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/orders\/18"
      }
    ]
  }
}
```

#### Available parameters ####

| Parameter |  Type  |                                  Description                                   |
|-----------|--------|--------------------------------------------------------------------------------|
| `force`   | string | Use `true` whether to permanently delete the subscription, Default is `false`. |

## Batch Update Subscriptions ##

This API helps you to batch create, update and delete multiple subscriptions.

### HTTP request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-post">POST</i>
		<h6>/wp-json/wc/v1/subscriptions/batch</h6>
	</div>
</div>

```shell
curl -X POST https://example.com/wp-json/wc/v1/subscriptions/batch \
    -u consumer_key:consumer_secret \
    -H "Content-Type: application/json" \
    -d '{
  "create": [
    {
      "customer_id": 1,
      "billing_interval": 1,
      "billing_period": "month",
      "payment_method": "bacs",
      "payment_method_title": "Direct Bank Transfer",
      "billing": {
        "first_name": "John",
        "last_name": "Doe",
        "address_1": "969 Market",
        "address_2": "",
        "city": "San Francisco",
        "state": "CA",
        "postcode": "94103",
        "country": "US",
        "email": "john.doe@example.com",
        "phone": "(555) 555-5555"
      },
      "shipping": {
        "first_name": "John",
        "last_name": "Doe",
        "address_1": "969 Market",
        "address_2": "",
        "city": "San Francisco",
        "state": "CA",
        "postcode": "94103",
        "country": "US"
      },
      "line_items": [
        {
          "product_id": 11,
          "quantity": 2
        },
        {
          "product_id": 28,
          "quantity": 1
        }
      ],
      "shipping_lines": [
        {
          "method_id": "flat_rate",
          "method_title": "Flat Rate",
          "total": 30
        }
      ]
    },
    {
      "customer_id": 1,
      "billing_interval": 1,
      "billing_period": "month",
      "payment_method": "bacs",
      "payment_method_title": "Direct Bank Transfer",
      "set_paid": true,
      "billing": {
        "first_name": "John",
        "last_name": "Doe",
        "address_1": "969 Market",
        "address_2": "",
        "city": "San Francisco",
        "state": "CA",
        "postcode": "94103",
        "country": "US",
        "email": "john.doe@example.com",
        "phone": "(555) 555-5555"
      },
      "shipping": {
        "first_name": "John",
        "last_name": "Doe",
        "address_1": "969 Market",
        "address_2": "",
        "city": "San Francisco",
        "state": "CA",
        "postcode": "94103",
        "country": "US"
      },
      "line_items": [
        {
          "product_id": 28,
          "quantity": 2
        }
      ],
      "shipping_lines": [
        {
          "method_id": "flat_rate",
          "method_title": "Flat Rate",
          "total": 20
        }
      ]
    }
  ],
  "update": [
    {
      "id": 316,
      "status": "active"
    }
  ],
  "delete": [
    299
  ]
}'
```

```javascript
var data = {
  create: [
    {
      customer_id: 1,
      billing_interval: 1,
      billing_period: 'month',
      payment_method: 'bacs',
      payment_method_title: 'Direct Bank Transfer',
      billing: {
        first_name: 'John',
        last_name: 'Doe',
        address_1: '969 Market',
        address_2: '',
        city: 'San Francisco',
        state: 'CA',
        postcode: '94103',
        country: 'US',
        email: 'john.doe@example.com',
        phone: '(555) 555-5555'
      },
      shipping: {
        first_name: 'John',
        last_name: 'Doe',
        address_1: '969 Market',
        address_2: '',
        city: 'San Francisco',
        state: 'CA',
        postcode: '94103',
        country: 'US'
      },
      line_items: [
        {
          product_id: 11,
          quantity: 2
        },
        {
          product_id: 28,
          quantity: 1
        }
      ],
      shipping_lines: [
        {
          method_id: 'flat_rate',
          method_title: 'Flat Rate',
          total: 30
        }
      ]
    },
    {
      customer_id: 1,
      billing_interval: 1,
      billing_period: 'month',
      payment_method: 'bacs',
      payment_method_title: 'Direct Bank Transfer',
      set_paid: true,
      billing: {
        first_name: 'John',
        last_name: 'Doe',
        address_1: '969 Market',
        address_2: '',
        city: 'San Francisco',
        state: 'CA',
        postcode: '94103',
        country: 'US',
        email: 'john.doe@example.com',
        phone: '(555) 555-5555'
      },
      shipping: {
        first_name: 'John',
        last_name: 'Doe',
        address_1: '969 Market',
        address_2: '',
        city: 'San Francisco',
        state: 'CA',
        postcode: '94103',
        country: 'US'
      },
      line_items: [
        {
          product_id: 28,
          quantity: 2
        }
      ],
      shipping_lines: [
        {
          method_id: 'flat_rate',
          method_title: 'Flat Rate',
          total: 20
        }
      ]
    }
  ],
  update: [
    {
      id: 316,
      status: 'active'
    }
  ],
  delete: [
    299
  ]
};

WooCommerce.post('subscriptions/batch', data, function(err, data, res) {
  console.log(res);
});
```

```php
<?php
$data = [
    'create' => [
        [
            'customer_id => 1,
            'billing_interval' => 1,
            'billing_period' => 'month',
            'payment_method' => 'bacs',
            'payment_method_title' => 'Direct Bank Transfer',
            'billing' => [
                'first_name' => 'John',
                'last_name' => 'Doe',
                'address_1' => '969 Market',
                'address_2' => '',
                'city' => 'San Francisco',
                'state' => 'CA',
                'postcode' => '94103',
                'country' => 'US',
                'email' => 'john.doe@example.com',
                'phone' => '(555) 555-5555'
            ],
            'shipping' => [
                'first_name' => 'John',
                'last_name' => 'Doe',
                'address_1' => '969 Market',
                'address_2' => '',
                'city' => 'San Francisco',
                'state' => 'CA',
                'postcode' => '94103',
                'country' => 'US'
            ],
            'line_items' => [
                [
                    'product_id' => 11,
                    'quantity' => 2
                ],
                [
                    'product_id' => 28,
                    'quantity' => 1
                ]
            ],
            'shipping_lines' => [
                [
                    'method_id' => 'flat_rate',
                    'method_title' => 'Flat Rate',
                    'total' => 30
                ]
            ]
        ],
        [
            'customer_id' => 1,
            'billing_interval' => 1,
            'billing_period' => 'month',
            'payment_method' => 'bacs',
            'payment_method_title' => 'Direct Bank Transfer',
            'set_paid' => true,
            'billing' => [
                'first_name' => 'John',
                'last_name' => 'Doe',
                'address_1' => '969 Market',
                'address_2' => '',
                'city' => 'San Francisco',
                'state' => 'CA',
                'postcode' => '94103',
                'country' => 'US',
                'email' => 'john.doe@example.com',
                'phone' => '(555) 555-5555'
            ],
            'shipping' => [
                'first_name' => 'John',
                'last_name' => 'Doe',
                'address_1' => '969 Market',
                'address_2' => '',
                'city' => 'San Francisco',
                'state' => 'CA',
                'postcode' => '94103',
                'country' => 'US'
            ],
            'line_items' => [
                [
                    'product_id' => 28,
                    'quantity' => 2
                [
            ],
            'shipping_lines' => [
                [
                    'method_id' => 'flat_rate',
                    'method_title' => 'Flat Rate',
                    'total' => 20
                ]
            ]
        ]
    ],
    'update' => [
        [
            'id' => 316,
            'status' => 'active'
        ]
    ],
    'delete' => [
        299
    ]
];

print_r($woocommerce->post('subscriptions/batch', $data));
?>
```

```python
data = {
    "create": [
        {
            "customer_id": 1,
            "billing_interval": 1,
            "billing_period": "month",
            "payment_method": "bacs",
            "payment_method_title": "Direct Bank Transfer",
            "billing": {
                "first_name": "John",
                "last_name": "Doe",
                "address_1": "969 Market",
                "address_2": "",
                "city": "San Francisco",
                "state": "CA",
                "postcode": "94103",
                "country": "US",
                "email": "john.doe@example.com",
                "phone": "(555) 555-5555"
            },
            "shipping": {
                "first_name": "John",
                "last_name": "Doe",
                "address_1": "969 Market",
                "address_2": "",
                "city": "San Francisco",
                "state": "CA",
                "postcode": "94103",
                "country": "US"
            },
            "line_items": [
                {
                    "product_id": 11,
                    "quantity": 2
                },
                {
                    "product_id": 28,
                    "quantity": 1
                }
            ],
            "shipping_lines": [
                {
                    "method_id": "flat_rate",
                    "method_title": "Flat Rate",
                    "total": 30
                }
            ]
        },
        {
            "customer_id": 1,
            "billing_interval": 1,
            "billing_period": "month",
            "payment_method": "bacs",
            "payment_method_title": "Direct Bank Transfer",
            "set_paid": True,
            "billing": {
                "first_name": "John",
                "last_name": "Doe",
                "address_1": "969 Market",
                "address_2": "",
                "city": "San Francisco",
                "state": "CA",
                "postcode": "94103",
                "country": "US",
                "email": "john.doe@example.com",
                "phone": "(555) 555-5555"
            },
            "shipping": {
                "first_name": "John",
                "last_name": "Doe",
                "address_1": "969 Market",
                "address_2": "",
                "city": "San Francisco",
                "state": "CA",
                "postcode": "94103",
                "country": "US"
            },
            "line_items": [
                {
                    "product_id": 28,
                    "quantity": 2
                }
            ],
            "shipping_lines": [
                {
                    "method_id": "flat_rate",
                    "method_title": "Flat Rate",
                    "total": 20
                }
            ]
        }
    ],
    "update": [
        {
            "id": 316,
            "status": "active"
        }
    ],
    "delete": [
        299
    ]
}

print(wcapi.post("subscriptions/batch", data).json())
```

```ruby
data = {
  create: [
    {
      customer_id: 1,
      billing_interval: 1,
      billing_period: "month",
      payment_method: "bacs",
      payment_method_title: "Direct Bank Transfer",
      billing: {
        first_name: "John",
        last_name: "Doe",
        address_1: "969 Market",
        address_2: "",
        city: "San Francisco",
        state: "CA",
        postcode: "94103",
        country: "US",
        email: "john.doe@example.com",
        phone: "(555) 555-5555"
      },
      shipping: {
        first_name: "John",
        last_name: "Doe",
        address_1: "969 Market",
        address_2: "",
        city: "San Francisco",
        state: "CA",
        postcode: "94103",
        country: "US"
      },
      line_items: [
        {
          product_id: 11,
          quantity: 2
        },
        {
          product_id: 28,
          quantity: 1
        }
      ],
      shipping_lines: [
        {
          method_id: "flat_rate",
          method_title: "Flat Rate",
          total: 30
        }
      ]
    },
    {
      customer_id: 1,
      billing_interval: 1,
      billing_period: "month",
      payment_method: "bacs",
      payment_method_title: "Direct Bank Transfer",
      set_paid: true,
      billing: {
        first_name: "John",
        last_name: "Doe",
        address_1: "969 Market",
        address_2: "",
        city: "San Francisco",
        state: "CA",
        postcode: "94103",
        country: "US",
        email: "john.doe@example.com",
        phone: "(555) 555-5555"
      },
      shipping: {
        first_name: "John",
        last_name: "Doe",
        address_1: "969 Market",
        address_2: "",
        city: "San Francisco",
        state: "CA",
        postcode: "94103",
        country: "US"
      },
      line_items: [
        {
          product_id: 28,
          quantity: 2
        }
      ],
      shipping_lines: [
        {
          method_id: "flat_rate",
          method_title: "Flat Rate",
          total: 20
        }
      ]
    }
  ],
  update: [
    {
      id: 316,
      status: "active"
    }
  ],
  delete: [
    299
  ]
}

woocommerce.post("subscriptions/batch", data).parsed_response
```

> JSON response example:

```json
{  
  "create":[  
    {  
      "id":331,
      "parent_id":0,
      "status":"pending",
      "order_key":"wc_order_576a173410502",
      "currency":"AUD",
      "version":"2.6.0",
      "prices_include_tax":true,
      "date_created":"2016-06-22T04:42:28",
      "date_modified":"2016-06-22T04:42:28",
      "customer_id":1,
      "discount_total":"0.00",
      "discount_tax":"0.00",
      "shipping_total":"30.00",
      "shipping_tax":"15.00",
      "cart_tax":"13.64",
      "total":"195.00",
      "total_tax":"28.64",
      "billing":{  
        "first_name":"John",
        "last_name":"Doe",
        "company":"",
        "address_1":"969 Market",
        "address_2":"",
        "city":"San Francisco",
        "state":"CA",
        "postcode":"94103",
        "country":"US",
        "email":"john.doe@example.com",
        "phone":"(555) 555-5555"
      },
      "shipping":{  
        "first_name":"John",
        "last_name":"Doe",
        "company":"",
        "address_1":"969 Market",
        "address_2":"",
        "city":"San Francisco",
        "state":"CA",
        "postcode":"94103",
        "country":"US"
      },
      "payment_method":"bacs",
      "payment_method_title":"bacs",
      "transaction_id":"",
      "customer_ip_address":"",
      "customer_user_agent":"",
      "created_via":"rest-api",
      "customer_note":"",
      "date_completed":"2016-06-22T04:42:28",
      "date_paid":"",
      "cart_hash":"",
      "line_items":[  
        {  
          "id":77,
          "name":"Cooper Dukes",
          "sku":"",
          "product_id":11,
          "variation_id":0,
          "quantity":2,
          "tax_class":"",
          "price":"45.45",
          "subtotal":"90.91",
          "subtotal_tax":"9.09",
          "total":"90.91",
          "total_tax":"9.09",
          "taxes":[  
            {  
              "id":1,
              "total":9.0909,
              "subtotal":9.0909
            }
          ],
          "meta":[  

          ]
        },
        {  
          "id":78,
          "name":"Simple subscription",
          "sku":"",
          "product_id":28,
          "variation_id":0,
          "quantity":1,
          "tax_class":"",
          "price":"45.45",
          "subtotal":"45.45",
          "subtotal_tax":"4.55",
          "total":"45.45",
          "total_tax":"4.55",
          "taxes":[  
            {  
              "id":1,
              "total":4.5455,
              "subtotal":4.5455
            }
          ],
          "meta":[  

          ]
        }
      ],
      "tax_lines":[  
        {  
          "id":80,
          "rate_code":"GST-1",
          "rate_id":"1",
          "label":"GST",
          "compound":false,
          "tax_total":"13.64",
          "shipping_tax_total":"0.00"
        },
        {  
          "id":81,
          "rate_code":"SHIP-1",
          "rate_id":"2",
          "label":"Ship",
          "compound":false,
          "tax_total":"0.00",
          "shipping_tax_total":"15.00"
        }
      ],
      "shipping_lines":[  
        {  
          "id":79,
          "method_title":"Flat Rate",
          "method_id":"flat_rate",
          "total":"30.00",
          "total_tax":"0.00",
          "taxes":[  

          ]
        }
      ],
      "fee_lines":[  

      ],
      "coupon_lines":[  

      ],
      "refunds":[  

      ],
      "billing_period":"month",
      "billing_interval":"1",
      "start_date":"2016-06-22T04:42:28",
      "trial_end_date":"",
      "next_payment_date":"",
      "end_date":""
      "_links":{  
        "self":[  
          {  
            "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/subscriptions\/331"
          }
        ],
        "collection":[  
          {  
            "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/subscriptions"
          }
        ],
        "customer":[  
          {  
            "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/customers\/1"
          }
        ]
      }
    },
    {  
      "id":332,
      "parent_id":0,
      "status":"active",
      "order_key":"wc_order_576a17342656c",
      "currency":"AUD",
      "version":"2.6.0",
      "prices_include_tax":true,
      "date_created":"2016-06-22T04:42:28",
      "date_modified":"2016-06-22T04:42:28",
      "customer_id":1,
      "discount_total":"0.00",
      "discount_tax":"0.00",
      "shipping_total":"20.00",
      "shipping_tax":"10.00",
      "cart_tax":"9.09",
      "total":"130.00",
      "total_tax":"19.09",
      "billing":{  
        "first_name":"John",
        "last_name":"Doe",
        "company":"",
        "address_1":"969 Market",
        "address_2":"",
        "city":"San Francisco",
        "state":"CA",
        "postcode":"94103",
        "country":"US",
        "email":"john.doe@example.com",
        "phone":"(555) 555-5555"
      },
      "shipping":{  
        "first_name":"John",
        "last_name":"Doe",
        "company":"",
        "address_1":"969 Market",
        "address_2":"",
        "city":"San Francisco",
        "state":"CA",
        "postcode":"94103",
        "country":"US"
      },
      "payment_method":"bacs",
      "payment_method_title":"bacs",
      "transaction_id":"",
      "customer_ip_address":"",
      "customer_user_agent":"",
      "created_via":"rest-api",
      "customer_note":"",
      "date_completed":"2016-06-22T04:42:28",
      "date_paid":"",
      "cart_hash":"",
      "line_items":[  
        {  
          "id":82,
          "name":"Simple subscription",
          "sku":"",
          "product_id":28,
          "variation_id":0,
          "quantity":2,
          "tax_class":"",
          "price":"45.45",
          "subtotal":"90.91",
          "subtotal_tax":"9.09",
          "total":"90.91",
          "total_tax":"9.09",
          "taxes":[  
            {  
              "id":1,
              "total":9.0909,
              "subtotal":9.0909
            }
          ],
          "meta":[  

          ]
        }
      ],
      "tax_lines":[  
        {  
          "id":84,
          "rate_code":"GST-1",
          "rate_id":"1",
          "label":"GST",
          "compound":false,
          "tax_total":"9.09",
          "shipping_tax_total":"0.00"
        },
        {  
          "id":85,
          "rate_code":"SHIP-1",
          "rate_id":"2",
          "label":"Ship",
          "compound":false,
          "tax_total":"0.00",
          "shipping_tax_total":"10.00"
        }
      ],
      "shipping_lines":[  
        {  
          "id":83,
          "method_title":"Flat Rate",
          "method_id":"flat_rate",
          "total":"20.00",
          "total_tax":"0.00",
          "taxes":[  

          ]
        }
      ],
      "fee_lines":[  

      ],
      "coupon_lines":[  

      ],
      "refunds":[  

      ],
      "billing_period":"month",
      "billing_interval":"1",
      "start_date":"2016-06-22T04:42:28",
      "trial_end_date":"",
      "next_payment_date":"2016-07-22T04:42:28",
      "end_date":""
      "_links":{  
        "self":[  
          {  
            "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/subscriptions\/332"
          }
        ],
        "collection":[  
          {  
            "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/subscriptions"
          }
        ],
        "customer":[  
          {  
            "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/customers\/1"
          }
        ]
      }
    }
  ],
  "update":[  
    {  
      "id":316,
      "parent_id":315,
      "status":"active",
      "order_key":"wc_order_576245c257a1f",
      "currency":"AUD",
      "version":"2.6.0",
      "prices_include_tax":true,
      "date_created":"2016-06-16T06:22:58",
      "date_modified":"2016-06-22T04:42:28",
      "customer_id":1,
      "discount_total":"0.00",
      "discount_tax":"0.00",
      "shipping_total":"15.00",
      "shipping_tax":"7.50",
      "cart_tax":"4.55",
      "total":"72.50",
      "total_tax":"12.05",
      "billing":{  
        "first_name":"John",
        "last_name":"Doe",
        "company":"",
        "address_1":"969 Market",
        "address_2":"",
        "city":"San Francisco",
        "state":"CA",
        "postcode":"94103",
        "country":"US",
        "email":"john.doe@example.com",
        "phone":"(555) 555-5555"
      },
      "shipping":{  
        "first_name":"John",
        "last_name":"Doe",
        "company":"",
        "address_1":"969 Market",
        "address_2":"",
        "city":"San Francisco",
        "state":"CA",
        "postcode":"94103",
        "country":"US"
      },
      "payment_method":"",
      "payment_method_title":"",
      "transaction_id":"",
      "customer_ip_address":"172.28.128.1",
      "customer_user_agent":"Mozilla\/5.0 (Macintosh; Intel Mac OS X 10_11_4) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/51.0.2704.84 Safari\/537.36",
      "created_via":"checkout",
      "customer_note":"",
      "date_completed":"2016-06-22T04:42:28",
      "date_paid":"",
      "cart_hash":"837192a02bc12d1ac767df9be65464c1",
      "line_items":[  
        {  
          "id":52,
          "name":"Simple subscription",
          "sku":"",
          "product_id":28,
          "variation_id":0,
          "quantity":1,
          "tax_class":"",
          "price":"45.45",
          "subtotal":"45.45",
          "subtotal_tax":"4.55",
          "total":"45.45",
          "total_tax":"4.55",
          "taxes":[  
            {  
              "id":1,
              "total":"4.5455",
              "subtotal":"4.5455"
            },
            {  
              "id":2,
              "total":"",
              "subtotal":""
            }
          ],
          "meta":[  

          ]
        }
      ],
      "tax_lines":[  
        {  
          "id":54,
          "rate_code":"GST-1",
          "rate_id":"1",
          "label":"GST",
          "compound":false,
          "tax_total":"4.55",
          "shipping_tax_total":"0.00"
        },
        {  
          "id":55,
          "rate_code":"SHIP-1",
          "rate_id":"2",
          "label":"Ship",
          "compound":false,
          "tax_total":"0.00",
          "shipping_tax_total":"7.50"
        }
      ],
      "shipping_lines":[  
        {  
          "id":53,
          "method_title":"Flat Rate",
          "method_id":"flat_rate:1",
          "total":"15.00",
          "total_tax":"7.50",
          "taxes":[  
            {  
              "id":1,
              "total":""
            },
            {  
              "id":2,
              "total":"7.5"
            }
          ]
        }
      ],
      "fee_lines":[  

      ],
      "coupon_lines":[  

      ],
      "refunds":[  

      ],
      "billing_period":"month",
      "billing_interval":"1",
      "start_date":"2016-06-16T06:22:58",
      "trial_end_date":"",
      "next_payment_date":"2016-07-16T06:22:58",
      "end_date":""
      "_links":{  
        "self":[  
          {  
            "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/subscriptions\/316"
          }
        ],
        "collection":[  
          {  
            "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/subscriptions"
          }
        ],
        "customer":[  
          {  
            "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/customers\/1"
          }
        ],
        "up":[  
          {  
            "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/orders\/315"
          }
        ]
      }
    }
  ],
  "delete":[  
    {  
      "id":299,
      "parent_id":0,
      "status":"active",
      "order_key":"wc_order_57566af9429d9",
      "currency":"AUD",
      "version":"2.6.0",
      "prices_include_tax":true,
      "date_created":"2016-06-07T06:34:33",
      "date_modified":"2016-06-07T06:34:33",
      "customer_id":1,
      "discount_total":"0.00",
      "discount_tax":"0.00",
      "shipping_total":"0.00",
      "shipping_tax":"0.00",
      "cart_tax":"0.00",
      "total":"17.99",
      "total_tax":"0.00",
      "billing":{  
        "first_name":"",
        "last_name":"",
        "company":"",
        "address_1":"",
        "address_2":"",
        "city":"",
        "state":"",
        "postcode":"",
        "country":"",
        "email":"admin@example.com",
        "phone":""
      },
      "shipping":{  
        "first_name":"",
        "last_name":"",
        "company":"",
        "address_1":"",
        "address_2":"",
        "city":"",
        "state":"",
        "postcode":"",
        "country":""
      },
      "payment_method":"stripe",
      "payment_method_title":"Credit card (Stripe)",
      "transaction_id":"",
      "customer_ip_address":"",
      "customer_user_agent":"",
      "created_via":"rest-api",
      "customer_note":"",
      "date_completed":"2016-06-07T06:34:33",
      "date_paid":"",
      "cart_hash":"",
      "line_items":[  

      ],
      "tax_lines":[  

      ],
      "shipping_lines":[  

      ],
      "fee_lines":[  

      ],
      "coupon_lines":[  

      ],
      "refunds":[  

      ],
      "billing_period":"month",
      "billing_interval":"2",
      "start_date":"2016-06-07T06:34:33",
      "trial_end_date":"",
      "next_payment_date":"2017-05-05T08:08:08",
      "end_date":""
      "_links":{  
        "self":[  
          {  
            "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/subscriptions\/299"
          }
        ],
        "collection":[  
          {  
            "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/subscriptions"
          }
        ],
        "customer":[  
          {  
            "href":"https:\/\/vagrant.local\/wp-json\/wc\/v1\/customers\/1"
          }
        ]
      }
    }
  ]
}
```

## Get Statuses ##

This API returns all available subscription statuses.

### HTTP request ###

<div class="api-endpoint">
  <div class="endpoint-data">
    <i class="label label-delete">GET</i>
    <h6>/wp-json/wc/v1/subscriptions/statuses</h6>
  </div>
</div>

```shell
curl -k https://vagrant.local/wp-json/wc/v1/subscriptions/statuses
```

```javascript
WooCommerce.get('subscriptions/statuses', data, function(err, data, res) {
  console.log(res);
```

```php
print_r($woocommerce->get('subscriptions/statuses'));
```

```python
print(wcapi.get("subscriptions/statuses").json())
```

```ruby
woocommerce.get("subscriptions/statuses").parsed_response
```

> JSON response example:

```json
{
  "wc-pending": "Pending",
  "wc-active": "Active",
  "wc-on-hold": "On hold",
  "wc-cancelled": "Cancelled",
  "wc-switched": "Switched",
  "wc-expired": "Expired",
  "wc-pending-cancel": "Pending Cancellation"
}
```
