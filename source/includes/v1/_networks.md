# Networks

The `networks` endpoint returns [`Network`](#network-properties) related data.


## Network Properties


The `Network` Object contains information about a single affiliate network.


Property | Type | Description
---|---|---
`_id` | integer | Affiliate network ID.
`name` | string | Affiliate network name.
`group` | string | Affiliate network group (common) name.
`merchant_count`  | integer | Total number of merchants in this network.
`product_count`  | integer | Total number of records in this network.
`type` | string | Type of records this network supports. Either "products" or "coupons".




## Get all networks

> Example Network Request

```shell
curl --request POST \
  --url https://api.datafeedr.com/networks \
  --data '{
    "aid": "ACCESS_ID",
    "akey": "ACCESS_KEY"
}'
```

```php
<?php

$endpoint = "https://api.datafeedr.com/networks";

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

> Example Network Response

```json
{
    "status": {
        "network_count": 173,
        "plan_id": 10300,
        "user_id": 190,
        "max_total": 10000,
        "merchant_count": 57934,
        "max_requests": 100000,
        "bill_day": 16,
        "request_count": 3301,
        "product_count": 456177393,
        "max_length": 100
    },
    "length": 173,
    "version": "0.2",
    "networks": [
        {
            "group": "Adrecord",
            "name": "Adrecord Coupons/Deals",
            "merchant_count": 67,
            "product_count": 17,
            "_id": 271,
            "type": "coupons"
        },
        {
            "group": "Adrecord",
            "name": "Adrecord Denmark",
            "merchant_count": 8,
            "product_count": 15497,
            "_id": 277,
            "type": "products"
        },
        {
            "group": "Adrecord",
            "name": "Adrecord Finland",
            "merchant_count": 7,
            "product_count": 98239,
            "_id": 276,
            "type": "products"
        },
        {
            "group": "Adrecord",
            "name": "Adrecord Norway",
            "merchant_count": 24,
            "product_count": 261900,
            "_id": 275,
            "type": "products"
        },
        {
            "group": "Adrecord",
            "name": "Adrecord Sweden",
            "merchant_count": 330,
            "product_count": 734460,
            "_id": 270,
            "type": "products"
        },

        // ...

        {
            "group": "Zanox",
            "name": "Zanox Norway",
            "merchant_count": 17,
            "product_count": 948567,
            "_id": 410,
            "type": "products"
        },
        {
            "group": "Zanox",
            "name": "Zanox Poland",
            "merchant_count": 55,
            "product_count": 417207,
            "_id": 416,
            "type": "products"
        },
        {
            "group": "Zanox",
            "name": "Zanox Spain",
            "merchant_count": 77,
            "product_count": 1751507,
            "_id": 405,
            "type": "products"
        },
        {
            "group": "Zanox",
            "name": "Zanox Sweden",
            "merchant_count": 46,
            "product_count": 892027,
            "_id": 407,
            "type": "products"
        },
        {
            "group": "Zanox",
            "name": "Zanox Switzerland",
            "merchant_count": 61,
            "product_count": 4065447,
            "_id": 411,
            "type": "products"
        }
    ],
    "time": 0
}
```

`POST https://api.datafeedr.com/networks`

Get all affiliate networks.


### Request Properties

There are no additional properties required for this Request.


### Response Properties

Property | Type | Description
---|---|---
`networks` | array | Array of [`Network`](#network-properties) Objects.
`length` | integer | Number of networks returned.
`status` | object | [`Status`](#status-properties) Object.
`time` | integer | Time spent processing the API request (in milliseconds).
`version` | string | The current version of the API.












## Get specific networks & fields

> Example Network Request

```shell
curl --request POST \
  --url https://api.datafeedr.com/networks \
  --data '{
    "aid": "ACCESS_ID",
    "akey": "ACCESS_KEY",
    "fields": ["name", "product_count"],
    "source_ids": [6, 126]
}'
```

```php
<?php

$endpoint = "https://api.datafeedr.com/networks";

$postfields = json_encode([
    'aid'        => 'ACCESS_ID',
    'akey'       => 'ACCESS_KEY',
    'source_ids' => [6, 126]
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

> Example Network Response

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
        "request_count": 4365,
        "product_count": 456469693,
        "max_length": 100
    },
    "length": 2,
    "version": "0.2",
    "networks": [
        {
            "product_count": 1615690,
            "_id": 126,
            "name": "AvantLink US"
        },
        {
            "product_count": 20053459,
            "_id": 6,
            "name": "ShareASale"
        }
    ],
    "time": 0
}
```

`POST https://api.datafeedr.com/networks`

Get affiliate networks by network ID and limit the fields returned for each network.



### Request Properties

Property | Value | Type | Required
---|---|---|---|---
`fields` | Array of `Network` properties to include in the results. | `["name","type","..."]` | No
`source_ids` | Array of network IDs to filter results by. | `[4,6,9,...]` | No


### Response Properties

Property | Type | Description
---|---|---
`networks` | array | Array of [`Network`](#network-properties) Objects.
`length` | integer | Number of networks returned.
`status` | object | [`Status`](#status-properties) Object.
`time` | integer | Time spent processing the API request (in milliseconds).
`version` | string | The current version of the API.









