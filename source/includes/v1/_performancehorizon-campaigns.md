# Partnerize Camref

The `performancehorizon_campaigns` endpoint returns [`PerformanceHorizonCampaign`](#performancehorizoncampaign-properties) Objects which can be used to get your Partnerize `camref` value which is the value you will use as your Partnerize affiliate ID.



## PerformanceHorizonCampaign Properties

The `PerformanceHorizonCampaign` Object contains information about a Partnerize merchant.


Property | Type | Description
---|---|---
`camref` | string | Partnerize Affiliate ID (Replace `@@@` with this value).
`campaign_id` | string | Partnerize Adspace ID.
`merchant_id`  | integer | Datafeedr Merchant ID.



## Get Partnerize camref

> Partnerize Campaign Request

```shell
curl --request POST \
  --url https://api.datafeedr.com/performancehorizon_campaigns \
  --data '{
    "aid": "ACCESS_ID",
    "akey": "ACCESS_KEY",
    "merchant_ids": [80512, 81737],
    "application_key": "PH_APPLICATION_KEY",
    "user_api_key": "PH_USER_API_KEY",
    "publisher_id": "PH_USER_PUBLISHER_ID"
}'
```

```php
<?php

$url = "https://api.datafeedr.com/performancehorizon_campaigns";

$data = json_encode([
    'aid'             => 'ACCESS_ID',
    'akey'            => 'ACCESS_KEY',
    'merchant_ids'    => [80512, 81737],
    'application_key' =>  'PH_APPLICATION_KEY',
    'user_api_key'    =>  'PH_USER_API_KEY',
    'publisher_id'    =>  'PH_USER_PUBLISHER_ID'
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

url = "https://api.datafeedr.com/performancehorizon_campaigns"

data = {
    "aid": "ACCESS_ID",
    "akey": "ACCESS_KEY",
    "merchant_ids": [80512, 81737],
    "application_key": "PH_APPLICATION_KEY",
    "user_api_key": "PH_USER_API_KEY",
    "publisher_id": "PH_USER_PUBLISHER_ID"
}

response = requests.post(url, json=data)
print(response.json())
```

```javascript
var axios = require('axios');

var url = "https://api.datafeedr.com/performancehorizon_campaigns";

var data = {
    "aid": "ACCESS_ID",
    "akey": "ACCESS_KEY",
    "merchant_ids": [80512, 81737],
    "application_key": "PH_APPLICATION_KEY",
    "user_api_key": "PH_USER_API_KEY",
    "publisher_id": "PH_USER_PUBLISHER_ID"
};

axios.post(url, data).then(function (response) {
    console.log(response.data)
});
```


> Partnerize Campaign Response

```json
{
    "status": {
        "network_count": 173,
        "plan_id": 10300,
        "user_id": 190,
        "max_total": 10000,
        "merchant_count": 58018,
        "max_requests": 100000,
        "bill_day": 16,
        "request_count": 5003,
        "product_count": 428272607,
        "max_length": 100
    },
    "version": "0.2",
    "time": 851,
    "performancehorizon_campaigns": [
        {
            "merchant_id": 80512,
            "campaign_id": "1101l991",
            "camref": "1199l3eMb"
        },
        {
            "merchant_id": 81737,
            "campaign_id": "1101l876",
            "camref": "1034l3bMe"
        }
    ]
}
```

`POST https://api.datafeedr.com/performancehorizon_campaigns`

Get the `camref` values (ie. affiliate IDs) for specific Partnerize merchants.




### Request Properties

Property | Value | Type | Required
---|---|---|---|---
`merchant_ids` | Array of Datafeedr [`Merchant`](#merchant-properties) IDs. | `[12345, 13524,...]` | Yes
`application_key` | Your [Partnerize Application Key](https://datafeedrapi.helpscoutdocs.com/article/195-how-to-find-your-performance-horizon-publisher-id-and-api-keys). | `string` | Yes
`user_api_key` | Your [Partnerize User API Key](https://datafeedrapi.helpscoutdocs.com/article/195-how-to-find-your-performance-horizon-publisher-id-and-api-keys). | `string` | Yes
`publisher_id` | Your [Partnerize Publisher ID](https://datafeedrapi.helpscoutdocs.com/article/195-how-to-find-your-performance-horizon-publisher-id-and-api-keys). | `string` | Yes




### Response Properties

Property | Type | Description
---|---|---
`performancehorizon_campaigns` | array | An array of [`PerformanceHorizonCampaign`](#performancehorizoncampaign-properties) Objects.


