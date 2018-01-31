# Zanox Merchant IDs

The `zanox_merchant_ids` endpoint returns [`ZanoxMerchant`](#zanoxmerchant-properties) Objects which can be used to get your Zanox Merchant IDs (`zmid`) which is the value you will use as your Zanox affiliate ID.



## ZanoxMerchant Properties

The `ZanoxMerchant` Object contains information a Zanox merchant.


Property | Type | Description
---|---|---
`zmid` | string | Zanox Affiliate ID (Replace `@@@` with this value).
`adspace_id` | integer | Zanox Adspace ID.
`program_id` | string | Zanox Program ID.
`merchant_id`  | integer | Datafeedr Merchant ID.



## Get Zanox zmid

> Zanox Merchant IDs Request

```shell
curl --request POST \
  --url https://api.datafeedr.com/zanox_merchant_ids \
  --data '{
    "aid": "ACCESS_ID",
    "akey": "ACCESS_KEY",
    "connect_id": "ZANOX_CONNECTION_ID",
    "merchant_ids": [46548, 79142]
}'
```

```php
<?php

$endpoint = "https://api.datafeedr.com/zanox_merchant_ids";

$data = json_encode([
    'aid'          => 'ACCESS_ID',
    'akey'         => 'ACCESS_KEY',
    'connect_id'   => 'ZANOX_CONNECTION_ID',
    'merchant_ids' => [46548, 79142]
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

url = "https://api.datafeedr.com/zanox_merchant_ids"

data = {
    "aid": "ACCESS_ID",
    "akey": "ACCESS_KEY",
    "connect_id": "ZANOX_CONNECTION_ID",
    "merchant_ids": [46548, 79142]
}

response = requests.post(url, json=data)
print(response.json())
```

```javascript
var axios = require('axios');

var url = "https://api.datafeedr.com/zanox_merchant_ids";

var data = {
    "aid": "ACCESS_ID",
    "akey": "ACCESS_KEY",
    "connect_id": "ZANOX_CONNECTION_ID",
    "merchant_ids": [46548, 79142]
};

axios.post(url, data).then(function (response) {
    console.log(response.data)
});
```


> Zanox Merchant IDs Response

```json
{
    "status": {
        "network_count": 173,
        "plan_id": 10300,
        "user_id": 190,
        "max_total": 10000,
        "merchant_count": 57973,
        "max_requests": 100000,
        "bill_day": 16,
        "request_count": 4402,
        "product_count": 455689593,
        "max_length": 100
    },
    "version": "0.2",
    "zanox_merchant_ids": [
        {
            "zmid": "21612326605C04682",
            "adspace_id": 1234567,
            "merchant_id": 46548,
            "program_id": 10779
        },
        {
            "zmid": "68221612326605C18",
            "adspace_id": 3456789,
            "merchant_id": 79142,
            "program_id": 19192
        }
    ],
    "time": 329
}
```

`POST https://api.datafeedr.com/zanox_merchant_ids`

Get the `zmid` values (ie. affiliate IDs) for specific Zanox merchants.




### Request Properties

Property | Value | Type | Required
---|---|---|---|---
`merchant_ids` | Array of Datafeedr [`Merchant`](#merchant-properties) IDs. | `[12345, 13524,...]` | Yes
`connect_id` | Your [Zanox Connection ID](https://datafeedrapi.helpscoutdocs.com/article/149-how-to-find-your-zanox-api-keys). | `string` | Yes




### Response Properties

Property | Type | Description
---|---|---
`zanox_merchant_ids` | array | An array of [`ZanoxMerchant`](#zanoxmerchant-properties) Objects.
`status` | object | [`Status`](#status-properties) Object.
`time` | integer | Time spent processing the API request (in milliseconds).
`version` | string | The current version of the API.

