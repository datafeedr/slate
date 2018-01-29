# Status

The `Status` Object contains information about the API status and your account.




## Status Properties

The `Status` Object contains the following properties.

Property | Type | Description
---|---|---
`network_count` | integer | Total number of affiliate networks.
`merchant_count` | integer | Total number of merchants.
`product_count`  | integer | Total number of products.
`plan_id` | string | Your Datafeedr subscription plan ID.
`bill_day` | integer | Day of the month your subscription billing cycle renews.
`request_count` | integer | Total number of API requests made since the start of the billing cycle.
`max_total` | integer | Maximum number of results returned for a search (requires `offset`).
`max_length` | integer | Maximum number of records returned per API Request.
`max_requests` | integer | Maximum number of API Requests per billing cycle.




## Retrieve Status

> Status Request

```shell
curl --request POST \
  --url https://api.datafeedr.com/status \
  --data '{
    "aid": "ACCESS_ID",
    "akey": "ACCESS_KEY"
}'
```

```php
<?php

$endpoint = "https://api.datafeedr.com/status";

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

url = URI("https://api.datafeedr.com/status")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Post.new(url)
request.body = "{\n    \"aid\": \"ACCESS_ID\",\n    \"akey\": \"ACCESS_KEY\"\n}"

response = http.request(request)
puts response.read_body
```

```python
import requests

url = "https://api.datafeedr.com/status"

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
    "status"
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

> Status Response

```json
{
    "status": {
        "network_count": 173,
        "plan_id": 10300,
        "user_id": 190,
        "max_total": 10000,
        "merchant_count": 57970,
        "max_requests": 100000,
        "bill_day": 16,
        "request_count": 4053,
        "product_count": 454449243,
        "max_length": 100
    },
    "version": "0.2",
    "time": 0
}
```

`POST https://api.datafeedr.com/status`

Retrieve information about the Datafeedr API and your account.




### Request Properties

There are no additional properties required for this Request.




### Response Properties

Property | Type | Description
---|---|---
`status` | object | `Status` Object.
`time` | integer | Time spent processing the API request (in milliseconds).
`version` | string | The current version of the API.

