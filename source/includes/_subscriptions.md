# Subscriptions #

The Subscriptions API enables you to create, view, update, and delete individual, or a batch of subscriptions.

## Subscription properties ##

|          Attribute          |    Type   |                                                                                              Description                                                                                                 |
|-----------------------------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `id`                        | integer   | Unique identifier for the resource.                                                                                                                                                                      |
| `parent_id`                 | integer   | Parent/initial order ID for the subscription.                                                                                                                                                            |
| `status`                    | string    | Subscription status. Default is `pending`. Options (plugins may include new status): `pending`, `active`, `on-hold`, `expired`, `pending-cancel` and `cancelled`. See [Setting status](#setting-status). |
| `currency`                  | string    | Currency the subscription was created with, in ISO format.                                                                                                                                               |
| `version`                   | string    | Version of WooCommerce when the subscription was made. <i class="label label-info">read-only</i>                                                                                                         |
| `prices_include_tax`        | boolean   | Shows if the prices included tax during checkout. <i class="label label-info">read-only</i>                                                                                                              |
| `date_created`              | date-time | The date the subscription was created, in the site's timezone. <i class="label label-info">read-only</i>                                                                                                 |
| `date_modified`             | date-time | The date the subscription was last modified, in the site's timezone. <i class="label label-info">read-only</i>                                                                                           |
| `date_completed`            | date-time | The date the subscription was completed, in the site's timezone. <i class="label label-info">read-only</i>                                                                                               |
| `date_paid`                 | date-time | The date the subscription has been paid, in the site's timezone. <i class="label label-info">read-only</i>                                                                                               |
| `date_created_gmt`          | data-time | The date the subscription was created, as GMT.                                                                                                                                                           |
| `date_modified_gmt`         | data-time | The date the subscription was modified, as GMT.                                                                                                                                                          |
| `date_completed_gmt`        | data-time | The date the subscription was completed, as GMT.                                                                                                                                                         |
| `date_paid_gmt`             | data-time | The date the subscription was paid, as GMT.                                                                                                                                                              |
| `start_date_gmt`            | date-time | The subscription's start date in GMT. Defaults to the current time. In a write context. it must be the format `YYYY-mm-dd H:i:s`.                                                                        |
| `trial_end_date_gmt`        | date-time | The subscription's trial end date in GMT. In a write context, it must be the format `YYYY-mm-dd H:i:s`.                                                                                                  |
| `next_payment_date_gmt`     | date-time | The subscription's next payment date in GMT. In a write context, it must be the format `YYYY-mm-dd H:i:s`.                                                                                               |
| `last_payment_date_gmt`     | date-time | The subscription's last parent, renewal or switch order date in GMT.                                                                                                                                     |
| `cancelled_date_gmt`        | date-time | The date the subscription was cancelled in GMT. In a write context, it must be the format `YYYY-mm-dd H:i:s`.                                                                                            |
| `end_date_gmt`              | date-time | The subscription's end date in GMT. In a write context, it must be the format `YYYY-mm-dd H:i:s`.                                                                                                        |
| `discount_total`            | string    | Total discount amount for the subscription. <i class="label label-info">read-only</i>                                                                                                                    |
| `discount_tax`              | string    | Total discount tax amount for the subscription. <i class="label label-info">read-only</i>                                                                                                                |
| `shipping_total`            | string    | Total shipping amount for the subscription. <i class="label label-info">read-only</i>                                                                                                                    |
| `shipping_tax`              | string    | Total shipping tax amount for the subscription. <i class="label label-info">read-only</i>                                                                                                                |
| `cart_tax`                  | string    | Sum of line item taxes only. <i class="label label-info">read-only</i>                                                                                                                                   |
| `total`                     | string    | Grand total. <i class="label label-info">read-only</i>                                                                                                                                                   |
| `total_tax`                 | string    | Sum of all taxes. <i class="label label-info">read-only</i>                                                                                                                                              |
| `customer_id`               | integer   | User ID who owns the subscription.                                                                                                                                                                       |
| `order_key`                 | string    | Order key. <i class="label label-info">read-only</i>                                                                                                                                                     |
| `billing`                   | array     | Billing address. See [Subscription customer billing address properties](#subscription-billing-address-properties).                                                                                       |
| `shipping`                  | array     | Shipping address. See [Subscription customer shipping address properties](#subscription-shipping-address-properties).                                                                                    |
| `payment_method`            | string    | Payment method ID.                                                                                                                                                                                       |
| `payment_method_title`      | string    | Payment method title.                                                                                                                                                                                    |
| `customer_ip_address`       | string    | Customer's IP address. <i class="label label-info">read-only</i>                                                                                                                                         |
| `customer_user_agent`       | string    | User agent of the customer. <i class="label label-info">read-only</i>                                                                                                                                    |
| `created_via`               | string    | Where the subscription was created. <i class="label label-info">read-only</i>                                                                                                                            |
| `customer_note`             | string    | Note left by customer during checkout.                                                                                                                                                                   |
| `number`                    | string    | The subscription's number.                                                                                                                                                                               |
| `meta_data`                 | array     | Meta data. See [Subscription meta data properties](#subscription-meta-data-properties).                                                                                                                  |
| `line_items`                | array     | Line items data. See [Subscription line items properties](#subscription-line-item-properties).                                                                                                           |
| `tax_lines`                 | array     | Tax lines data. See [Subscription tax lines properties](#subscription-tax-lines-properties). <i class="label label-info">read-only</i>                                                                   |
| `shipping_lines`            | array     | Shipping lines data. See [Subscription shipping lines properties](#subscription-shipping-lines-properties).                                                                                              |
| `fee_lines`                 | array     | Fee lines data. See [Subscription fee lines properties](#subscription-fee-lines-properties).                                                                                                             |
| `coupon_lines`              | array     | Coupons line data. See [Subscription coupon lines properties](#subscription-coupon-line-properties).                                                                                                     |
| `billing_period`            | string    | The subscription's billing period. Options: `day`, `week`, `month`and `year`.                                                                                                                            |
| `billing_interval`          | integer   | The number of billing periods between subscription renewals.                                                                                                                                             |
| `resubscribed_from`         | string    | The ID of the subscription this subscription was resubscribed from. <i class="label label-info">read-only</i>                                                                                            |
| `resubscribed_subscription` | string    | The ID of the new resubscribed subscription. <i class="label label-info">read-only</i>                                                                                                                   |
| `removed_line_items`        | array     | Item data for items removed by the customer from their my account page. See [Subscription line items properties](#subscription-line-item-properties). <i class="label label-info">read-only</i>          |
| `payment_details`           | array     | Payment method data. See [Payment details properties](#payment-details-properties). <i class="label label-info">edit-only</i>                                                                            |
| `status_transition`         | string    | The subscription status to transition to. Status transitions will re-calculate the appropriote subscription dates. See [Setting status](#setting-status) <i class="label label-info">write-only</i>      |

### Subscription billing address properties ###

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

### Subscription shipping address properties ###

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

### Subscription meta data properties ###

|   Attribute    |   Type  |                                          Description                                           |
|----------------|---------|------------------------------------------------------------------------------------------------|
| `id`           | integer | Meta ID. <i class="label label-info">read-only</i>                                             |
| `key`          | string  | Meta key.                                                                                      |
| `value`        | string  | Meta value.                                                                                    |

### Subscription line item properties ###

|   Attribute    |   Type  |                                                           Description                                                               |
|----------------|---------|-------------------------------------------------------------------------------------------------------------------------------------|
| `id`           | integer | Item ID. <i class="label label-info">read-only</i>                                                                                  |
| `name`         | string  | Product name. <i class="label label-info">read-only</i>                                                                             |
| `product_id`   | integer | Product ID.                                                                                                                         |
| `variation_id` | integer | Variation ID, if applicable.                                                                                                        |
| `quantity`     | integer | Quantity ordered.                                                                                                                   |
| `tax_class`    | string  | Slug of the tax class of product.                                                                                                   |
| `subtotal`     | string  | Line subtotal (before discounts).                                                                                                   |
| `subtotal_tax` | string  | Line subtotal tax (before discounts). <i class="label label-info">read-only</i>                                                     |
| `total`        | string  | Line total (after discounts).                                                                                                       |
| `total_tax`    | string  | Line total tax (after discounts). <i class="label label-info">read-only</i>                                                         |
| `taxes`        | array   | Line taxes. See [Subscription item taxes properties](#subscription-item-taxes-properties) <i class="label label-info">read-only</i> |
| `meta_data`    | array   | Meta data. See [Subscription item meta data properties](#subscription-item-meta-data-properties)                                    |
| `sku`          | string  | Product SKU. <i class="label label-info">read-only</i>                                                                              |
| `price`        | integer | Product price. <i class="label label-info">read-only</i>                                                                            |
| `parent_name`  | string  | Parent product name if the product is a variation.                                                                                  |

### Subscription item taxes properties ###

|   Attribute    |   Type  |                                          Description                                            |
|----------------|---------|-------------------------------------------------------------------------------------------------|
| `id`           | integer | Tax rate ID.                                                                                    |
| `total`        | string  | Tax total.                                                                                      |
| `subtotal`     | string  | Tax subtotal.                                                                                   |

### Subscription item meta data properties ###

|    Attribute    |   Type  |                                          Description                                            |
|-----------------|---------|-------------------------------------------------------------------------------------------------|
| `id`            | integer | Meta ID.                                                                                        |
| `key`           | string  | Meta key.                                                                                       |
| `value`         | string  | Meta value.                                                                                     |
| `display_key`   | string  | Meta key for UI display.                                                                        |
| `display_value` | string  | Meta value for UI display.                                                                      |

### Subscription tax lines properties ###

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
| `meta_data`          | array   | Meta data. See [Subscription item meta data properties](#subscription-item-meta-data-properties)                                                  |

### Subscription shipping lines properties ###

|   Attribute    |   Type  |                                                           Description                                                               |
|----------------|---------|-------------------------------------------------------------------------------------------------------------------------------------|
| `id`           | integer | Item ID. <i class="label label-info">read-only</i>                                                                                  |
| `method_title` | string  | Shipping method name.                                                                                                               |
| `method_id`    | string  | Shipping method ID. <i class="label label-info">required</i>                                                                        |
| `instance_id`  | string  | Shipping instance ID.                                                                                                               |
| `total`        | string  | Line total (after discounts).                                                                                                       |
| `total_tax`    | string  | Line total tax (after discounts). <i class="label label-info">read-only</i>                                                         |
| `taxes`        | array   | Line taxes. See [Subscription item taxes properties](#subscription-item-taxes-properties) <i class="label label-info">read-only</i> |
| `meta_data`    | array   | Meta data. See [Subscription item meta data properties](#subscription-item-meta-data-properties).                                   |

### Subscription fee lines properties ###

|  Attribute   |   Type  |                                                  Description                                                                        |
|--------------|---------|-------------------------------------------------------------------------------------------------------------------------------------|
| `id`         | integer | Item ID. <i class="label label-info">read-only</i>                                                                                  |
| `name`       | string  | Fee name. <i class="label label-info">required</i>                                                                                  |
| `tax_class`  | string  | Tax class. <i class="label label-info">required if the fee is taxable</i>                                                           |
| `tax_status` | string  | Tax status of fee. Set to `taxable` if need apply taxes.                                                                            |
| `amount`     | string  | Fee amount.                                                                                                                         |
| `total`      | string  | Line total (after discounts).                                                                                                       |
| `total_tax`  | string  | Line total tax (after discounts).                                                                                                   |
| `taxes`      | array   | Line taxes. See [Subscription item taxes properties](#subscription-item-taxes-properties) <i class="label label-info">read-only</i> |
| `meta_data`  | array   | Meta data. See [Subscription item meta data properties](#subscription-item-meta-data-properties)                                    |

### Subscription coupon line properties ###

|   Attribute    |   Type  |                                           Description                                            |
|----------------|---------|--------------------------------------------------------------------------------------------------|
| `id`           | integer | Item ID. <i class="label label-info">read-only</i>                                               |
| `code`         | string  | Coupon code. <i class="label label-info">required</i>                                            |
| `discount`     | string  | Discount total. <i class="label label-info">required</i>                                         |
| `discount_tax` | string  | Discount total tax. <i class="label label-info">read-only</i>                                    |
| `meta_data`    | array   | Meta data. See [Subscription item meta data properties](#subscription-item-meta-data-properties) |

### Payment details properties ###

When setting payment gateway meta you will need the following information:

1. The payment method ID. The request which sets the payment method meta must also contain the `payment_method`.
2. The meta key(s) the payment gateway uses to store the meta.
3. The meta value(s).
4. Where the meta is stored. Some gateways store the payment meta in post meta, and user meta.

The `payment_details` property format:

|  Attribute  | Type  |                                           Description                                               |
|-------------|-------|-----------------------------------------------------------------------------------------------------|
| `post_meta` | array | Payment meta stored as subscription meta. See [Payment details meta](#payment-details-meta)         |
| `user_meta` | array | Payment meta stored as user meta on the customer. See [Payment details meta](#payment-details-meta) |

See the example requests for an example of the correct format.

### Payment details meta

|     Key      | Type  |                                         Description                                             |
|------------- |-------|-------------------------------------------------------------------------------------------------|
| `{meta_key}` | array | The key is the payment meta key you want to set. The value is the payment meta.                 |


### Setting status ###

There are two ways you can set a subscriptions status, via the `status` and `status_transition` arguments. This short guide aims to explain the differences between both args.

#### `status` ####

- Simple sets the subscription status via `$subscription->set_status()`. No date calculations or changes occur.

#### `status_transition` ####

- Sets the subscription status via `$subscription->update_status()`.
- Using this method of `WC_Subscription::update_status()` to set the status is more inline with how setting a status by a user via the store behaves. For example:
   - Next payment dates are set or recalculated on activation.
   - Suspension counts are updated on on-hold/suspension.
   - Cancelled dates are set on cancellation.

In general, when setting a status, use `status` when you want to full control the subscription's dates. If you want the system to calculate the appropriate dates changes as if a user changed the status on the store, use `status_transition`.

<aside class="notice">
  <strong>Please note</strong>, when processing the request, the subscription status is set last and so setting date properties when using <strong><code>status_transition</code></strong> may lead to those dates being overriden by the transition calculations.
</aside>

## Create a subscription ##

This API creates a new subscription.

### HTTP request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-post">POST</i>
		<h6>/wp-json/wc/v3/subscriptions</h6>
	</div>
</div>

> Example of creating an active subscription with Stripe payment tokens:

```shell
curl -X POST https://example.com/wp-json/wc/v3/subscriptions \
  -u consumer_key:consumer_secret \
  -H "Content-Type: application/json" \
  -d '{
  "customer_id": 1,
  "status": "active",
  "billing_period": "month",
  "billing_interval": 3,
  "start_date": "2021-04-23 10:45:00",
  "next_payment_date":"2021-07-23 10:45:00",
  "payment_method": "stripe",
  "payment_details":{
    "post_meta": {
      "_stripe_customer_id":"cus_Yjw4cyvPHBFzc8",
      "_stripe_source_id":"src_BSFD2kaYChDBtg2tP5qn7R3E"
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
      "product_id": 1175,
      "quantity": 2
    },
    {
      "product_id": 633,
      "variation_id": 636,
      "quantity": 1
    }
  ],
  "shipping_lines": [
    {
      "method_id": "flat_rate",
      "method_title": "Flat Rate",
      "total": "10"
    }
  ],
   "meta_data": [
    {
      "key": "_custom_subscription_meta",
      "value": "custom meta"
    }
  ]
}'
```

```javascript
var data = {
  customer_id: 1,
  status: 'active',
  billing_period: 'month',
  billing_interval: 3,
  start_date: '2021-04-23 10:45:00',
  next_payment_date: '2021-07-23 10:45:00',
  payment_method: 'stripe',
  payment_details: {
    post_meta: {
      _stripe_customer_id: 'cus_Yjw4cyvPHBFzc8',
      _stripe_source_id: 'src_BSFD2kaYChDBtg2tP5qn7R3E'
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
      product_id: 1175,
      quantity: 2
    },
    {
      product_id: 633,
      variation_id: 636,
      quantity: 1
    }
  ],
  shipping_lines: [
    {
      method_id: 'flat_rate',
      method_title: 'Flat Rate',
      total: '10'
    }
  ],
  meta_data: [
    {
      key: '_custom_subscription_meta',
      value: 'custom meta'
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
    'customer_id'       => 1
    'status'            => 'active',
    'billing_period'    => 'month',
    'billing_interval'  => 3,
    'start_date'        => '2021-04-23 10:45:00',
    'next_payment_date' => '2021-07-23 10:45:00',
    'payment_method'    => 'stripe',
    'payment_details'   => [
      'post_meta' => [
        "_stripe_customer_id" => "cus_Yjw4cyvPHBFzc8",
        "_stripe_source_id"   => "src_BSFD2kaYChDBtg2tP5qn7R3E"
      ]
    ],
    'billing' => [
        'first_name' => 'John',
        'last_name'  => 'Doe',
        'address_1'  => '969 Market',
        'address_2'  => '',
        'city'       => 'San Francisco',
        'state'      => 'CA',
        'postcode'   => '94103',
        'country'    => 'US',
        'email'      => 'john.doe@example.com',
        'phone'      => '(555) 555-5555'
    ],
    'shipping' => [
        'first_name' => 'John',
        'last_name'  => 'Doe',
        'address_1'  => '969 Market',
        'address_2'  => '',
        'city'       => 'San Francisco',
        'state'      => 'CA',
        'postcode'   => '94103',
        'country'    => 'US'
    ],
    'line_items' => [
        [
            'product_id' => 1175,
            'quantity'   => 2
        ],
        [
            'product_id'   => 633,
            'variation_id' => 636,
            'quantity'     => 1
        ]
    ],
    'shipping_lines' => [
        [
            'method_id'    => 'flat_rate',
            'method_title' => 'Flat Rate',
            'total'        => '10'
        ]
    ],
    'meta_data' => [
        [
            'key'   => '_custom_subscription_meta',
            'value' => 'custom meta'
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
    "billing_interval": 3,
    "start_date": "2021-04-23 10:45:00",
    "next_payment_date":"2021-07-23 10:45:00",
    "payment_method": "stripe",
    "payment_details":{
      "post_meta": {
        "_stripe_customer_id":"cus_Yjw4cyvPHBFzc8",
        "_stripe_source_id":"src_BSFD2kaYChDBtg2tP5qn7R3E"
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
            "product_id": 1175,
            "quantity": 2
        },
        {
            "product_id": 633,
            "variation_id": 636,
            "quantity": 1
        }
    ],
    "shipping_lines": [
        {
            "method_id": "flat_rate",
            "method_title": "Flat Rate",
            "total": '10'
        }
    ],
    'meta_data': [
        {
            'key': '_custom_subscription_meta',
            'value': 'custom meta'
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
  billing_interval: 3,
  start_date: "2021-04-23 10:45:00",
  next_payment_date: "2021-07-23 10:45:00",
  payment_method: "stripe",
  payment_details: {
    post_meta: {
      _stripe_customer_id: "cus_Yjw4cyvPHBFzc8",
      _stripe_source_id: "src_BSFD2kaYChDBtg2tP5qn7R3E"
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
      product_id: 1175,
      quantity: 2
    },
    {
      product_id: 633,
      variation_id: 636,
      quantity: 1
    }
  ],
  shipping_lines: [
    {
      method_id: "flat_rate",
      method_title: "Flat Rate",
      total: '10'
    }
  ],
  meta_data: [
    {
      key: "_custom_subscription_meta",
      value: "custom meta",
    }
  ]
}

woocommerce.post("subscriptions", data).parsed_response
```

> JSON response example:

```json
{
    "id": 1313,
    "parent_id": 0,
    "status": "active",
    "currency": "USD",
    "version": "5.2.0",
    "prices_include_tax": true,
    "date_created": "2021-04-23T16:38:41",
    "date_modified": "2021-04-23T16:38:41",
    "discount_total": "0.00",
    "discount_tax": "0.00",
    "shipping_total": "10.00",
    "shipping_tax": "0.00",
    "cart_tax": "16.60",
    "total": "192.61",
    "total_tax": "16.60",
    "customer_id": 1,
    "order_key": "wc_order_lyCT6s4CE82cP",
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
    "payment_method_title": "Credit Card (Stripe)",
    "customer_ip_address": "",
    "customer_user_agent": "",
    "created_via": "rest-api",
    "customer_note": "",
    "date_completed": null,
    "date_paid": null,
    "number": "1313",
    "meta_data": [
        {
            "id": 53824,
            "key": "_custom_subscription_meta",
            "value": "custom meta"
        },
        {
            "id": 53825,
            "key": "_stripe_customer_id",
            "value": "cus_Yjw4cyvPHBFzc8"
        },
        {
            "id": 53826,
            "key": "_stripe_source_id",
            "value": "src_BSFD2kaYChDBtg2tP5qn7R3E"
        }
    ],
    "line_items": [
        {
            "id": 1685,
            "name": "Yearly",
            "product_id": 1175,
            "variation_id": 0,
            "quantity": 2,
            "tax_class": "",
            "subtotal": "126.48",
            "subtotal_tax": "12.65",
            "total": "126.48",
            "total_tax": "12.65",
            "taxes": [
                {
                    "id": 2,
                    "total": "12.648221",
                    "subtotal": "12.648221"
                }
            ],
            "meta_data": [],
            "sku": "",
            "price": 63.241107,
            "parent_name": null
        },
        {
            "id": 1686,
            "name": "Variable Subscription - Small",
            "product_id": 633,
            "variation_id": 636,
            "quantity": 1,
            "tax_class": "",
            "subtotal": "39.53",
            "subtotal_tax": "3.95",
            "total": "39.53",
            "total_tax": "3.95",
            "taxes": [
                {
                    "id": 2,
                    "total": "3.952569",
                    "subtotal": "3.952569"
                }
            ],
            "meta_data": [
                {
                    "id": 13607,
                    "key": "pa_size",
                    "value": "small",
                    "display_key": "Size",
                    "display_value": "Small"
                }
            ],
            "sku": "",
            "price": 39.525691999999999,
            "parent_name": "Variable Subscription"
        }
    ],
    "tax_lines": [
        {
            "id": 1688,
            "rate_code": "US-TAX-1",
            "rate_id": 2,
            "label": "TAX",
            "compound": true,
            "tax_total": "16.60",
            "shipping_tax_total": "0.00",
            "rate_percent": 10,
            "meta_data": []
        }
    ],
    "shipping_lines": [
        {
            "id": 1687,
            "method_title": "Flat Rate",
            "method_id": "flat_rate",
            "instance_id": "",
            "total": "10.00",
            "total_tax": "0.00",
            "taxes": [],
            "meta_data": []
        }
    ],
    "fee_lines": [],
    "coupon_lines": [],
    "date_created_gmt": "2021-04-23T06:38:41",
    "date_modified_gmt": "2021-04-23T06:38:41",
    "date_completed_gmt": null,
    "date_paid_gmt": null,
    "billing_period": "month",
    "billing_interval": "3",
    "start_date_gmt": "2021-04-23T10:45:00",
    "trial_end_date_gmt": "",
    "next_payment_date_gmt": "2021-07-23T10:45:00",
    "last_payment_date_gmt": "",
    "cancelled_date_gmt": "",
    "end_date_gmt": "",
    "resubscribed_from": "",
    "resubscribed_subscription": "",
    "removed_line_items": [],
    "_links": {
        "self": [
            {
                "href": "https://example.com/wp-json/wc/v3/subscriptions/1313"
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
```

## Retrieve a subscription ##

This API retrieves a specific subscription.

### HTTP request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-get">GET</i>
		<h6>/wp-json/wc/v3/subscriptions/&lt;id&gt;</h6>
	</div>
</div>

```shell
curl https://example.com/wp-json/wc/v3/subscriptions/1300 \
	-u consumer_key:consumer_secret
```

```javascript
WooCommerce.get('subscriptions/1300', function(err, data, res) {
  console.log(res);
});
```

```php
<?php print_r($woocommerce->get('subscriptions/1300')); ?>
```

```python
print(wcapi.get("subscriptions/1300").json())
```

```ruby
woocommerce.get("subscriptions/1300").parsed_response
```

> JSON response example:

```json
{
    "id": 1300,
    "parent_id": 1299,
    "status": "active",
    "currency": "USD",
    "version": "5.2.0",
    "prices_include_tax": true,
    "date_created": "2021-04-22T20:44:41",
    "date_modified": "2021-04-22T20:47:58",
    "discount_total": "0.00",
    "discount_tax": "0.00",
    "shipping_total": "10.00",
    "shipping_tax": "0.00",
    "cart_tax": "4.74",
    "total": "32.65",
    "total_tax": "4.74",
    "customer_id": 1,
    "order_key": "wc_order_lDWPiAmVoaBRL",
    "billing": {
        "first_name": "James",
        "last_name": "Allan",
        "company": "",
        "address_1": "1 Main Road",
        "address_2": "",
        "city": "Brisbane",
        "state": "QLD",
        "postcode": "4000",
        "country": "AU",
        "email": "james.allan@automattic.com",
        "phone": "0000000000"
    },
    "shipping": {
        "first_name": "James",
        "last_name": "Allan",
        "company": "",
        "address_1": "1 Main Road",
        "address_2": "",
        "city": "Brisbane",
        "state": "QLD",
        "postcode": "4000",
        "country": "AU"
    },
    "payment_method": "stripe",
    "payment_method_title": "Credit Card (Stripe)",
    "customer_ip_address": "",
    "customer_user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 11_2_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.128 Safari/537.36",
    "created_via": "checkout",
    "customer_note": "",
    "date_completed": null,
    "date_paid": "2021-04-22T20:44:45",
    "number": "1300",
    "meta_data": [
        {
            "id": 53158,
            "key": "is_vat_exempt",
            "value": "no"
        },
        {
            "id": 53178,
            "key": "_stripe_customer_id",
            "value": "cus_xxxxxx"
        },
        {
            "id": 53179,
            "key": "_stripe_source_id",
            "value": "src_xxxxxx"
        }
    ],
    "line_items": [
        {
            "id": 1648,
            "name": "Weekly",
            "product_id": 1027,
            "variation_id": 0,
            "quantity": 1,
            "tax_class": "",
            "subtotal": "7.91",
            "subtotal_tax": "2.09",
            "total": "7.91",
            "total_tax": "2.09",
            "taxes": [
                {
                    "id": 3,
                    "total": "0.790514",
                    "subtotal": "0.790514"
                },
                {
                    "id": 4,
                    "total": "1.304348",
                    "subtotal": "1.304348"
                }
            ],
            "meta_data": [],
            "sku": "",
            "price": 7.905138,
            "parent_name": null
        }
    ],
    "tax_lines": [
        {
            "id": 1649,
            "rate_code": "AU-GST-2",
            "rate_id": 3,
            "label": "GST",
            "compound": true,
            "tax_total": "1.79",
            "shipping_tax_total": "0.00",
            "rate_percent": 10,
            "meta_data": []
        },
        {
            "id": 1650,
            "rate_code": "AU-QLD-TAX-3",
            "rate_id": 4,
            "label": "Tax",
            "compound": true,
            "tax_total": "2.95",
            "shipping_tax_total": "0.00",
            "rate_percent": 15,
            "meta_data": []
        }
    ],
    "shipping_lines": [
        {
            "id": 1647,
            "method_title": "Flat rate",
            "method_id": "flat_rate",
            "instance_id": "2",
            "total": "10.00",
            "total_tax": "0.00",
            "taxes": [
                {
                    "id": 3,
                    "total": "",
                    "subtotal": ""
                },
                {
                    "id": 4,
                    "total": "",
                    "subtotal": ""
                }
            ],
            "meta_data": [
                {
                    "id": 13309,
                    "key": "Items",
                    "value": "Weekly &times; 1",
                    "display_key": "Items",
                    "display_value": "Weekly &times; 1"
                }
            ]
        }
    ],
    "fee_lines": [
        {
            "id": 1652,
            "name": "Express",
            "tax_class": "",
            "tax_status": "taxable",
            "amount": "10",
            "total": "10.00",
            "total_tax": "2.65",
            "taxes": [
                {
                    "id": 3,
                    "total": "1",
                    "subtotal": ""
                },
                {
                    "id": 4,
                    "total": "1.65",
                    "subtotal": ""
                }
            ],
            "meta_data": []
        }
    ],
    "coupon_lines": [],
    "date_created_gmt": "2021-04-22T10:44:41",
    "date_modified_gmt": "2021-04-22T10:47:58",
    "date_completed_gmt": null,
    "date_paid_gmt": "2021-04-22T10:44:45",
    "billing_period": "week",
    "billing_interval": "1",
    "start_date_gmt": "2021-04-22T10:44:41",
    "trial_end_date_gmt": "",
    "next_payment_date_gmt": "2021-04-29T10:44:41",
    "last_payment_date_gmt": "2021-04-22T10:44:41",
    "cancelled_date_gmt": "",
    "end_date_gmt": "",
    "resubscribed_from": "",
    "resubscribed_subscription": "",
    "removed_line_items": [],
    "_links": {
        "self": [
            {
                "href": "https://example.com/wp-json/wc/v3/subscriptions/1300"
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
        ],
        "up": [
            {
                "href": "https://example.com/wp-json/wc/v3/orders/1299"
            }
        ]
    }
}
```

#### Available parameters ####

| Parameter |  Type  |                    Description                    |
|-----------|--------|---------------------------------------------------|
| `dp`      | string | Number of decimal points to use in each resource. |

## List all subscriptions ##

This API retreives all the subscriptions.

### HTTP request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-get">GET</i>
		<h6>/wp-json/wc/v3/subscriptions</h6>
	</div>
</div>

```shell
curl https://example.com/wp-json/wc/v3/subscriptions \
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
        "id": 1314,
        "parent_id": 0,
        "status": "pending",
        "currency": "USD",
        "version": "5.2.0",
        "prices_include_tax": true,
        "date_created": "2021-04-23T17:22:22",
        "date_modified": "2021-04-23T17:24:34",
        "discount_total": "0.00",
        "discount_tax": "0.00",
        "shipping_total": "0.00",
        "shipping_tax": "0.00",
        "cart_tax": "6.32",
        "total": "69.56",
        "total_tax": "6.32",
        "customer_id": 3,
        "order_key": "wc_order_vYhjmTsexB6rH",
        "billing": {
            "first_name": "Jane",
            "last_name": "Doe",
            "company": "",
            "address_1": "10 Main Rd",
            "address_2": "",
            "city": "Brisbane",
            "state": "QLD",
            "postcode": "4000",
            "country": "AU",
            "email": "jane-doe@example.com",
            "phone": "0000000000"
        },
        "shipping": {
            "first_name": "Jane",
            "last_name": "Doe",
            "company": "",
            "address_1": "10 Main Rd",
            "address_2": "",
            "city": "Brisbane",
            "state": "QLD",
            "postcode": "4000",
            "country": "AU"
        },
        "payment_method": "",
        "payment_method_title": "",
        "customer_ip_address": "",
        "customer_user_agent": "",
        "created_via": "",
        "customer_note": "",
        "date_completed": null,
        "date_paid": null,
        "number": "1314",
        "meta_data": [
            {
                "id": 53835,
                "key": "_stripe_source_id",
                "value": ""
            }
        ],
        "line_items": [
            {
                "id": 1689,
                "name": "Subscription",
                "product_id": 1035,
                "variation_id": 0,
                "quantity": 1,
                "tax_class": "",
                "subtotal": "63.24",
                "subtotal_tax": "6.32",
                "total": "63.24",
                "total_tax": "6.32",
                "taxes": [
                    {
                        "id": 3,
                        "total": "6.324111",
                        "subtotal": "6.324111"
                    }
                ],
                "meta_data": [],
                "sku": "",
                "price": 63.241106000000002,
                "parent_name": null
            }
        ],
        "tax_lines": [
            {
                "id": 1690,
                "rate_code": "AU-GST-2",
                "rate_id": 3,
                "label": "GST",
                "compound": true,
                "tax_total": "6.32",
                "shipping_tax_total": "0.00",
                "rate_percent": 10,
                "meta_data": []
            }
        ],
        "shipping_lines": [],
        "fee_lines": [],
        "coupon_lines": [],
        "date_created_gmt": "2021-04-23T07:22:22",
        "date_modified_gmt": "2021-04-23T07:24:34",
        "date_completed_gmt": null,
        "date_paid_gmt": null,
        "billing_period": "day",
        "billing_interval": "1",
        "start_date_gmt": "2021-04-23T07:21:00",
        "trial_end_date_gmt": "",
        "next_payment_date_gmt": "",
        "last_payment_date_gmt": "",
        "cancelled_date_gmt": "",
        "end_date_gmt": "",
        "resubscribed_from": "",
        "resubscribed_subscription": "",
        "removed_line_items": [],
        "_links": {
            "self": [
                {
                    "href": "https://example.com/wp-json/wc/v3/subscriptions/1314"
                }
            ],
            "collection": [
                {
                    "href": "https://xample.com/wp-json/wc/v3/subscriptions"
                }
            ],
            "customer": [
                {
                    "href": "https://example.com/wp-json/wc/v3/customers/3"
                }
            ]
        }
    },
    {
        "id": 1313,
        "parent_id": 0,
        "status": "active",
        "currency": "USD",
        "version": "5.2.0",
        "prices_include_tax": true,
        "date_created": "2021-04-23T16:38:41",
        "date_modified": "2021-04-23T16:38:41",
        "discount_total": "0.00",
        "discount_tax": "0.00",
        "shipping_total": "10.00",
        "shipping_tax": "0.00",
        "cart_tax": "16.60",
        "total": "192.61",
        "total_tax": "16.60",
        "customer_id": 1,
        "order_key": "wc_order_lyCT6s4CE82cP",
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
        "payment_method_title": "Credit Card (Stripe)",
        "customer_ip_address": "",
        "customer_user_agent": "",
        "created_via": "rest-api",
        "customer_note": "",
        "date_completed": null,
        "date_paid": null,
        "number": "1313",
        "meta_data": [
            {
                "id": 53824,
                "key": "_custom_subscription_meta",
                "value": "custom meta"
            },
            {
                "id": 53825,
                "key": "_stripe_customer_id",
                "value": "cus_Yjw4cyvPHBFzc8"
            },
            {
                "id": 53826,
                "key": "_stripe_source_id",
                "value": "src_BSFD2kaYChDBtg2tP5qn7R3E"
            }
        ],
        "line_items": [
            {
                "id": 1685,
                "name": "Yearly",
                "product_id": 1175,
                "variation_id": 0,
                "quantity": 2,
                "tax_class": "",
                "subtotal": "126.48",
                "subtotal_tax": "12.65",
                "total": "126.48",
                "total_tax": "12.65",
                "taxes": [
                    {
                        "id": 2,
                        "total": "12.648221",
                        "subtotal": "12.648221"
                    }
                ],
                "meta_data": [],
                "sku": "",
                "price": 63.241107,
                "parent_name": null
            },
            {
                "id": 1686,
                "name": "Variable Subscription - Small",
                "product_id": 633,
                "variation_id": 636,
                "quantity": 1,
                "tax_class": "",
                "subtotal": "39.53",
                "subtotal_tax": "3.95",
                "total": "39.53",
                "total_tax": "3.95",
                "taxes": [
                    {
                        "id": 2,
                        "total": "3.952569",
                        "subtotal": "3.952569"
                    }
                ],
                "meta_data": [
                    {
                        "id": 13607,
                        "key": "pa_size",
                        "value": "small",
                        "display_key": "Size",
                        "display_value": "Small"
                    }
                ],
                "sku": "",
                "price": 39.525691999999999,
                "parent_name": "Variable Subscription"
            }
        ],
        "tax_lines": [
            {
                "id": 1688,
                "rate_code": "US-TAX-1",
                "rate_id": 2,
                "label": "TAX",
                "compound": true,
                "tax_total": "16.60",
                "shipping_tax_total": "0.00",
                "rate_percent": 10,
                "meta_data": []
            }
        ],
        "shipping_lines": [
            {
                "id": 1687,
                "method_title": "Flat Rate",
                "method_id": "flat_rate",
                "instance_id": "",
                "total": "10.00",
                "total_tax": "0.00",
                "taxes": [],
                "meta_data": []
            }
        ],
        "fee_lines": [],
        "coupon_lines": [],
        "date_created_gmt": "2021-04-23T06:38:41",
        "date_modified_gmt": "2021-04-23T06:38:41",
        "date_completed_gmt": null,
        "date_paid_gmt": null,
        "billing_period": "month",
        "billing_interval": "3",
        "start_date_gmt": "2021-04-23T10:45:00",
        "trial_end_date_gmt": "",
        "next_payment_date_gmt": "2021-07-23T10:45:00",
        "last_payment_date_gmt": "",
        "cancelled_date_gmt": "",
        "end_date_gmt": "",
        "resubscribed_from": "",
        "resubscribed_subscription": "",
        "removed_line_items": [],
        "_links": {
            "self": [
                {
                    "href": "https://example.com/wp-json/wc/v3/subscriptions/1313"
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
        "id": 1312,
        "parent_id": 0,
        "status": "pending",
        "currency": "USD",
        "version": "5.2.0",
        "prices_include_tax": false,
        "date_created": "2021-04-23T15:41:47",
        "date_modified": "2021-04-23T15:41:47",
        "discount_total": "0.00",
        "discount_tax": "0.00",
        "shipping_total": "0.00",
        "shipping_tax": "0.00",
        "cart_tax": "0.00",
        "total": "0.00",
        "total_tax": "0.00",
        "customer_id": 1,
        "order_key": "wc_order_5Us6R9XndaBRA",
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
        "payment_method": "",
        "payment_method_title": "",
        "customer_ip_address": "",
        "customer_user_agent": "",
        "created_via": "",
        "customer_note": "",
        "date_completed": null,
        "date_paid": null,
        "number": "1312",
        "meta_data": [
            {
                "id": 53775,
                "key": "_custom_subscription_meta",
                "value": "custom meta"
            },
            {
                "id": 53776,
                "key": "_stripe_customer_id",
                "value": "cus_Yjw4cyvPHBFzc8"
            },
            {
                "id": 53777,
                "key": "_stripe_source_id",
                "value": "src_BSFD2kaYChDBtg2tP5qn7R3E"
            }
        ],
        "line_items": [
            {
                "id": 1682,
                "name": "Yearly",
                "product_id": 1175,
                "variation_id": 0,
                "quantity": 2,
                "tax_class": "",
                "subtotal": "126.48",
                "subtotal_tax": "0.00",
                "total": "126.48",
                "total_tax": "0.00",
                "taxes": [],
                "meta_data": [],
                "sku": "",
                "price": 63.241107,
                "parent_name": null
            },
            {
                "id": 1683,
                "name": "Variable Subscription - Small",
                "product_id": 633,
                "variation_id": 636,
                "quantity": 1,
                "tax_class": "",
                "subtotal": "39.53",
                "subtotal_tax": "0.00",
                "total": "39.53",
                "total_tax": "0.00",
                "taxes": [],
                "meta_data": [
                    {
                        "id": 13583,
                        "key": "pa_size",
                        "value": "small",
                        "display_key": "Size",
                        "display_value": "Small"
                    }
                ],
                "sku": "",
                "price": 39.525691999999999,
                "parent_name": "Variable Subscription"
            }
        ],
        "tax_lines": [],
        "shipping_lines": [
            {
                "id": 1684,
                "method_title": "Flat Rate",
                "method_id": "flat_rate",
                "instance_id": "",
                "total": "10.00",
                "total_tax": "0.00",
                "taxes": [],
                "meta_data": []
            }
        ],
        "fee_lines": [],
        "coupon_lines": [],
        "date_created_gmt": "2021-04-23T05:41:47",
        "date_modified_gmt": "2021-04-23T05:41:47",
        "date_completed_gmt": null,
        "date_paid_gmt": null,
        "billing_period": "month",
        "billing_interval": "3",
        "start_date_gmt": "2021-04-23T05:41:47",
        "trial_end_date_gmt": "",
        "next_payment_date_gmt": "",
        "last_payment_date_gmt": "",
        "cancelled_date_gmt": "",
        "end_date_gmt": "",
        "resubscribed_from": "",
        "resubscribed_subscription": "",
        "removed_line_items": [],
        "_links": {
            "self": [
                {
                    "href": "https://example.com/wp-json/wc/v3/subscriptions/1312"
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
        "id": 1311,
        "parent_id": 0,
        "status": "active",
        "currency": "USD",
        "version": "5.2.0",
        "prices_include_tax": true,
        "date_created": "2021-04-23T15:02:42",
        "date_modified": "2021-04-23T15:02:42",
        "discount_total": "0.00",
        "discount_tax": "0.00",
        "shipping_total": "10.00",
        "shipping_tax": "0.00",
        "cart_tax": "16.60",
        "total": "192.61",
        "total_tax": "16.60",
        "customer_id": 1,
        "order_key": "wc_order_sjJYONc6eMdua",
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
        "payment_method_title": "Credit Card (Stripe)",
        "customer_ip_address": "",
        "customer_user_agent": "",
        "created_via": "rest-api",
        "customer_note": "",
        "date_completed": null,
        "date_paid": null,
        "number": "1311",
        "meta_data": [
            {
                "id": 53724,
                "key": "_custom_subscription_meta",
                "value": "custom meta"
            },
            {
                "id": 53725,
                "key": "_stripe_customer_id",
                "value": "cus_Yjw4cyvPHBFzc8"
            },
            {
                "id": 53726,
                "key": "_stripe_source_id",
                "value": "src_BSFD2kaYChDBtg2tP5qn7R3E"
            }
        ],
        "line_items": [
            {
                "id": 1678,
                "name": "Yearly",
                "product_id": 1175,
                "variation_id": 0,
                "quantity": 2,
                "tax_class": "",
                "subtotal": "126.48",
                "subtotal_tax": "12.65",
                "total": "126.48",
                "total_tax": "12.65",
                "taxes": [
                    {
                        "id": 2,
                        "total": "12.648221",
                        "subtotal": "12.648221"
                    }
                ],
                "meta_data": [],
                "sku": "",
                "price": 63.241107,
                "parent_name": null
            },
            {
                "id": 1679,
                "name": "Variable Subscription - Small",
                "product_id": 633,
                "variation_id": 636,
                "quantity": 1,
                "tax_class": "",
                "subtotal": "39.53",
                "subtotal_tax": "3.95",
                "total": "39.53",
                "total_tax": "3.95",
                "taxes": [
                    {
                        "id": 2,
                        "total": "3.952569",
                        "subtotal": "3.952569"
                    }
                ],
                "meta_data": [
                    {
                        "id": 13553,
                        "key": "pa_size",
                        "value": "small",
                        "display_key": "Size",
                        "display_value": "Small"
                    }
                ],
                "sku": "",
                "price": 39.525691999999999,
                "parent_name": "Variable Subscription"
            }
        ],
        "tax_lines": [
            {
                "id": 1681,
                "rate_code": "US-TAX-1",
                "rate_id": 2,
                "label": "TAX",
                "compound": true,
                "tax_total": "16.60",
                "shipping_tax_total": "0.00",
                "rate_percent": 10,
                "meta_data": []
            }
        ],
        "shipping_lines": [
            {
                "id": 1680,
                "method_title": "Flat Rate",
                "method_id": "flat_rate",
                "instance_id": "",
                "total": "10.00",
                "total_tax": "0.00",
                "taxes": [],
                "meta_data": []
            }
        ],
        "fee_lines": [],
        "coupon_lines": [],
        "date_created_gmt": "2021-04-23T05:02:42",
        "date_modified_gmt": "2021-04-23T05:02:42",
        "date_completed_gmt": null,
        "date_paid_gmt": null,
        "billing_period": "month",
        "billing_interval": "3",
        "start_date_gmt": "2021-04-23T10:45:00",
        "trial_end_date_gmt": "",
        "next_payment_date_gmt": "2021-07-23T10:45:00",
        "last_payment_date_gmt": "",
        "cancelled_date_gmt": "",
        "end_date_gmt": "",
        "resubscribed_from": "",
        "resubscribed_subscription": "",
        "removed_line_items": [],
        "_links": {
            "self": [
                {
                    "href": "https://example.com/wp-json/wc/v3/subscriptions/1311"
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

#### Available parameters ####

|    Parameter     |   Type  |                                                                                                 Description                                                                                                  |
|------------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `context`        | string  | Scope under which the request is made; determines fields present in response. Options: `view` and `edit`. Default is `view`.                                                                                 |
| `page`           | integer | Current page of the collection. Default is 1.                                                                                                                                                                |
| `per_page`       | integer | Maximum number of items to be returned in result set. Default is 10.                                                                                                                                         |
| `search`         | string  | Limit results to those matching a string.                                                                                                                                                                    |
| `after`          | string  | Limit response to resources published after a given ISO8601 compliant date.                                                                                                                                  |
| `before`         | string  | Limit response to resources published before a given ISO8601 compliant date.                                                                                                                                 |
| `exclude`        | string  | Ensure result set excludes specific IDs.                                                                                                                                                                     |
| `include`        | string  | Limit result set to specific IDs.                                                                                                                                                                            |
| `offset`         | integer | Offset the result set by a specific number of items.                                                                                                                                                         |
| `order`          | string  | Order sort attribute ascending or descending. Options: `asc` and `desc`. Default is `desc`.                                                                                                                  |
| `orderby`        | string  | Sort collection by object attribute. Options: `date`, `id`, `include`, `title` and `slug`. Default is `date`.                                                                                                |
| `parent`         | array   | Limit result set to those of particular parent IDs.                                                                                                                                                          |
| `parent_exclude` | array   | Limit result set to all items except those of a particular parent ID.                                                                                                                                        |
| `status`         | string  | Limit result set to subscriptions assigned a specific status. Default is `any`. Options (plugins may add new status): `any`, `pending`, `on-hold`, `active`, `cancelled`, `pending-cancel` and `expired`.    |
| `customer`       | string  | Limit result set to subscriptions assigned a specific customer ID.                                                                                                                                              |
| `product`        | string  | Limit result set to subscriptions assigned a specific product ID.                                                                                                                                               |
| `dp`             | string  | Number of decimal points to return values in.                                                                                                                                                                |

## Update a subscription ##

This API updates a subscription.

### HTTP Request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-put">PUT</i>
		<h6>/wp-json/wc/v3/subscriptions/&lt;id&gt;</h6>
	</div>
</div>

```shell
curl -X PUT https://example.com/wp-json/wc/v3/subscriptions/30 \
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

WooCommerce.put('subscriptions/1246', data, function(err, data, res) {
  console.log(res);
});
```

```php
<?php
$data = [
    'status' => 'on-hold'
];

print_r($woocommerce->put('subscriptions/1246', $data));
?>
```

```python
data = {
    "status": "on-hold"
}

print(wcapi.put("subscriptions/1246", data).json())
```

```ruby
data = {
  status: "on-hold"
}

woocommerce.put("subscriptions/1246", data).parsed_response
```

> JSON response example:

```json
{
    "id": 1246,
    "parent_id": 1245,
    "status": "on-hold",
    "currency": "USD",
    "version": "5.2.0",
    "prices_include_tax": true,
    "date_created": "2021-04-16T13:54:52",
    "date_modified": "2021-04-23T17:49:23",
    "discount_total": "3.24",
    "discount_tax": "0.32",
    "shipping_total": "0.00",
    "shipping_tax": "0.00",
    "cart_tax": "2.10",
    "total": "23.13",
    "total_tax": "2.10",
    "customer_id": 1,
    "order_key": "wc_order_Cf9ANTFb5GOun",
    "billing": {
        "first_name": "John",
        "last_name": "Doe",
        "company": "",
        "address_1": "1 Main Rd",
        "address_2": "",
        "city": "Brisbame",
        "state": "QLD",
        "postcode": "4000",
        "country": "AU",
        "email": "john@example.com",
        "phone": "0000000000"
    },
    "shipping": {
        "first_name": "John",
        "last_name": "Doe",
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
    "customer_ip_address": "",
    "customer_user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 11_2_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36",
    "created_via": "checkout",
    "customer_note": "",
    "date_completed": null,
    "date_paid": "2021-04-16T13:54:56",
    "number": "1246",
    "meta_data": [
        {
            "id": 50628,
            "key": "is_vat_exempt",
            "value": "no"
        },
        {
            "id": 50648,
            "key": "_stripe_customer_id",
            "value": "cus_XtEynWZ4SWRUXm"
        },
        {
            "id": 50649,
            "key": "_stripe_source_id",
            "value": "src_XE3xLw39fq4Ck7c2h8RgaQ25"
        }
    ],
    "line_items": [
        {
            "id": 1532,
            "name": "Monthly",
            "product_id": 916,
            "variation_id": 0,
            "quantity": 2,
            "tax_class": "",
            "subtotal": "24.27",
            "subtotal_tax": "2.43",
            "total": "21.03",
            "total_tax": "2.10",
            "taxes": [
                {
                    "id": 3,
                    "total": "2.102727",
                    "subtotal": "2.427273"
                }
            ],
            "meta_data": [],
            "sku": "",
            "price": 10.5136365,
            "parent_name": null
        }
    ],
    "tax_lines": [
        {
            "id": 1533,
            "rate_code": "AU-GST-2",
            "rate_id": 3,
            "label": "GST",
            "compound": true,
            "tax_total": "2.10",
            "shipping_tax_total": "0.00",
            "rate_percent": 10,
            "meta_data": []
        }
    ],
    "shipping_lines": [
        {
            "id": 1531,
            "method_title": "Free shipping",
            "method_id": "free_shipping",
            "instance_id": "4",
            "total": "0.00",
            "total_tax": "0.00",
            "taxes": [
                {
                    "id": 3,
                    "total": "",
                    "subtotal": ""
                }
            ],
            "meta_data": [
                {
                    "id": 12423,
                    "key": "Items",
                    "value": "Monthly &times; 2",
                    "display_key": "Items",
                    "display_value": "Monthly &times; 2"
                }
            ]
        }
    ],
    "fee_lines": [],
    "coupon_lines": [
        {
            "id": 1534,
            "code": "13%off",
            "discount": "3.25",
            "discount_tax": "0.32",
            "meta_data": [
                {
                    "id": 12441,
                    "key": "coupon_data",
                    "value": {
                        "id": 917,
                        "code": "13%off",
                        "amount": "13.36",
                        "date_created": {
                            "date": "2021-03-18 01:26:41.000000",
                            "timezone_type": 1,
                            "timezone": "+00:00"
                        },
                        "date_modified": {
                            "date": "2021-03-18 01:30:46.000000",
                            "timezone_type": 1,
                            "timezone": "+00:00"
                        },
                        "date_expires": null,
                        "discount_type": "recurring_percent",
                        "description": "",
                        "usage_count": 11,
                        "individual_use": false,
                        "product_ids": [],
                        "excluded_product_ids": [],
                        "usage_limit": 0,
                        "usage_limit_per_user": 0,
                        "limit_usage_to_x_items": null,
                        "free_shipping": false,
                        "product_categories": [],
                        "excluded_product_categories": [],
                        "exclude_sale_items": false,
                        "minimum_amount": "",
                        "maximum_amount": "",
                        "email_restrictions": [],
                        "virtual": false,
                        "meta_data": [
                            {
                                "id": 36451,
                                "key": "_wcs_number_payments",
                                "value": ""
                            }
                        ]
                    },
                    "display_key": "coupon_data",
                    "display_value": {
                        "id": 917,
                        "code": "13%off",
                        "amount": "13.36",
                        "date_created": {
                            "date": "2021-03-18 01:26:41.000000",
                            "timezone_type": 1,
                            "timezone": "+00:00"
                        },
                        "date_modified": {
                            "date": "2021-03-18 01:30:46.000000",
                            "timezone_type": 1,
                            "timezone": "+00:00"
                        },
                        "date_expires": null,
                        "discount_type": "recurring_percent",
                        "description": "",
                        "usage_count": 11,
                        "individual_use": false,
                        "product_ids": [],
                        "excluded_product_ids": [],
                        "usage_limit": 0,
                        "usage_limit_per_user": 0,
                        "limit_usage_to_x_items": null,
                        "free_shipping": false,
                        "product_categories": [],
                        "excluded_product_categories": [],
                        "exclude_sale_items": false,
                        "minimum_amount": "",
                        "maximum_amount": "",
                        "email_restrictions": [],
                        "virtual": false,
                        "meta_data": [
                            {
                                "id": 36451,
                                "key": "_wcs_number_payments",
                                "value": ""
                            }
                        ]
                    }
                }
            ]
        }
    ],
    "date_created_gmt": "2021-04-16T03:54:52",
    "date_modified_gmt": "2021-04-23T07:49:23",
    "date_completed_gmt": null,
    "date_paid_gmt": "2021-04-16T03:54:56",
    "billing_period": "month",
    "billing_interval": "1",
    "start_date_gmt": "2021-04-23T07:49:23",
    "trial_end_date_gmt": "",
    "next_payment_date_gmt": "2021-05-16T03:54:51",
    "last_payment_date_gmt": "2021-04-16T03:54:51",
    "cancelled_date_gmt": "",
    "end_date_gmt": "",
    "resubscribed_from": "",
    "resubscribed_subscription": "",
    "removed_line_items": [],
    "_links": {
        "self": [
            {
                "href": "https://example.com/wp-json/wc/v3/subscriptions/1246"
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
        ],
        "up": [
            {
                "href": "https://example.com/wp-json/wc/v3/orders/1245"
            }
        ]
    }
}
```

## Delete a subscription ##

This API deletes a subscription.

### HTTP request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-delete">DELETE</i>
		<h6>/wp-json/wc/v3/subscriptions/&lt;id&gt;</h6>
	</div>
</div>

```shell
curl -X DELETE https://example.com/wp-json/wc/v3/subscriptions/1313?force=true \
	-u consumer_key:consumer_secret
```

```javascript
WooCommerce.delete('subscriptions/1313?force=true', function(err, data, res) {
  console.log(res);
});
```

```php
<?php print_r($woocommerce->delete('subscriptions/1313', ['force' => true])); ?>
```

```python
print(wcapi.delete("subscriptions/1313?force=true").json())
```

```ruby
woocommerce.delete("subscriptions/1313", force: true).parsed_response
```

> JSON response example:

```json
{
    "id": 1313,
    "parent_id": 0,
    "status": "active",
    "currency": "USD",
    "version": "5.2.0",
    "prices_include_tax": true,
    "date_created": "2021-04-23T16:38:41",
    "date_modified": "2021-04-23T16:38:41",
    "discount_total": "0.00",
    "discount_tax": "0.00",
    "shipping_total": "10.00",
    "shipping_tax": "0.00",
    "cart_tax": "16.60",
    "total": "192.61",
    "total_tax": "16.60",
    "customer_id": 1,
    "order_key": "wc_order_lyCT6s4CE82cP",
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
    "payment_method_title": "Credit Card (Stripe)",
    "customer_ip_address": "",
    "customer_user_agent": "",
    "created_via": "rest-api",
    "customer_note": "",
    "date_completed": null,
    "date_paid": null,
    "number": "1313",
    "meta_data": [
        {
            "id": 53824,
            "key": "_custom_subscription_meta",
            "value": "custom meta"
        },
        {
            "id": 53825,
            "key": "_stripe_customer_id",
            "value": "cus_Yjw4cyvPHBFzc8"
        },
        {
            "id": 53826,
            "key": "_stripe_source_id",
            "value": "src_BSFD2kaYChDBtg2tP5qn7R3E"
        }
    ],
    "line_items": [
        {
            "id": 1685,
            "name": "Yearly",
            "product_id": 1175,
            "variation_id": 0,
            "quantity": 2,
            "tax_class": "",
            "subtotal": "126.48",
            "subtotal_tax": "12.65",
            "total": "126.48",
            "total_tax": "12.65",
            "taxes": [
                {
                    "id": 2,
                    "total": "12.648221",
                    "subtotal": "12.648221"
                }
            ],
            "meta_data": [],
            "sku": "",
            "price": 63.241107,
            "parent_name": null
        },
        {
            "id": 1686,
            "name": "Variable Subscription - Small",
            "product_id": 633,
            "variation_id": 636,
            "quantity": 1,
            "tax_class": "",
            "subtotal": "39.53",
            "subtotal_tax": "3.95",
            "total": "39.53",
            "total_tax": "3.95",
            "taxes": [
                {
                    "id": 2,
                    "total": "3.952569",
                    "subtotal": "3.952569"
                }
            ],
            "meta_data": [
                {
                    "id": 13607,
                    "key": "pa_size",
                    "value": "small",
                    "display_key": "Size",
                    "display_value": "Small"
                }
            ],
            "sku": "",
            "price": 39.525691999999999,
            "parent_name": "Variable Subscription"
        }
    ],
    "tax_lines": [
        {
            "id": 1688,
            "rate_code": "US-TAX-1",
            "rate_id": 2,
            "label": "TAX",
            "compound": true,
            "tax_total": "16.60",
            "shipping_tax_total": "0.00",
            "rate_percent": 10,
            "meta_data": []
        }
    ],
    "shipping_lines": [
        {
            "id": 1687,
            "method_title": "Flat Rate",
            "method_id": "flat_rate",
            "instance_id": "",
            "total": "10.00",
            "total_tax": "0.00",
            "taxes": [],
            "meta_data": []
        }
    ],
    "fee_lines": [],
    "coupon_lines": [],
    "date_created_gmt": "2021-04-23T06:38:41",
    "date_modified_gmt": "2021-04-23T06:38:41",
    "date_completed_gmt": null,
    "date_paid_gmt": null,
    "billing_period": "month",
    "billing_interval": "3",
    "start_date_gmt": "2021-04-23T10:45:00",
    "trial_end_date_gmt": "",
    "next_payment_date_gmt": "2021-07-23T10:45:00",
    "last_payment_date_gmt": "",
    "cancelled_date_gmt": "",
    "end_date_gmt": "",
    "resubscribed_from": "",
    "resubscribed_subscription": "",
    "removed_line_items": [],
    "_links": {
        "self": [
            {
                "href": "https://example.com/wp-json/wc/v3/subscriptions/1313"
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
```

#### Available parameters ####

| Parameter |  Type  |                                  Description                                   |
|-----------|--------|--------------------------------------------------------------------------------|
| `force`   | string | Use `true` to permanently delete the subscription. Default is `false`.         |

## Batch update subscriptions ##

This API can batch create, update and delete multiple subscriptions.

### HTTP request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-post">POST</i>
		<h6>/wp-json/wc/v3/subscriptions/batch</h6>
	</div>
</div>

```shell
curl -X POST https://example.com/wp-json/wc/v3/subscriptions/batch \
    -u consumer_key:consumer_secret \
    -H "Content-Type: application/json" \
    -d '{
  {
  "create": [
    {
      "customer_id": 1,
      "billing_interval": 1,
      "billing_period": "month",
      "payment_method": "bacs",
      "payment_method_title": "Direct Bank Transfer",
      "billing": {
        "first_name": "Jane",
        "last_name": "Doe",
        "address_1": "969 Market",
        "address_2": "",
        "city": "San Francisco",
        "state": "CA",
        "postcode": "94103",
        "country": "US",
        "email": "jane.doe@example.com",
        "phone": "(555) 555-5555"
      },
      "shipping": {
        "first_name": "Jane",
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
          "product_id": 1175,
          "quantity": 2
        },
        {
          "product_id": 1030,
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
      "customer_id": 3,
      "billing_interval": 1,
      "billing_period": "day",
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
          "product_id": 1026,
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
      "id": 1212,
      "status": "active"
    },
    {
      "id": 1355,
      "status": "on-hold"
    },
    {
      "id": 1347,
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
      }
    }
  ],
  "delete": [
    1345
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
        first_name: 'Jane',
        last_name: 'Doe',
        address_1: '969 Market',
        address_2: '',
        city: 'San Francisco',
        state: 'CA',
        postcode: '94103',
        country: 'US',
        email: 'jane.doe@example.com',
        phone: '(555) 555-5555'
      },
      shipping: {
        first_name: 'Jane',
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
          product_id: 1175,
          quantity: 2
        },
        {
          product_id: 1030,
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
      customer_id: 3,
      billing_interval: 1,
      billing_period: 'day',
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
          product_id: 1026,
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
      id: 1212,
      status: 'active'
    },
    {
      id: 1355,
      status: 'on-hold'
    },
    {
      id: 1347,
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
      }
    }
  ],
  delete: [
    1345
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
            'customer_id' => 1,
            'billing_interval' => 1,
            'billing_period' => 'month',
            'payment_method' => 'bacs',
            'payment_method_title' => 'Direct Bank Transfer',
            'billing' => [
                'first_name' => 'Jane',
                'last_name' => 'Doe',
                'address_1' => '969 Market',
                'address_2' => '',
                'city' => 'San Francisco',
                'state' => 'CA',
                'postcode' => '94103',
                'country' => 'US',
                'email' => 'jane.doe@example.com',
                'phone' => '(555) 555-5555'
            ],
            'shipping' => [
                'first_name' => 'Jane',
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
                    'product_id' => 1175,
                    'quantity' => 2
                ],
                [
                    'product_id' => 1030,
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
            'customer_id' => 3,
            'billing_interval' => 1,
            'billing_period' => 'day',
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
                    'product_id' => 1026,
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
            'id' => 1212,
            'status' => 'active'
        ],
        [
            'id' => 1355,
            'status' => 'on-hold'
        ],
        [
            'id' => 1347,
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
            ]
        ]
    ],
    'delete' => [
        1345
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
                "first_name": "Jane",
                "last_name": "Doe",
                "address_1": "969 Market",
                "address_2": "",
                "city": "San Francisco",
                "state": "CA",
                "postcode": "94103",
                "country": "US",
                "email": "jane.doe@example.com",
                "phone": "(555) 555-5555"
            },
            "shipping": {
                "first_name": "Jane",
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
                    "product_id": 1175,
                    "quantity": 2
                },
                {
                    "product_id": 1030,
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
            "customer_id": 3,
            "billing_interval": 1,
            "billing_period": "day",
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
                    "product_id": 1026,
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
            "id": 1212,
            "status": "active"
        },
        {
            "id": 1355,
            "status": "on-hold"
        },
        {
            "id": 1347,
            "billing": [
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
            ]
        }
    ],
    "delete": [
        1345
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
        first_name: "Jane",
        last_name: "Doe",
        address_1: "969 Market",
        address_2: "",
        city: "San Francisco",
        state: "CA",
        postcode: "94103",
        country: "US",
        email: "jane.doe@example.com",
        phone: "(555) 555-5555"
      },
      shipping: {
        first_name: "Jane",
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
          product_id: 1175,
          quantity: 2
        },
        {
          product_id: 1030,
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
      customer_id: 3,
      billing_interval: 1,
      billing_period: "day",
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
          product_id: 1026,
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
      id: 1212,
      status: "active"
    }
    {
      id: 1355,
      status: "on-hold"
    },
    {
      id: 1347,
      billing: [
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
        ]
    }
  ],
  delete: [
    1345
  ]
}

woocommerce.post("subscriptions/batch", data).parsed_response
```

> JSON response example:

```json
{
    "create": [
        {
            "id": 1357,
            "parent_id": 0,
            "status": "pending",
            "currency": "USD",
            "version": "5.2.0",
            "prices_include_tax": true,
            "date_created": "2021-04-29T14:48:33",
            "date_modified": "2021-04-29T14:48:33",
            "discount_total": "0.00",
            "discount_tax": "0.00",
            "shipping_total": "30.00",
            "shipping_tax": "0.00",
            "cart_tax": "14.63",
            "total": "190.87",
            "total_tax": "14.63",
            "customer_id": 1,
            "order_key": "wc_order_G7ImClNBd9f6N",
            "billing": {
                "first_name": "Jane",
                "last_name": "Doe",
                "company": "",
                "address_1": "969 Market",
                "address_2": "",
                "city": "San Francisco",
                "state": "CA",
                "postcode": "94103",
                "country": "US",
                "email": "jane.doe@example.com",
                "phone": "(555) 555-5555"
            },
            "shipping": {
                "first_name": "Jane",
                "last_name": "Doe",
                "company": "",
                "address_1": "969 Market",
                "address_2": "",
                "city": "San Francisco",
                "state": "CA",
                "postcode": "94103",
                "country": "US"
            },
            "payment_method": "bacs",
            "payment_method_title": "Direct bank transfer",
            "customer_ip_address": "",
            "customer_user_agent": "",
            "created_via": "rest-api",
            "customer_note": "",
            "date_completed": null,
            "date_paid": null,
            "number": "1357",
            "meta_data": [],
            "line_items": [
                {
                    "id": 1791,
                    "name": "Yearly",
                    "product_id": 1175,
                    "variation_id": 0,
                    "quantity": 2,
                    "tax_class": "",
                    "subtotal": "126.48",
                    "subtotal_tax": "12.65",
                    "total": "126.48",
                    "total_tax": "12.65",
                    "taxes": [
                        {
                            "id": 2,
                            "total": "12.648221",
                            "subtotal": "12.648221"
                        }
                    ],
                    "meta_data": [],
                    "sku": "",
                    "price": 63.241107,
                    "parent_name": null
                },
                {
                    "id": 1792,
                    "name": "Weekly  2",
                    "product_id": 1030,
                    "variation_id": 0,
                    "quantity": 1,
                    "tax_class": "",
                    "subtotal": "19.76",
                    "subtotal_tax": "1.98",
                    "total": "19.76",
                    "total_tax": "1.98",
                    "taxes": [
                        {
                            "id": 2,
                            "total": "1.976285",
                            "subtotal": "1.976285"
                        }
                    ],
                    "meta_data": [],
                    "sku": "",
                    "price": 19.762844999999999,
                    "parent_name": null
                }
            ],
            "tax_lines": [
                {
                    "id": 1794,
                    "rate_code": "US-TAX-1",
                    "rate_id": 2,
                    "label": "TAX",
                    "compound": true,
                    "tax_total": "14.63",
                    "shipping_tax_total": "0.00",
                    "rate_percent": 10,
                    "meta_data": []
                }
            ],
            "shipping_lines": [
                {
                    "id": 1793,
                    "method_title": "Flat Rate",
                    "method_id": "flat_rate",
                    "instance_id": "",
                    "total": "30.00",
                    "total_tax": "0.00",
                    "taxes": [],
                    "meta_data": []
                }
            ],
            "fee_lines": [],
            "coupon_lines": [],
            "date_created_gmt": "2021-04-29T04:48:33",
            "date_modified_gmt": "2021-04-29T04:48:33",
            "date_completed_gmt": null,
            "date_paid_gmt": null,
            "billing_period": "month",
            "billing_interval": "1",
            "start_date_gmt": "2021-04-29T04:48:33",
            "trial_end_date_gmt": "",
            "next_payment_date_gmt": "",
            "last_payment_date_gmt": "",
            "cancelled_date_gmt": "",
            "end_date_gmt": "",
            "resubscribed_from": "",
            "resubscribed_subscription": "",
            "removed_line_items": [],
            "_links": {
                "self": [
                    {
                        "href": "https://example/wp-json/wc/v3/subscriptions/1357"
                    }
                ],
                "collection": [
                    {
                        "href": "https://example/wp-json/wc/v3/subscriptions"
                    }
                ],
                "customer": [
                    {
                        "href": "https://example/wp-json/wc/v3/customers/1"
                    }
                ]
            }
        },
        {
            "id": 1358,
            "parent_id": 0,
            "status": "pending",
            "currency": "USD",
            "version": "5.2.0",
            "prices_include_tax": true,
            "date_created": "2021-04-29T14:48:33",
            "date_modified": "2021-04-29T14:48:33",
            "discount_total": "0.00",
            "discount_tax": "0.00",
            "shipping_total": "20.00",
            "shipping_tax": "0.00",
            "cart_tax": "0.79",
            "total": "28.70",
            "total_tax": "0.79",
            "customer_id": 3,
            "order_key": "wc_order_wBr74T1upRJlL",
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
            "payment_method": "bacs",
            "payment_method_title": "Direct bank transfer",
            "customer_ip_address": "",
            "customer_user_agent": "",
            "created_via": "rest-api",
            "customer_note": "",
            "date_completed": null,
            "date_paid": null,
            "number": "1358",
            "meta_data": [],
            "line_items": [
                {
                    "id": 1795,
                    "name": "Daily",
                    "product_id": 1026,
                    "variation_id": 0,
                    "quantity": 2,
                    "tax_class": "",
                    "subtotal": "7.91",
                    "subtotal_tax": "0.79",
                    "total": "7.91",
                    "total_tax": "0.79",
                    "taxes": [
                        {
                            "id": 2,
                            "total": "0.790514",
                            "subtotal": "0.790514"
                        }
                    ],
                    "meta_data": [],
                    "sku": "",
                    "price": 3.952569,
                    "parent_name": null
                }
            ],
            "tax_lines": [
                {
                    "id": 1797,
                    "rate_code": "US-TAX-1",
                    "rate_id": 2,
                    "label": "TAX",
                    "compound": true,
                    "tax_total": "0.79",
                    "shipping_tax_total": "0.00",
                    "rate_percent": 10,
                    "meta_data": []
                }
            ],
            "shipping_lines": [
                {
                    "id": 1796,
                    "method_title": "Flat Rate",
                    "method_id": "flat_rate",
                    "instance_id": "",
                    "total": "20.00",
                    "total_tax": "0.00",
                    "taxes": [],
                    "meta_data": []
                }
            ],
            "fee_lines": [],
            "coupon_lines": [],
            "date_created_gmt": "2021-04-29T04:48:33",
            "date_modified_gmt": "2021-04-29T04:48:33",
            "date_completed_gmt": null,
            "date_paid_gmt": null,
            "billing_period": "day",
            "billing_interval": "1",
            "start_date_gmt": "2021-04-29T04:48:33",
            "trial_end_date_gmt": "",
            "next_payment_date_gmt": "",
            "last_payment_date_gmt": "",
            "cancelled_date_gmt": "",
            "end_date_gmt": "",
            "resubscribed_from": "",
            "resubscribed_subscription": "",
            "removed_line_items": [],
            "_links": {
                "self": [
                    {
                        "href": "https://example/wp-json/wc/v3/subscriptions/1358"
                    }
                ],
                "collection": [
                    {
                        "href": "https://example/wp-json/wc/v3/subscriptions"
                    }
                ],
                "customer": [
                    {
                        "href": "https://example/wp-json/wc/v3/customers/3"
                    }
                ]
            }
        }
    ],
    "update": [
        {
            "id": 1212,
            "parent_id": 1211,
            "status": "active",
            "currency": "USD",
            "version": "5.2.0",
            "prices_include_tax": true,
            "date_created": "2021-04-15T17:06:37",
            "date_modified": "2021-04-29T14:48:33",
            "discount_total": "0.00",
            "discount_tax": "0.00",
            "shipping_total": "0.00",
            "shipping_tax": "0.00",
            "cart_tax": "4.09",
            "total": "45.00",
            "total_tax": "4.09",
            "customer_id": 1,
            "order_key": "wc_order_kqNFp1kS5iGgG",
            "billing": {
                "first_name": "James",
                "last_name": "Allan",
                "company": "Automattic",
                "address_1": "1",
                "address_2": "",
                "city": "LA",
                "state": "QLD",
                "postcode": "4006",
                "country": "AU",
                "email": "james.allan@automattic.com",
                "phone": "0400000000"
            },
            "shipping": {
                "first_name": "James",
                "last_name": "Allan",
                "company": "Automattic",
                "address_1": "1",
                "address_2": "",
                "city": "LA",
                "state": "QLD",
                "postcode": "4006",
                "country": "AU"
            },
            "payment_method": "stripe",
            "payment_method_title": "Credit Card (Stripe)",
            "customer_ip_address": "127.0.0.1",
            "customer_user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 11_2_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36",
            "created_via": "checkout",
            "customer_note": "",
            "date_completed": null,
            "date_paid": "2021-04-15T17:06:38",
            "number": "1212",
            "meta_data": [
                {
                    "id": 49220,
                    "key": "is_vat_exempt",
                    "value": "no"
                },
                {
                    "id": 49240,
                    "key": "_stripe_customer_id",
                    "value": "cus_ITzwp55rw7z3uI"
                },
                {
                    "id": 49241,
                    "key": "_stripe_source_id",
                    "value": "src_1Ht1x0IoMdrH5jqSwNmHvYGs"
                },
                {
                    "id": 49250,
                    "key": "end_date_pre_cancellation",
                    "value": "0"
                },
                {
                    "id": 49251,
                    "key": "trial_end_pre_cancellation",
                    "value": "2021-06-15 07:06:36"
                }
            ],
            "line_items": [
                {
                    "id": 1452,
                    "name": "Yearly - free trial",
                    "product_id": 1032,
                    "variation_id": 0,
                    "quantity": 1,
                    "tax_class": "",
                    "subtotal": "40.91",
                    "subtotal_tax": "4.09",
                    "total": "40.91",
                    "total_tax": "4.09",
                    "taxes": [
                        {
                            "id": 3,
                            "total": "4.090909",
                            "subtotal": "4.090909"
                        }
                    ],
                    "meta_data": [
                        {
                            "id": 11903,
                            "key": "_has_trial",
                            "value": "true",
                            "display_key": "_has_trial",
                            "display_value": "true"
                        }
                    ],
                    "sku": "",
                    "price": 40.909090999999997,
                    "parent_name": null
                }
            ],
            "tax_lines": [
                {
                    "id": 1453,
                    "rate_code": "AU-GST-2",
                    "rate_id": 3,
                    "label": "GST",
                    "compound": true,
                    "tax_total": "4.09",
                    "shipping_tax_total": "0.00",
                    "rate_percent": 10,
                    "meta_data": []
                }
            ],
            "shipping_lines": [
                {
                    "id": 1451,
                    "method_title": "Free shipping",
                    "method_id": "free_shipping",
                    "instance_id": "4",
                    "total": "0.00",
                    "total_tax": "0.00",
                    "taxes": [],
                    "meta_data": [
                        {
                            "id": 11893,
                            "key": "Items",
                            "value": "Yearly - free trial &times; 1",
                            "display_key": "Items",
                            "display_value": "Yearly - free trial &times; 1"
                        }
                    ]
                }
            ],
            "fee_lines": [],
            "coupon_lines": [],
            "date_created_gmt": "2021-04-15T07:06:37",
            "date_modified_gmt": "2021-04-29T04:48:33",
            "date_completed_gmt": null,
            "date_paid_gmt": "2021-04-15T07:06:38",
            "billing_period": "year",
            "billing_interval": "1",
            "start_date_gmt": "2021-04-29T04:48:33",
            "trial_end_date_gmt": "",
            "next_payment_date_gmt": "",
            "last_payment_date_gmt": "2021-04-15T07:06:36",
            "cancelled_date_gmt": "2021-04-15T07:07:17",
            "end_date_gmt": "2021-04-15T07:07:23",
            "resubscribed_from": "",
            "resubscribed_subscription": "",
            "removed_line_items": [],
            "_links": {
                "self": [
                    {
                        "href": "https://example/wp-json/wc/v3/subscriptions/1212"
                    }
                ],
                "collection": [
                    {
                        "href": "https://example/wp-json/wc/v3/subscriptions"
                    }
                ],
                "customer": [
                    {
                        "href": "https://example/wp-json/wc/v3/customers/1"
                    }
                ],
                "up": [
                    {
                        "href": "https://example/wp-json/wc/v3/orders/1211"
                    }
                ]
            }
        },
        {
            "id": 1355,
            "parent_id": 0,
            "status": "on-hold",
            "currency": "USD",
            "version": "5.2.0",
            "prices_include_tax": true,
            "date_created": "2021-04-29T14:44:57",
            "date_modified": "2021-04-29T14:48:33",
            "discount_total": "0.00",
            "discount_tax": "0.00",
            "shipping_total": "20.00",
            "shipping_tax": "0.00",
            "cart_tax": "0.79",
            "total": "28.70",
            "total_tax": "0.79",
            "customer_id": 3,
            "order_key": "wc_order_sMwcVPqcUEjgr",
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
            "payment_method": "bacs",
            "payment_method_title": "Direct bank transfer",
            "customer_ip_address": "",
            "customer_user_agent": "",
            "created_via": "rest-api",
            "customer_note": "",
            "date_completed": null,
            "date_paid": null,
            "number": "1355",
            "meta_data": [],
            "line_items": [
                {
                    "id": 1786,
                    "name": "Daily",
                    "product_id": 1026,
                    "variation_id": 0,
                    "quantity": 2,
                    "tax_class": "",
                    "subtotal": "7.91",
                    "subtotal_tax": "0.79",
                    "total": "7.91",
                    "total_tax": "0.79",
                    "taxes": [
                        {
                            "id": 2,
                            "total": "0.790514",
                            "subtotal": "0.790514"
                        }
                    ],
                    "meta_data": [],
                    "sku": "",
                    "price": 3.952569,
                    "parent_name": null
                }
            ],
            "tax_lines": [
                {
                    "id": 1788,
                    "rate_code": "US-TAX-1",
                    "rate_id": 2,
                    "label": "TAX",
                    "compound": true,
                    "tax_total": "0.79",
                    "shipping_tax_total": "0.00",
                    "rate_percent": 10,
                    "meta_data": []
                }
            ],
            "shipping_lines": [
                {
                    "id": 1787,
                    "method_title": "Flat Rate",
                    "method_id": "flat_rate",
                    "instance_id": "",
                    "total": "20.00",
                    "total_tax": "0.00",
                    "taxes": [],
                    "meta_data": []
                }
            ],
            "fee_lines": [],
            "coupon_lines": [],
            "date_created_gmt": "2021-04-29T04:44:57",
            "date_modified_gmt": "2021-04-29T04:48:33",
            "date_completed_gmt": null,
            "date_paid_gmt": null,
            "billing_period": "day",
            "billing_interval": "1",
            "start_date_gmt": "2021-04-29T04:48:33",
            "trial_end_date_gmt": "",
            "next_payment_date_gmt": "2021-04-30T04:44:57",
            "last_payment_date_gmt": "",
            "cancelled_date_gmt": "",
            "end_date_gmt": "",
            "resubscribed_from": "",
            "resubscribed_subscription": "",
            "removed_line_items": [],
            "_links": {
                "self": [
                    {
                        "href": "https://example/wp-json/wc/v3/subscriptions/1355"
                    }
                ],
                "collection": [
                    {
                        "href": "https://example/wp-json/wc/v3/subscriptions"
                    }
                ],
                "customer": [
                    {
                        "href": "https://example/wp-json/wc/v3/customers/3"
                    }
                ]
            }
        },
        {
            "id": 1347,
            "parent_id": 0,
            "status": "active",
            "currency": "USD",
            "version": "5.2.0",
            "prices_include_tax": true,
            "date_created": "2021-04-29T14:25:56",
            "date_modified": "2021-04-29T14:25:56",
            "discount_total": "0.00",
            "discount_tax": "0.00",
            "shipping_total": "20.00",
            "shipping_tax": "0.00",
            "cart_tax": "0.79",
            "total": "28.70",
            "total_tax": "0.79",
            "customer_id": 3,
            "order_key": "wc_order_4ylc4ZcUX30cg",
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
            "payment_method": "bacs",
            "payment_method_title": "Direct bank transfer",
            "customer_ip_address": "",
            "customer_user_agent": "",
            "created_via": "rest-api",
            "customer_note": "",
            "date_completed": null,
            "date_paid": null,
            "number": "1347",
            "meta_data": [],
            "line_items": [
                {
                    "id": 1758,
                    "name": "Daily",
                    "product_id": 1026,
                    "variation_id": 0,
                    "quantity": 2,
                    "tax_class": "",
                    "subtotal": "7.91",
                    "subtotal_tax": "0.79",
                    "total": "7.91",
                    "total_tax": "0.79",
                    "taxes": [
                        {
                            "id": 2,
                            "total": "0.790514",
                            "subtotal": "0.790514"
                        }
                    ],
                    "meta_data": [],
                    "sku": "",
                    "price": 3.952569,
                    "parent_name": null
                }
            ],
            "tax_lines": [
                {
                    "id": 1760,
                    "rate_code": "US-TAX-1",
                    "rate_id": 2,
                    "label": "TAX",
                    "compound": true,
                    "tax_total": "0.79",
                    "shipping_tax_total": "0.00",
                    "rate_percent": 10,
                    "meta_data": []
                }
            ],
            "shipping_lines": [
                {
                    "id": 1759,
                    "method_title": "Flat Rate",
                    "method_id": "flat_rate",
                    "instance_id": "",
                    "total": "20.00",
                    "total_tax": "0.00",
                    "taxes": [],
                    "meta_data": []
                }
            ],
            "fee_lines": [],
            "coupon_lines": [],
            "date_created_gmt": "2021-04-29T04:25:56",
            "date_modified_gmt": "2021-04-29T04:25:56",
            "date_completed_gmt": null,
            "date_paid_gmt": null,
            "billing_period": "day",
            "billing_interval": "1",
            "start_date_gmt": "2021-04-29T04:48:33",
            "trial_end_date_gmt": "",
            "next_payment_date_gmt": "2021-04-30T04:25:56",
            "last_payment_date_gmt": "",
            "cancelled_date_gmt": "",
            "end_date_gmt": "",
            "resubscribed_from": "",
            "resubscribed_subscription": "",
            "removed_line_items": [],
            "_links": {
                "self": [
                    {
                        "href": "https://example/wp-json/wc/v3/subscriptions/1347"
                    }
                ],
                "collection": [
                    {
                        "href": "https://example/wp-json/wc/v3/subscriptions"
                    }
                ],
                "customer": [
                    {
                        "href": "https://example/wp-json/wc/v3/customers/3"
                    }
                ]
            }
        }
    ],
    "delete": [
        {
            "id": 1345,
            "parent_id": 0,
            "status": "active",
            "currency": "USD",
            "version": "5.2.0",
            "prices_include_tax": true,
            "date_created": "2021-04-29T14:25:48",
            "date_modified": "2021-04-29T14:25:48",
            "discount_total": "0.00",
            "discount_tax": "0.00",
            "shipping_total": "20.00",
            "shipping_tax": "0.00",
            "cart_tax": "0.79",
            "total": "28.70",
            "total_tax": "0.79",
            "customer_id": 3,
            "order_key": "wc_order_3JB8p2ejr7Jz8",
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
            "payment_method": "bacs",
            "payment_method_title": "Direct bank transfer",
            "customer_ip_address": "",
            "customer_user_agent": "",
            "created_via": "rest-api",
            "customer_note": "",
            "date_completed": null,
            "date_paid": null,
            "number": "1345",
            "meta_data": [],
            "line_items": [
                {
                    "id": 1751,
                    "name": "Daily",
                    "product_id": 1026,
                    "variation_id": 0,
                    "quantity": 2,
                    "tax_class": "",
                    "subtotal": "7.91",
                    "subtotal_tax": "0.79",
                    "total": "7.91",
                    "total_tax": "0.79",
                    "taxes": [
                        {
                            "id": 2,
                            "total": "0.790514",
                            "subtotal": "0.790514"
                        }
                    ],
                    "meta_data": [],
                    "sku": "",
                    "price": 3.952569,
                    "parent_name": null
                }
            ],
            "tax_lines": [
                {
                    "id": 1753,
                    "rate_code": "US-TAX-1",
                    "rate_id": 2,
                    "label": "TAX",
                    "compound": true,
                    "tax_total": "0.79",
                    "shipping_tax_total": "0.00",
                    "rate_percent": 10,
                    "meta_data": []
                }
            ],
            "shipping_lines": [
                {
                    "id": 1752,
                    "method_title": "Flat Rate",
                    "method_id": "flat_rate",
                    "instance_id": "",
                    "total": "20.00",
                    "total_tax": "0.00",
                    "taxes": [],
                    "meta_data": []
                }
            ],
            "fee_lines": [],
            "coupon_lines": [],
            "date_created_gmt": "2021-04-29T04:25:48",
            "date_modified_gmt": "2021-04-29T04:25:48",
            "date_completed_gmt": null,
            "date_paid_gmt": null,
            "billing_period": "day",
            "billing_interval": "1",
            "start_date_gmt": "2021-04-29T04:25:48",
            "trial_end_date_gmt": "",
            "next_payment_date_gmt": "2021-04-30T04:25:48",
            "last_payment_date_gmt": "",
            "cancelled_date_gmt": "",
            "end_date_gmt": "",
            "resubscribed_from": "",
            "resubscribed_subscription": "",
            "removed_line_items": [],
            "_links": {
                "self": [
                    {
                        "href": "https://example/wp-json/wc/v3/subscriptions/1345"
                    }
                ],
                "collection": [
                    {
                        "href": "https://example/wp-json/wc/v3/subscriptions"
                    }
                ],
                "customer": [
                    {
                        "href": "https://example/wp-json/wc/v3/customers/3"
                    }
                ]
            }
        }
    ]
}
```

## Get statuses ##

This API returns all available subscription statuses.

### HTTP request ###

<div class="api-endpoint">
  <div class="endpoint-data">
    <i class="label label-delete">GET</i>
    <h6>/wp-json/wc/v3/subscriptions/statuses</h6>
  </div>
</div>

```shell
curl -k https://example.com/wp-json/wc/v3/subscriptions/statuses
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
