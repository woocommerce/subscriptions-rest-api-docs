# System Status #

Please refer to WooCommerce's guide on the [System Status endpoint](https://woocommerce.github.io/woocommerce-rest-api-docs/?shell#list-all-system-status-items). WooCommerce Subscriptions adds additional data to that endpoint's response. That additional data is documented below.

## Subscriptions properties ##

|             Attribute              |   Type  |                                Description                            |
|------------------------------------|---------|-----------------------------------------------------------------------|
| `wcs_debug`                        | boolean | Is WC Subscriptions debugging mode active?                            |
| `mode`                             | string  | Whether the site is in `"live"` or `"staging"` mode.                  |
| `live_url`                         | string  | The URL Subscriptions considers to be the site's live URL.            |
| `statuses`                         | array   | A breakdown of subscriptions and their statuses.                      |
| `report_cache_enabled`             | boolean | Whether the report caches are enabled.                                |
| `cache_update_failures`            | integer | The number of times report cache updates have failed.                 |
| `subscriptions_by_payment_gateway` | array   | A breakdown of subscriptions by the gateway and their status.         |
| `payment_gateway_feature_support`  | array   | A breakdown of the features supported by the active payment gateways. |

## List all system status items ##

### HTTP request ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-get">GET</i>
		<h6>wp-json/wc/v3/system_status</h6>
	</div>
</div>

<aside class="notice">
	The JSON example response only includes the sections added by WC Subscriptions. Please refer to <a href="https://woocommerce.github.io/woocommerce-rest-api-docs/#list-all-system-status-items">WooCommerce's documentation of the System Status endpoint</a> for the base response.
</aside>

```shell
curl https://example.com/wp-json/wc/v3/system_status \
	-u consumer_key:consumer_secret
```

```javascript
WooCommerce.get("system_status")
  .then((response) => {
    console.log(response.data);
  })
  .catch((error) => {
    console.log(error.response.data);
  });
```

```php
<?php print_r($woocommerce->get('system_status')); ?>
```

```python
print(wcapi.get("system_status").json())
```

```ruby
woocommerce.get("system_status").parsed_response
```

> JSON response example:

```json
{
...
"subscriptions": {
        "wcs_debug": true,
        "mode": "live",
        "live_url": "http://example.com",
        "statuses": {
            "trash": "3",
            "auto-draft": "1",
            "wc-active": "106",
            "wc-pending-cancel": "3",
            "wc-pending": "34",
            "wc-on-hold": "120",
            "wc-cancelled": "22"
        },
        "report_cache_enabled": true,
        "cache_update_failures": 0,
        "subscriptions_by_payment_gateway": {
            "paypal": {
                "wc-cancelled": "1"
            },
            "square_credit_card": {
                "wc-active": "1",
                "wc-on-hold": "60"
            },
            "stripe": {
                "trash": "3",
                "wc-active": "104",
                "wc-cancelled": "21",
                "wc-on-hold": "51",
                "wc-pending": "23",
                "wc-pending-cancel": "2"
            }
        },
        "payment_gateway_feature_support": {
            "paypal": [
                "subscription_payment_method_change_customer",
                "subscription_payment_method_change_admin",
                "subscription_amount_changes",
                "subscription_date_changes",
                "multiple_subscriptions",
                "subscription_payment_method_delayed_change",
                "subscriptions",
                "subscription_cancellation",
                "subscription_suspension",
                "subscription_reactivation",
                "products",
                "refunds",
                "paypal_reference_transactions"
            ],
            "ppec_paypal": [
                "products",
                "refunds",
                "subscriptions",
                "subscription_cancellation",
                "subscription_reactivation",
                "subscription_suspension",
                "multiple_subscriptions",
                "subscription_payment_method_change_customer",
                "subscription_payment_method_change_admin",
                "subscription_amount_changes",
                "subscription_date_changes"
            ],
            "stripe": [
                "products",
                "refunds",
                "tokenization",
                "add_payment_method",
                "subscriptions",
                "subscription_cancellation",
                "subscription_suspension",
                "subscription_reactivation",
                "subscription_amount_changes",
                "subscription_date_changes",
                "subscription_payment_method_change",
                "subscription_payment_method_change_customer",
                "subscription_payment_method_change_admin",
                "multiple_subscriptions",
                "pre-orders"
            ]
        }
    }
```





