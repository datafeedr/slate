# Status

The `status` endpoint returns [`Status`](#status-properties) related data.



## Status Properties

The `Status` Object contains information about the API status and your account.


Property | Type | Description
---|---|---
`network_count` | integer | Total number of affiliate networks.
`merchant_count` | integer | Total number of merchants.
`product_count`  | integer | Total number of products.
`plan_id` | integer | Your Datafeedr subscription plan ID.
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

$url = "https://api.datafeedr.com/status";

$data = json_encode([
    'aid'  => 'ACCESS_ID',
    'akey' => 'ACCESS_KEY'
]);

$ch = curl_init($url);
curl_setopt_array($ch, [
    CURLOPT_RETURNTRANSFER => 1,
    CURLOPT_HTTPHEADER     => ['Content-Type: application/json'],
    CURLOPT_POSTFIELDS     => $data
]);

$response = curl_exec($ch);
curl_close($ch);

print_r(json_decode($response));
```

```python
import requests

url = "https://api.datafeedr.com/status"

data = {
    "aid": "ACCESS_ID",
    "akey": "ACCESS_KEY"
}

response = requests.post(url, json=data)
print(response.json())
```

```javascript
var axios = require('axios');

var url = "https://api.datafeedr.com/status";

var data = {
    "aid": "ACCESS_ID",
    "akey": "ACCESS_KEY"
};

axios.post(url, data).then(function (response) {
    console.log(response.data)
});
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
`status` | object | [`Status`](#status-properties) Object.
`time` | integer | Time spent processing the API request (in milliseconds).
`version` | string | The current version of the API.

