# Introduction

WooCommerce Subscriptions 2.1+ and WooCommerce 2.6+ have been fully integrated with the WordPress REST API. This allows WC and Subscriptions data to be created, read, updated, and deleted using requests in JSON format and using WordPress REST API Authentication methods and standard HTTP verbs which are understood by most HTTP clients.

The current WP REST API integration version is v3 which takes a first-order position in endpoints.

The following table shows API versions present in each major version of WooCommerce:

| API Version | WC Subscriptions Version |  WC Version  |  WP Version  |    Documentation    |
|-------------|--------------------------|--------------|--------------|---------------------|
| `v3`        | 3.1 or later             | 3.7 or later | 4.4 or later | -                   |
| `v1`        | 2.1 or later             | 2.6 or later | 4.4 or later | [v1 docs](v1.html)  |

## Requirements

To use the latest version of the REST API you must be using:

* WooCommerce Subscriptions 3.1+.
* WooCommerce 3.7+.
* WordPress 4.4+.
* Pretty permalinks in `Settings > Permalinks` so that the custom endpoints are supported. __Default permalinks will not work.__
* You may access the API over either HTTP or HTTPS, but *HTTPS is recommended where possible*.

If you use ModSecurity and see `501 Method Not Implemented` errors, see [this issue](https://github.com/woocommerce/woocommerce/issues/9838) for details.

<aside class="notice">
	Please note that you are <strong>not</strong> required to install the <a href="https://wordpress.org/plugins/rest-api/" target="_blank">WP REST API (WP API)</a> plugin.
</aside>

## Request/Response Format ##

The default response format is JSON. Requests with a message-body use plain JSON to set or update resource attributes. Successful requests will return a `200 OK` HTTP status.

Some general information about responses:

* Dates are returned in [RFC3339](http://www.ietf.org/rfc/rfc3339.txt) format in UTC timezone: `YYYY-MM-DDTHH:MM:SSZ`
* Resource IDs are returned as integers.
* Any decimal monetary amount, such as prices or totals, will be returned as strings with two decimal places.
* Other amounts, such as item counts, are returned as integers.
* Blank fields are generally included as `null` instead of being returned as blank strings or omitted.

### JSONP Support ###

The WP REST API supports JSONP by default. JSONP responses use the `application/javascript` content-type. You can specify the callback using the `?_jsonp` parameter for `GET` requests to have the response wrapped in a JSON function:

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-get">GET</i>
		<h6>/wp-json/wc/v1?_jsonp=callback</h6>
	</div>
</div>

```shell
curl https://example.com/wp-json/wc/v1/products/tags/34?_jsonp=tagDetails \
	-u consumer_key:consumer_secret
```

```javascript
WooCommerce.get('products/tags/34?_jsonp=tagDetails', function(err, data, res) {
  console.log(res);
});
```

```php
<?php print_r($woocommerce->get('products/tags/34', ['_jsonp' => 'tagDetails'])); ?>
```

```python
print(wcapi.get("products/tags/34?_jsonp=tagDetails").json())
```

```ruby
woocommerce.get("products/tags/34", _jsonp: "tagDetails").parsed_response
```

> Response:

```
/**/tagDetails({"id":34,"name":"Leather Shoes","slug":"leather-shoes","description":"","count":0,"_links":{"self":[{"href":"https://example.com/wp-json/wc/v1/products/tags/34"}],"collection":[{"href":"https://example.com/wp-json/wc/v1/products/tags"}]}})%
```
