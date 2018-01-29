# Merchant Search

The `merchant_search` endpoint allows you to search for merchants based on various parameters and returns an array of [Merchant Objects](#merchant-properties) that match your search.


## Search merchants

> Example Merchant Search Request

```shell
curl --request POST \
  --url https://api.datafeedr.com/merchant_search \
  --data '{
    "aid": "ACCESS_ID",
    "akey": "ACCESS_KEY",
    "query": [
        "name LIKE magazines|=books",
        "source LIKE coupons",
        "product_count > 5"
    ],
    "sort": ["+name", "-product_count"],
    "fields": ["name", "product_count", "source"],
    "limit": 10,
    "offset": 0
}'
```

```php
<?php

$endpoint = "https://api.datafeedr.com/merchant_search";

$postfields = json_encode([
    'aid'  => 'ACCESS_ID',
    'akey' => 'ACCESS_KEY'
]);

$curl = curl_init();

curl_setopt_array($curl, array(
    CURLOPT_URL            => $endpoint,
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_ENCODING       => "",
    CURLOPT_MAXREDIRS      => 10,
    CURLOPT_TIMEOUT        => 30,
    CURLOPT_HTTP_VERSION   => CURL_HTTP_VERSION_1_1,
    CURLOPT_CUSTOMREQUEST  => "POST",
    CURLOPT_POSTFIELDS     => $postfields,
    CURLOPT_HTTPHEADER     => array(
        "Cache-Control: no-cache"
    ),
));

$response = curl_exec($curl);
$err      = curl_error($curl);

curl_close($curl);

if ($err) {
    echo "cURL Error #:" . $err;
} else {
    echo $response;
}
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.datafeedr.com/networks")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Post.new(url)
request.body = "{\n    \"aid\": \"ACCESS_ID\",\n    \"akey\": \"ACCESS_KEY\"\n}"

response = http.request(request)
puts response.read_body
```

```python
import requests

url = "https://api.datafeedr.com/networks"

payload = "{\n    \"aid\": \"ACCESS_ID\",\n    \"akey\": \"ACCESS_KEY\"\n}"
headers = {
    'Cache-Control': "no-cache"
    }

response = requests.request("POST", url, data=payload, headers=headers)

print(response.text)
```

```javascript
var http = require("https");

var options = {
  "method": "POST",
  "hostname": [
    "api",
    "datafeedr",
    "com"
  ],
  "path": [
    "networks"
  ],
  "headers": {
    "Cache-Control": "no-cache"
  }
};

var req = http.request(options, function (res) {
  var chunks = [];

  res.on("data", function (chunk) {
    chunks.push(chunk);
  });

  res.on("end", function () {
    var body = Buffer.concat(chunks);
    console.log(body.toString());
  });
});

req.write("{\n    \"aid\": \"ACCESS_ID\",\n    \"akey\": \"ACCESS_KEY\"\n}");
req.end();
```

> Example Merchant Search Response

```json
{
    "status": {
        "network_count": 173,
        "plan_id": 10300,
        "user_id": 190,
        "max_total": 10000,
        "merchant_count": 57971,
        "max_requests": 100000,
        "bill_day": 16,
        "request_count": 4368,
        "product_count": 456469693,
        "max_length": 100
    },
    "merchants": [
        {
            "product_count": 28,
            "source": "ShareASale Coupons/Deals",
            "name": "Best Deal Magazines"
        },
        {
            "product_count": 15,
            "source": "Commission Junction Coupons/Deals",
            "name": "www.iseeme.com Personalized Children's Books"
        },
        {
            "product_count": 9,
            "source": "Commission Junction Coupons/Deals",
            "name": "Indigo Books & Music"
        }
    ],
    "version": "0.2",
    "length": 3,
    "found_count": 3,
    "time": 2494,
    "networks": [
        {
            "group": "ShareASale",
            "name": "ShareASale Coupons/Deals",
            "merchant_count": 7219,
            "product_count": 19535,
            "_id": 8,
            "type": "coupons"
        },
        {
            "group": "Commission Junction",
            "name": "Commission Junction Coupons/Deals",
            "merchant_count": 2106,
            "product_count": 7176,
            "_id": 120,
            "type": "coupons"
        }
    ],
    "result_count": 3
}
```

`POST https://api.datafeedr.com/merchant_search`

Search for merchants matching specific criteria.

See a list of [queryable Merchant fields](#merchant-fields).


### Request Properties

Property | Value | Type | Required
---|---|---|---
`query` | [`Query`](#query-object) Object. | `object`  | Yes
`sort` | An array of fields to sort results by.  Each field should be preceded by `+` for ascending or `-` for descending. | `["+name","..."]` | No
`fields` | Array of `Merchant` properties to include in the results. | `["name","source","..."]` | No
`limit` | Number of results to return. | `integer` | No
`offset` | Offset (for paginating through the results). | `integer` | No

### Response Properties

Property | Type | Description
---|---|---
`merchants` | array | Array of [`Merchant`](#merchant-properties) Objects.
`length` | integer | Number of merchants returned.
`status` | object | [`Status`](#status-properties) Object.
`time` | integer | Time spent processing the API request (in milliseconds).
`version` | string | The current version of the API.








