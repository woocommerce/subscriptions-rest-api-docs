# Subscriptions #

This section lists all API that can be used to create, edit or otherwise manipulate subscriptions.

## Subscription Properties ##
|          Attribute          |   Type  |                                                                                                Description                                                                                                |
| --------------------------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                        | integer | Subscription ID (post ID) <i class="label label-info">read-only</i>                                                                                                                                       |
| `order_number`              | integer | Order number <i class="label label-info">read-only</i>                                                                                                                                                    |
| `created_at`                | string  | UTC DateTime when the order was created <i class="label label-info">read-only</i>                                                                                                                         |
| `updated_at`                | string  | UTC DateTime when the order was last updated <i class="label label-info">read-only</i>                                                                                                                    |
| `completed_at`              | string  | UTC DateTime when the order was last completed <i class="label label-info">read-only</i>                                                                                                                  |
| `start_date`                | string  | UTC DateTime for the subscription start date.                                                                                                                                                             |
| `next_payment_date`         | string  | UTC DateTime for the subscriptions next payment date.                                                                                                                                                     |
| `trial_end_date`            | string  | UTC DateTime for the subscriptions trial end date.                                                                                                                                                        |
| `end_date`                  | string  | UTC DateTime for the subscription end date.                                                                                                                                                               |
| `status`                    | string  | Subscription status. By default the statuses available are: `pending`, `on-hold`, `active`, `pending-cancel`, `cancelled` and `expired`. See [View List of Subscription Statuses](#view-list-of-subscription-statuses) |
| `billing_period`            | string  | Billing period for the subscription. By default, valid billing periods are: `day`, `week`, `month`, `year`. See [View List of Subscription Periods](#view-list-of-subscription-periods)                   |
| `billing_interval`          | integer | The number of billing periods between each payment cycle.                                                                                                                                                 |
| `currency`                  | string  | Currency in ISO format, e.g `USD`                                                                                                                                                                         |
| `total`                     | float   | Order total <i class="label label-info">read-only</i>                                                                                                                                                     |
| `subtotal`                  | float   | Order subtotal <i class="label label-info">read-only</i>                                                                                                                                                  |
| `total_line_items_quantity` | integer | Total of order items <i class="label label-info">read-only</i>                                                                                                                                            |
| `total_tax`                 | float   | Order tax total <i class="label label-info">read-only</i>                                                                                                                                                 |
| `total_shipping`            | float   | Order shipping total <i class="label label-info">read-only</i>                                                                                                                                            |
| `cart_tax`                  | float   | Order cart tax <i class="label label-info">read-only</i>                                                                                                                                                  |
| `shipping_tax`              | float   | Order shipping tax <i class="label label-info">read-only</i>                                                                                                                                              |
| `total_discount`            | float   | Order total discount <i class="label label-info">read-only</i>                                                                                                                                            |
| `shipping_methods`          | string  | Text list of the shipping methods used in the order <i class="label label-info">read-only</i>                                                                                                             |
| `payment_details`           | array   | List of payment details. See [Payment Details Properties](#payment-details-properties)                                                                                                                    |
| `billing_address`           | array   | List of customer billing address. See [Customer Billing Address Properties](#billing-address-properties)                                                                                                  |
| `shipping_address`          | array   | List of customer shipping address. See [Customer Shipping Address Properties](#shipping-address-properties)                                                                                               |
| `note`                      | string  | Customer subscription notes                                                                                                                                                                                      |
| `customer_ip`               | string  | Customer IP address <i class="label label-info">read-only</i>                                                                                                                                             |
| `customer_user_agent`       | string  | Customer User-Agent <i class="label label-info">read-only</i>                                                                                                                                             |
| `customer_id`               | integer | Customer ID (user ID) <i class="label label-info">required</i>                                                                                                                                            |
| `view_order_url`            | string  | URL to view the subscription in frontend <i class="label label-info">read-only</i>                                                                                                                               |
| `line_items`                | array   | List of order line items. See [Line Items Properties](#line-items-properties)                                                                                                                             |
| `shipping_lines`            | array   | List of shipping line items. See [Shipping Lines Properties](#shipping-lines-properties)                                                                                                                  |
| `tax_lines`                 | array   | List of tax line items. See [Tax Lines Properties](#tax-lines-properties) <i class="label label-info">read-only</i>                                                                                       |
| `fee_lines`                 | array   | List of fee line items. See [Fee Lines Properites](#fee-lines-properites)                                                                                                                                 |
| `coupon_lines`              | array   | List of cupon line items. See [Coupon Lines Properties](#coupon-lines-properties)                                                                                                                         |
| `customer`                  | array   | Customer data. See [Customer Properties](#customers-properties)                                                                                                                                           |

### Payment Details Properties ###

|    Attribute     |   Type  |                                                               Description                                                                |
| ---------------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| `method_id`      | string  | Payment method ID <i class="label label-info">required</i>                                                                               |
| `method_title`   | string  | Payment method title <i class="label label-info">required</i>                                                                            |
| `transaction_id` | string  | Transaction ID, an optional field to set the transacion ID when complate one payment (to set this you need set the `paid` as `true` too) |

Payment method meta specific to the `method_id` can also be given in [Payment Details](#payment-details-properties) to support recurring payments on the subscription.

### Line Items Properties ###

|   Attribute    |   Type  |                                                                                         Description                                                                                         |
| -------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`           | integer | Line item ID <i class="label label-info">read-only</i>                                                                                                                                      |
| `subtotal`     | float   | Line item subtotal                                                                                                                                                                          |
| `subtotal_tax` | float   | Line item tax subtotal                                                                                                                                                                      |
| `total`        | float   | Line item total                                                                                                                                                                             |
| `total_tax`    | float   | Line item tax total                                                                                                                                                                         |
| `price`        | float   | Product price <i class="label label-info">read-only</i>                                                                                                                                     |
| `quantity`     | integer | Quantity                                                                                                                                                                                    |
| `tax_class`    | string  | Product tax class <i class="label label-info">read-only</i>                                                                                                                                 |
| `name`         | string  | Product name <i class="label label-info">read-only</i>                                                                                                                                      |
| `product_id`   | integer | Product ID <i class="label label-info">required</i>. This value _does not_ need to be a subscription product.                                                                                                                                          |
| `sku`          | string  | Product SKU <i class="label label-info">read-only</i>                                                                                                                                       |
| `meta`         | array   | List of product meta items. See [Products Meta Items Properties](#products-meta-items-properties)                                                                                           |
| `variations`   | array   | List of product variation attributes. e.g: `"variation": {"pa_color": "Black", "pa_size": "XGG"}` (Use `pa_` prefix when is a product attribute) <i class="label label-info">write-only</i> |

#### Products Meta Items Properties ####

| Attribute |  Type  |   Description   |
| --------- | ------ | --------------- |
| `key`     | string | Meta item key   |
| `label`   | string | Meta item label |
| `value`   | string | Meta item value |

### Shipping Lines Properties ###

|   Attribute    |   Type  |                          Description                           |
| -------------- | ------- | -------------------------------------------------------------- |
| `id`           | integer | Shipping line ID <i class="label label-info">read-only</i>     |
| `method_id`    | string  | Shipping method ID <i class="label label-info">required</i>    |
| `method_title` | string  | Shipping method title <i class="label label-info">required</i> |
| `total`        | float   | Total amount                                                   |

### Tax Lines Properties ###

| Attribute  |   Type  |                                                               Description                                                               |
| ---------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| `id`       | integer | Tax rate line ID <i class="label label-info">read-only</i>                                                                              |
| `rate_id`  | integer | Tax rate ID <i class="label label-info">read-only</i>                                                                                   |
| `code`     | string  | Tax rate code <i class="label label-info">read-only</i>                                                                                 |
| `title`    | string  | Tax rate title/name <i class="label label-info">read-only</i>                                                                           |
| `total`    | float   | Tax rate total <i class="label label-info">read-only</i>                                                                                |
| `compound` | boolean | Shows if is or not a compound rate. Compound tax rates are applied on top of other tax rates. <i class="label label-info">read-only</i> |

### Fee Lines Properites ###

|  Attribute  |   Type  |                                  Description                                  |
| ----------- | ------- | ----------------------------------------------------------------------------- |
| `id`        | integer | Fee line ID <i class="label label-info">read-only</i>                         |
| `title`     | string  | Shipping method title <i class="label label-info">required</i>                |
| `taxable`   | boolean | Shows/define if the fee is taxable <i class="label label-info">write-only</i> |
| `tax_class` | string  | Tax class, requered in write-mode if the fee is taxable                       |
| `total`     | float   | Total amount                                                                  |
| `total_tax` | float   | Tax total                                                                     |

### Coupon Lines Properties ###

| Attribute |   Type  |                       Description                        |
| --------- | ------- | -------------------------------------------------------- |
| `id`      | integer | Coupon line ID <i class="label label-info">read-only</i> |
| `code`    | string  | Coupon code <i class="label label-info">required</i>     |
| `amount`  | float   | Total amount <i class="label label-info">required</i>    |


## Create A Subscription ##

This API helps you to create a new subscription.

### HTTP Request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-post">POST</i>
		<h6>/wc-api/v3/subscriptions</h6>
	</div>
</div>

> Example to create a basic subscription:

```shell
curl -X POST https://example.com/wc-api/v3/subscriptions \
	-u consumer_key:consumer_secret \
	-H "Content-Type: application/json" \
	-d '{
  "subscription": {
    "billing_period": "month",
    "billing_interval": 1,
    "start_date": "2015-05-10 08:30:00",
    "next_payment_date": "2015-06-10 08:30:00",
    "payment_details": {
      "method_id": "stripe",
      "method_title": "Stripe (Credit Card)",
      "post_meta": {
        "_stripe_customer_id": "cus_T35TCU57M3R",
        "_stripe_card_id": "card_T35TC4RD"
      }
    },
    "billing_address": {
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
    "shipping_address": {
      "first_name": "John",
      "last_name": "Doe",
      "address_1": "969 Market",
      "address_2": "",
      "city": "San Francisco",
      "state": "CA",
      "postcode": "94103",
      "country": "US"
    },
    "customer_id": 2,
    "line_items": [
      {
        "product_id": 546,
        "quantity": 2
      },
      {
        "product_id": 613,
        "quantity": 1,
        "variations": {
          "pa_color": "Black"
        }
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
}'
```

```javascript
var data = {
  subscription: {
    billing_period: 'month',
    billing_interval: 1,
    start_date: '2015-05-10 08:30:00',
    next_payment_date: '2015-06-10 08:30:00',
    payment_details: {
      method_id: 'stripe',
      method_title: 'Stripe (Credit Card)',
        post_meta: {
          _stripe_customer_id: 'cus_T35TCU57M3R',
          _stripe_card_id: 'card_T35TC4RD'
        }
    },
    billing_address: {
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
    shipping_address: {
      first_name: 'John',
      last_name: 'Doe',
      address_1: '969 Market',
      address_2: '',
      city: 'San Francisco',
      state: 'CA',
      postcode: '94103',
      country: 'US'
    },
    customer_id: 2,
    line_items: [
      {
        product_id: 546,
        quantity: 2
      },
      {
        product_id: 613,
        quantity: 1,
        variations: {
          pa_color: 'Black'
        }
      }
    ],
    shipping_lines: [
      {
        method_id: 'flat_rate',
        method_title: 'Flat Rate',
        total: 10
      }
    ]
  }
};

WooCommerce.post('subscriptions', data, function(err, data, res) {
  console.log(res);
});
```

```python
data = {
    "subscription": {
        "billing_period": "month",
        "billing_interval": 1,
        "start_date": "2015-05-10 08:30:00",
        "next_payment_date": "2015-06-10 08:30:00",
        "payment_details": {
            "method_id": "stripe",
            "method_title": "Stripe (Credit Card)",
            "post_meta": {
                "_stripe_customer_id": "cus_T35TCU57M3R",
                "_stripe_card_id": "card_T35TC4RD"
            }
        },
        "billing_address": {
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
        "shipping_address": {
            "first_name": "John",
            "last_name": "Doe",
            "address_1": "969 Market",
            "address_2": "",
            "city": "San Francisco",
            "state": "CA",
            "postcode": "94103",
            "country": "US"
        },
        "customer_id": 2,
        "line_items": [
            {
                "product_id": 546,
                "quantity": 2
            },
            {
                "product_id": 613,
                "quantity": 1,
                "variations": {
                    "pa_color": "Black"
                }
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
}

print(wcapi.post("subscriptions", data).json())
```

```ruby
data = {
  subscription: {
    billing_period: "month",
    billing_interval: 1,
    start_date: "2015-05-10 08:30:00",
    next_payment_date: "2015-06-10 08:30:00",
    payment_details: {
        method_id: "stripe",
        method_title: "Stripe (Credit Card)",
        post_meta: {
            _stripe_customer_id: "cus_T35TCU57M3R",
            _stripe_card_id: "card_T35TC4RD"
        }
    },
    payment_details: {
      method_id: "bacs",
      method_title: "Direct Bank Transfer",
      paid: true
    },
    billing_address: {
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
    shipping_address: {
      first_name: "John",
      last_name: "Doe",
      address_1: "969 Market",
      address_2: "",
      city: "San Francisco",
      state: "CA",
      postcode: "94103",
      country: "US"
    },
    customer_id: 2,
    line_items: [
        {
          product_id: 546,
          quantity: 2
        },
        {
          product_id: 613,
          quantity: 1,
          variations: {
            pa_color: "Black"
          }
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
}

woocommerce.post("subscriptions", data).parsed_response
```

> JSON response example:

```json
{
"creating_subscription": {
    "subscription": {
      "id": 4923,
      "order_number": 4923,
      "created_at": "2015-10-21T02:28:42Z",
      "updated_at":"2015-10-21T02:28:42Z",
      "status": "active",
      "currency": "AUD",
      "total": "30.00",
      "subtotal": "20.00",
      "total_line_items_quantity" :2,
      "total_tax": "0.00",
      "total_shipping": "10.00",
      "cart_tax": "0.00",
      "shipping_tax": "0.00",
      "total_discount":"0.00",
      "shipping_methods": "Flat Rate",
      "payment_details": {
        "method_id": "stripe",
        "method_title":"Stripe (Credit Card)",
        "paid": false
      },
      "billing_address": {
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
      "shipping_address": {
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
      "note": "",
      "customer_ip": "",
      "customer_user_agent": "",
      "customer_id": 1,
      "view_order_url": "https:example.com\/my-account\/view-subscription\/4923",
      "line_items": [
        {
          "id": 7500,
          "subtotal": "20.00",
          "subtotal_tax": "0.00",
          "total": "20.00",
          "total_tax": "0.00",
          "price": "10.00",
          "quantity": 2,
          "tax_class": null,
          "name": "Monthly Membership &rarr; Bronze Subscription",
          "product_id": 2761,
          "sku": "",
          "meta":[]
         }
      ],
      "shipping_lines": [
        {
          "id": 7501,
          "method_id": "flat_rate",
          "method_title": "Flat Rate",
          "total": "10.00"
        }
      ],
      "tax_lines": [],
      "fee_lines": [],
      "coupon_lines": [],
      "customer": {
        "id": 1,
        "created_at": "2014-10-28T23:08:19Z",
        "email": "matt@prospress.com",
        "first_name": "Matthew",
        "last_name": "Allan",
        "username": "matt",
        "role": "administrator",
        "last_order_id": "4913",
        "last_order_date": "2015-10-20T06:57:36Z",
        "orders_count": 481,
        "total_spent": "6614.00",
        "avatar_url": "https:\/\/secure.gravatar.com\/avatar\/?s=96",
        "billing_address": {
          "first_name": "John",
          "last_name": "Doe",
          "company": "Prospress",
          "address_1": "969 Market",
          "address_2": "",
          "city": "San Francisco",
          "state": "CA",
          "postcode": "94103",
          "country": "US",
          "email": "john.doe@example.com",
          "phone": "(555) 555-5555"
        },
        "shipping_address": {
          "first_name": "John",
          "last_name": "Doe",
          "company": "Prospress",
          "address_1": "969 Market",
          "address_2": "",
          "city": "San Francisco",
          "state": "CA",
          "postcode": "94103",
          "country": "US"
        }
      },
      "billing_schedule": {
        "period":"month",
        "interval": "1",
        "start_at": "2015-10-21T02:28:42Z",
        "trial_end_at": "",
        "next_payment_at": "2015-06-10T08:30:00Z",
        "end_at": ""
      },
      "parent_order_id": []
    }
}
}
```

## View A Subscription ##

This API lets you retrieve and view a specific subscription.

### HTTP Request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-get">GET</i>
		<h6>/wc-api/v3/subscriptions/&lt;id&gt;</h6>
	</div>
</div>

```shell
curl https://example.com/wc-api/v3/subscriptions/4925 \
	-u consumer_key:consumer_secret
```

```javascript
WooCommerce.get('subscriptions/4925', function(err, data, res) {
  console.log(res);
});
```

```python
print(wcapi.get("subscriptions/4925").json())
```

```ruby
woocommerce.get("subscriptions/4925").parsed_response
```

> JSON response example:

```json
{
  "subscription": {
    "id": 4938,
    "order_number": 4938,
    "created_at": "2015-10-21T05:45:28Z",
    "updated_at": "2015-10-21T05:45:28Z",
    "status": "active",
    "currency": "AUD",
    "total": "36.00",
    "subtotal": "22.73",
    "total_line_items_quantity": 2,
    "total_tax": "3.27",
    "total_shipping": "10.00",
    "cart_tax": "2.27",
    "shipping_tax": "1.00",
    "total_discount": "0.00",
    "shipping_methods": "Flat Rate",
    "payment_details": {
      "method_id": "stripe",
      "method_title": "Credit card (Stripe)",
      "paid":false
    },
    "billing_address": {
      "first_name": "John",
      "last_name": "Doe",
      "company": "Prospress",
      "address_1": "969 Market",
      "address_2":"",
      "city":"San Francisco",
      "state":"CA",
      "postcode":"94103",
      "country":"US",
      "email":"john.doe@example.com",
      "phone":"(555) 555-5555"
    },
    "shipping_address": {
      "first_name":"John",
      "last_name": "Doe",
      "company": "Prospress",
      "address_1": "969 Market",
      "address_2": "",
      "city": "San Francisco",
      "state":"CA",
      "postcode": "94103",
      "country": "US"
    },
    "note": "",
    "customer_ip": "127.0.0.1",
    "customer_user_agent": "",
    "customer_id": 1,
    "view_order_url": "https://example.com/my-account/view-subscription/4938",
    "line_items": [
      {
        "id": 7529,
        "subtotal": "13.64",
        "subtotal_tax": "1.36",
        "total": "13.64",
        "total_tax": "1.36",
        "price": "13.64",
        "quantity": 1,
        "tax_class": null,
        "name": "Monthly Membership &rarr; Gold Membership",
        "product_id": 2102,
        "sku": "",
        "meta":[]
      },
      {
        "id":7530,
        "subtotal":"9.09",
        "subtotal_tax":"0.91",
        "total":"9.09",
        "total_tax":"0.91",
        "price":"9.09",
        "quantity":1,
        "tax_class":null,
        "name":"Colourful Subscription",
        "product_id":3456,
        "sku":"",
        "meta": [
          {
            "key":"pa_colour",
            "label":"Colour",
            "value":"Blue"
          }
        ]
      }
    ],
    "shipping_lines": [
      {
        "id":7531,
        "method_id":"flat_rate",
        "method_title":"Flat Rate",
        "total":"10.00"
      }
    ],
    "tax_lines": [
      {
        "id":7532,
        "rate_id":"3",
        "code":"TAX-1",
        "title":"Tax",
        "total":"3.27",
        "compound":false
      }
    ],
    "fee_lines":[],
    "coupon_lines":[],
    "customer":{
      "id":1,
      "created_at":"2014-10-28T23:08:19Z",
      "email":"matt@prospress.com",
      "first_name":"Matthew",
      "last_name":"Allan",
      "username":"matt",
      "role":"administrator",
      "last_order_id":"4937",
      "last_order_date":"2015-10-21T05:45:28Z",
      "orders_count":481,
      "total_spent":"6614.00",
      "avatar_url": "https://secure.gravatar.com/avatar/ad516503a11cd5ca435acc9bb6523536?s=96",
      "billing_address": {
        "first_name":"John",
        "last_name":"Doe",
        "company":"Prospress",
        "address_1":"969 Market",
        "address_2":"",
        "city":"San Francisco",
        "state":"CA",
        "postcode":"94103",
        "country":"US",
        "email":"john.doe@example.com",
        "phone":"(555) 555-5555"
      },
      "shipping_address": {
        "first_name":"John",
        "last_name":"Doe",
        "company":"Prospress",
        "address_1":"969 Market",
        "address_2":"",
        "city":"San Francisco",
        "state":"CA",
        "postcode":"94103",
        "country":"US"
      }
    },
    "billing_schedule": {
      "period":"month",
      "interval":"1",
      "start_at":"2015-10-21T05:45:28Z",
      "trial_end_at":"",
      "next_payment_at":"2015-11-21T05:45:26Z",
      "end_at":""
    },
    "parent_order_id":4937
  }
}
```

## View List Of Subscriptions ##

This API helps you to view all the subscriptions.

### HTTP Request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-get">GET</i>
		<h6>/wc-api/v3/subscriptions</h6>
	</div>
</div>

```shell
curl https://example.com/wc-api/v3/subscriptions \
	-u consumer_key:consumer_secret
```

```javascript
WooCommerce.get('subscriptions', function(err, data, res) {
  console.log(res);
});
```

```python
print(wcapi.get("subscriptions").json())
```

```ruby
woocommerce.get("subscriptions").parsed_response
```

> JSON response example:

```json
[SAME AS ABOVE JSON RESPONSE]
```

#### Available Filters ####

|  Filter  |  Type  |                    Description                    |
| -------- | ------ | ------------------------------------------------- |
| `status` | string | Subscriptions by status. eg: `active` or `on-hold`       |

## Update A Subscription ##

This API lets you make changes to an Subscription. All fields that can be changed via the API for an order can also be changed on a subscription; with the additional of a few extra fields.
billing_period, billing_interval, status, start/trial_end/next_payment/end dates can all be modified with this API endpoint

### HTTP Request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-put">PUT</i>
		<h6>/wc-api/v3/subscriptions/&lt;id&gt;</h6>
	</div>
</div>

#### Example: activate subscription and change start and end dates #####

```shell
curl -X PUT https://example.com/wc-api/v3/subscriptions/645 \
	-u consumer_key:consumer_secret \
	-H "Content-Type: application/json" \
	-d '{
  "subscription" : {
    "status": "active",
    "start_date":"2015-10-22 10:12:15",
    "end_date":"2016-10-22 10:12:15"
  }
}'
}'
```

```javascript
var data = {
  subscription = {
    status: 'active',
    start_date: '2015-10-22 10:12:15',
    end_date: '2016-10-22 10:12:15'
  }
};

WooCommerce.put('subscriptions/645', data, function(err, data, res) {
  console.log(res);
});
```

```python
data = {
    "subscription": {
        "status": "active",
        "start_date": "2015-10-22 10:12:15",
        "end_date": "2016-10-22 10:12:15"
    }
}

print(wcapi.put("subscriptions/645", data).json())
```

```ruby
data = {
  subscription: {
      status: "active",
      start_date: "2015-10-22 10:12:15",
      end_date: "2016-10-22 10:12:15"
  }
}

woocommerce.put("subscriptions/645", data).parsed_response
```

```json
[SAME AS ABOVE JSON RESPONSE]
```

## Get related orders for a Subscription ##

This API allows you to get all orders related to a given subscription. In other words,
this endpoint will get all renewal orders, initial orders and switch orders tied to a subscription and
return the orders objects in the same format as wc-api.

### HTTP Request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-get">GET</i>
		<h6>/wc-api/v3/subscriptions/&lt;id&gt;/orders</h6>
	</div>
</div>

```shell
curl https://example.com/wc-api/v3/subscriptions/5286/orders \
	-u consumer_key:consumer_secret
```

```javascript
WooCommerce.get('subscriptions/5286/orders', function(err, data, res) {
  console.log(res);
});
```

```python
print(wcapi.get("subscriptions/5286/orders").json())
```

```ruby
woocommerce.get("subscriptions/5286/orders").parsed_response
```

> JSON response example

```json
{
"subscription_orders": [
   {
     "order": {
       "id": 5288,
       "order_number": 5288,
       "created_at": "2015-11-04T06:21:09Z",
       "updated_at": "2015-11-04T06:21:09Z",
       "completed_at": "2015-11-04T06:21:09Z",
       "status": "processing",
       "currency": "AUD",
       "total": "25.00",
       "subtotal": "15.00",
       "total_line_items_quantity": 1,
       "total_tax": "0.00",
       "total_shipping": "10.00",
       "cart_tax": "0.00",
       "shipping_tax": "0.00",
       "total_discount": "0.00",
       "shipping_methods": "Flat Rate",
       "payment_details": {
          "method_id": "stripe",
          "method_title": "Credit card (Stripe)",
          "paid": true
       },
       "billing_address": {
          "first_name": "John",
          "last_name": "Doe",
          "company": "Prospress",
          "address_1": "969 Market",
          "address_2": "",
          "city": "San Francisco",
          "state": "CA",
          "postcode": "94103",
          "country": "US",
          "email": "john.doe@example.com",
          "phone": "(555) 555-5555"
       },
       "shipping_address": {
          "first_name": "John",
          "last_name": "Doe",
          "company": "Prospress",
          "address_1": "969 Market",
          "address_2": "",
          "city": "San Francisco",
          "state": "CA",
          "postcode": "94103",
          "country": "US"
       },
       "note": "",
       "customer_ip": "127.0.0.1",
       "customer_user_agent": "",
       "customer_id": 1,
       "view_order_url": "https://example.com/my-account/view-order/5288",
       "line_items": [
          {
            "id": 7882,
            "subtotal": "15.00",
            "subtotal_tax": "0.00",
            "total": "15.00",
            "total_tax": "0.00",
            "price": "15.00",
            "quantity": 1,
            "tax_class": null,
            "name": "Prospress Product",
            "product_id": 5052,
            "sku": "",
            "meta": []
          }
        ],
        "shipping_lines": [
          {
            "id": 7883,
            "method_id": "flat_rate",
            "method_title": "Flat Rate",
            "total": "10.00"
          }
        ],
        "tax_lines": [],
        "fee_lines": [],
        "coupon_lines": [],
        "customer": {
           "id": 1,
           "created_at": "2014-10-28T23:08:19Z",
           "email": "matt@prospress.com",
           "first_name": "Matthew",
           "last_name": "Allan",
           "username": "matt",
           "role": "administrator",
           "last_order_id": "7039",
           "last_order_date": "2015-11-04T06:21:09Z",
           "orders_count": 508,
           "total_spent": "6644.00",
           "avatar_url": "",
           "billing_address": {
              "first_name": "John",
              "last_name": "Doe",
              "company": "Prospress",
              "address_1": "969 Market",
              "address_2": "",
              "city": "San Francisco",
              "state": "CA",
              "postcode": "94103",
              "country": "US",
              "email": "john.doe@example.com",
              "phone": "(555) 555-5555"
           },
           "shipping_address": {
              "first_name": "John",
              "last_name": "Doe",
              "company": "Prospress",
              "address_1": "969 Market",
              "address_2": "",
              "city": "San Francisco",
              "state": "CA",
              "postcode": "94103",
              "country": "US"
          }
        }
     }
    },
    "order": {
       "id": 5285,
       "order_number": 5285,
       "created_at": "2015-11-04T06:21:09Z",
       "updated_at": "2015-11-04T06:21:09Z",
       "completed_at": "2015-11-04T06:21:09Z",
       "status": "processing",
       "currency": "AUD",
       "total": "25.00",
       "subtotal": "15.00",
       "total_line_items_quantity": 1,
       "total_tax": "0.00",
       "total_shipping": "10.00",
       "cart_tax": "0.00",
       "shipping_tax": "0.00",
       "total_discount": "0.00",
       "shipping_methods": "Flat Rate",
       "payment_details": {
          "method_id": "stripe",
          "method_title": "Credit card (Stripe)",
          "paid": true
       },
       "billing_address": {
          "first_name": "John",
          "last_name": "Doe",
          "company": "Prospress",
          "address_1": "969 Market",
          "address_2": "",
          "city": "San Francisco",
          "state": "CA",
          "postcode": "94103",
          "country": "US",
          "email": "john.doe@example.com",
          "phone": "(555) 555-5555"
       },
       "shipping_address": {
          "first_name": "John",
          "last_name": "Doe",
          "company": "Prospress",
          "address_1": "969 Market",
          "address_2": "",
          "city": "San Francisco",
          "state": "CA",
          "postcode": "94103",
          "country": "US"
       },
       "note": "",
       "customer_ip": "127.0.0.1",
       "customer_user_agent": "",
       "customer_id": 1,
       "view_order_url": "https://example.com/my-account/view-order/5285",
       "line_items": [
          {
            "id": 7882,
            "subtotal": "15.00",
            "subtotal_tax": "0.00",
            "total": "15.00",
            "total_tax": "0.00",
            "price": "15.00",
            "quantity": 1,
            "tax_class": null,
            "name": "Prospress Product",
            "product_id": 5052,
            "sku": "",
            "meta": []
          }
        ],
        "shipping_lines": [
          {
            "id": 7883,
            "method_id": "flat_rate",
            "method_title": "Flat Rate",
            "total": "10.00"
          }
        ],
        "tax_lines": [],
        "fee_lines": [],
        "coupon_lines": [],
        "customer": {
           "id": 1,
           "created_at": "2014-10-28T23:08:19Z",
           "email": "matt@prospress.com",
           "first_name": "Matthew",
           "last_name": "Allan",
           "username": "matt",
           "role": "administrator",
           "last_order_id": "7039",
           "last_order_date": "2015-11-04T06:21:09Z",
           "orders_count": 508,
           "total_spent": "6644.00",
           "avatar_url": "",
           "billing_address": {
              "first_name": "John",
              "last_name": "Doe",
              "company": "Prospress",
              "address_1": "969 Market",
              "address_2": "",
              "city": "San Francisco",
              "state": "CA",
              "postcode": "94103",
              "country": "US",
              "email": "john.doe@example.com",
              "phone": "(555) 555-5555"
           },
           "shipping_address": {
              "first_name": "John",
              "last_name": "Doe",
              "company": "Prospress",
              "address_1": "969 Market",
              "address_2": "",
              "city": "San Francisco",
              "state": "CA",
              "postcode": "94103",
              "country": "US"
           }
       }
    }
]
```