# Products


The `search` endpoint returns [`Product`](#product-properties) data matching your search.


## Product properties

The `Product` Object contains information about a single Product.


### Mandatory `Product` Object Properties

The following properties are returned in every `Product` Object.

Property | Type | Description
---|---|---
`_id` | integer | Product ID.
`currency` | string | Three letter ISO-4217 currency code.
`finalprice` | integer | Lowest price of product (either sale or regular price) in least valued currency units (e.g cents).
`merchant_id` | integer | Merchant ID.
`merchant`  | string | Merchant name.
`name` | string | Product name.
`onsale` | integer | Indicates if product is on sale. 0=No, 1=Yes.
`price` | integer | Price of product in least valued currency units (e.g cents).
`salediscount` | integer | The percentage that price has been discounted in whole numbers.
`source_id` | integer | Affiliate network ID.
`source` | string | Affiliate network name.
`time_updated` | timestamp | Timestamp of the last time product was updated in API.
`url` | string | Affiliate URL.


### Common `Product` Object Properties

The following properties are often (but not always) returned in the `Product` Object.

Property | Type | Description
---|---|---
`brand` | string | Product brand.
`category` | string | Category field(s) product is in.
`color` | string | Product color.
`description` | string | Product description.
`direct_url` | string | Direct URL to product page on merchant's site (This is NOT an affiliate link and will NOT generate a commission).
`ean` | string | Product EAN.
`gender` | string | Product gender data.
`htmldescription` | string | Product description in HTML.
`image` | string | Product image URL.
`isbn` | string | Product ISBN.
`ref_url` | string | Affiliate URL with sub ID parameter
`saleprice` | integer | Sale price of product in least valued currency units (e.g cents).
`size` | string | Product size data.
`sku` | string | Product SKU.
`tags` | string | Product tags separated by semi-colons.
`thumbnail` | string | Product image thumbnail.
`upc` | string | Product UPC.


### Coupon Specific Properties

Coupons & Deals are returned as `Product` Objects and may contain the following properties depending on the type of coupon or deal being offered.

Property | Type | Description
---|---|---
`offerbegin` | timestamp | The date & time the offer begins.
`offerend` | timestamp | The date & time the offer ends.
`offercode` | string | Coupon or discount code required to get discount.











## Search products

> Example Product Search Request

```shell
curl --request POST \
  --url https://api.datafeedr.com/search \
  --data '{
    "aid": "ACCESS_ID",
    "akey": "ACCESS_KEY",
    "query": [
    	"any LIKE climbing women|woman",
        "name LIKE harness",
        "source LIKE avantlink|linkshare",
        "price > 5000",
        "price < 15000",
        "merchant !LIKE Jet|Groupon",
        "onsale = 1",
        "image !EMPTY",
        "currency = USD",
        "brand LIKE mammut|\"black diamond\"|petzl",
        "salediscount >= 15"
    ],
    "fields": ["name", "price", "finalprice", "merchant", "source", "brand", "salediscount", "url", "currency", "image"],
    "price_groups": 3,
    "limit": 10,
    "offset": 0,
    "sort": ["+finalprice"],
    "exclude_duplicates": "merchant_id name|image",
    "string_ids": false
}'
```

```php
<?php

$endpoint = "https://api.datafeedr.com/search";

$data = json_encode([
    'aid'    => 'ACCESS_ID',
    'akey'   => 'ACCESS_KEY',
    'query'              => [
        'any LIKE climbing women|woman',
        'name LIKE harness',
        'source LIKE avantlink|linkshare',
        'price > 5000',
        'price < 15000',
        'merchant !LIKE Jet|Groupon',
        'onsale = 1',
        'image !EMPTY',
        'currency = USD',
        'brand LIKE mammut|\'black diamond\'|petzl',
        'salediscount >= 15'
    ],
    'fields'             => [
        'name',
        'price',
        'finalprice',
        'merchant',
        'source',
        'brand',
        'salediscount',
        'url',
        'currency',
        'image'
    ],
    'price_groups'       => 3,
    'limit'              => 10,
    'offset'             => 0,
    'sort'               => ['+finalprice'],
    'exclude_duplicates' => 'merchant_id name|image',
    'string_ids'         => false
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
    CURLOPT_POSTFIELDS     => $data,
    CURLOPT_HTTPHEADER     => array("Cache-Control: no-cache"),
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

```python
import requests

url = "https://api.datafeedr.com/search"

data = {
    "aid": "ACCESS_ID",
    "akey": "ACCESS_KEY",
    "query": [
        "any LIKE climbing women|woman",
        "name LIKE harness",
        "source LIKE avantlink|linkshare",
        "price > 5000",
        "price < 15000",
        "merchant !LIKE Jet|Groupon",
        "onsale = 1",
        "image !EMPTY",
        "currency = USD",
        "brand LIKE mammut|'black diamond'|petzl",
        "salediscount >= 15"
    ],
    "fields": [
        "name",
        "price",
        "finalprice",
        "merchant",
        "source",
        "brand",
        "salediscount",
        "url",
        "currency",
        "image"
    ],
    "price_groups": 3,
    "limit": 10,
    "offset": 0,
    "sort": ["+finalprice"],
    "exclude_duplicates": "merchant_id name|image",
    "string_ids": False
}

response = requests.post(url, json=data)
print(response.json())
```

```javascript
var axios = require('axios');

var url = "https://api.datafeedr.com/search";

var data = {
    "aid": "ACCESS_ID",
    "akey": "ACCESS_KEY",
    "query": [
        "any LIKE climbing women|woman",
        "name LIKE harness",
        "source LIKE avantlink|linkshare",
        "price > 5000",
        "price < 15000",
        "merchant !LIKE Jet|Groupon",
        "onsale = 1",
        "image !EMPTY",
        "currency = USD",
        "brand LIKE mammut|'black diamond'|petzl",
        "salediscount >= 15"
    ],
    "fields": [
        "name",
        "price",
        "finalprice",
        "merchant",
        "source",
        "brand",
        "salediscount",
        "url",
        "currency",
        "image"
    ],
    "price_groups": 3,
    "limit": 10,
    "offset": 0,
    "sort": ["+finalprice"],
    "exclude_duplicates": "merchant_id name|image",
    "string_ids": false
}

axios.post(url, data).then(function (response) {
    console.log(response.data)
});
```

> Example Product Search Response

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
        "request_count": 4374,
        "product_count": 456437575,
        "max_length": 100
    },
    "merchants": [
        {
            "product_count": 5,
            "merchant": "Backcountry.com",
            "merchant_id": 33092,
            "source_id": 126,
            "source": "AvantLink US"
        },
        {
            "product_count": 2,
            "merchant": "Eastern Mountain Sports",
            "merchant_id": 21734,
            "source_id": 126,
            "source": "AvantLink US"
        },
        {
            "product_count": 5,
            "merchant": "Outdoorplay",
            "merchant_id": 61261,
            "source_id": 126,
            "source": "AvantLink US"
        },
        {
            "product_count": 1,
            "merchant": "Sunny Sports",
            "merchant_id": 67698,
            "source_id": 126,
            "source": "AvantLink US"
        },
        {
            "product_count": 2,
            "merchant": "Eastern Mountain Sports",
            "merchant_id": 81397,
            "source_id": 4,
            "source": "LinkShare US"
        },
        {
            "product_count": 2,
            "merchant": "Mountain Steals",
            "merchant_id": 78391,
            "source_id": 126,
            "source": "AvantLink US"
        },
        {
            "product_count": 2,
            "merchant": "Climb High",
            "merchant_id": 28506,
            "source_id": 126,
            "source": "AvantLink US"
        },
        {
            "product_count": 6,
            "merchant": "REI.com",
            "merchant_id": 21757,
            "source_id": 126,
            "source": "AvantLink US"
        }
    ],
    "version": "0.2",
    "total_found": 32,
    "length": 10,
    "found_count": 32,
    "products": [
        {
            "merchant": "REI.com",
            "name": "Black Diamond Women's Primrose Climbing Harness",
            "source": "AvantLink US",
            "url": "http://classic.avantlink.com/click.php?p=61371&pw=@@@&pt=3&pri=634361&tt=df",
            "image": "http://i1.avlws.com/115/l634361.png",
            "finalprice": 4373,
            "price": 5495,
            "currency": "USD",
            "salediscount": 20,
            "_id": 2175702112172441,
            "brand": "Black Diamond"
        },
        {
            "merchant": "REI.com",
            "name": "Mammut Women's Ophira 3 Slide Climbing Harness",
            "currency": "USD",
            "url": "http://classic.avantlink.com/click.php?p=61371&pw=@@@&pt=3&pri=580568&tt=df",
            "brand": "Mammut",
            "finalprice": 4393,
            "source": "AvantLink US",
            "image": "http://i1.avlws.com/115/l580568.png",
            "salediscount": 20,
            "_id": 2175700242158567,
            "price": 5495
        },
        {
            "merchant": "Backcountry.com",
            "name": "Black Diamond Primrose Speed Adjust Harness - Women's",
            "currency": "USD",
            "url": "http://classic.avantlink.com/click.php?p=86259&pw=@@@&pt=3&pri=1210518&tt=df",
            "image": "http://i2.avlws.com/52/l1210518.png",
            "finalprice": 4396,
            "price": 5495,
            "source": "AvantLink US",
            "salediscount": 20,
            "_id": 3309200309657707,
            "brand": "Black Diamond"
        },
        {
            "merchant": "Sunny Sports",
            "name": "Mammut Togira Slide Climbing Harness for Women",
            "source": "AvantLink US",
            "url": "http://classic.avantlink.com/click.php?p=234563&pw=@@@&pt=3&pri=7979&tt=df",
            "image": "http://www.sunnysports.com/image/product/large/MMTTSW.jpg",
            "brand": "Mammut",
            "finalprice": 4495,
            "currency": "USD",
            "salediscount": 31,
            "_id": 6769801092426801,
            "price": 6495
        },
        {
            "merchant": "Eastern Mountain Sports",
            "name": "Petzl Women's Selena Climbing Harness",
            "source": "LinkShare US",
            "url": "http://click.linksynergy.com/link?id=@@@&offerid=303281.7092379742&type=15&murl=http%3A%2F%2Fwww.ems.com%2Fpetzl-womens-selena-climbing-harness%2F20188100021.html",
            "image": "http://www.ems.com/dw/image/v2/AAQU_PRD/on/demandware.static/-/Sites-vestis-master-catalog/default/dwcf89725c/product/images/1313/560/1313560/1313560_607_main.jpg",
            "brand": "PETZL",
            "finalprice": 4547,
            "currency": "USD",
            "salediscount": 30,
            "_id": 8139700164302743,
            "price": 6495
        },
        {
            "merchant": "Eastern Mountain Sports",
            "name": "Petzl Women's Selena Climbing Harness",
            "currency": "USD",
            "url": "http://classic.avantlink.com/click.php?p=60837&pw=@@@&pt=3&pri=561791&tt=df",
            "image": "http://i1.avlws.com/843/l561791.png",
            "brand": "Petzl",
            "finalprice": 4547,
            "source": "AvantLink US",
            "salediscount": 30,
            "_id": 2173400004351340,
            "price": 6495
        },
        {
            "merchant": "REI.com",
            "name": "Petzl Women's Selena Climbing Harness",
            "currency": "USD",
            "url": "http://classic.avantlink.com/click.php?p=61371&pw=@@@&pt=3&pri=580573&tt=df",
            "brand": "Petzl",
            "finalprice": 4793,
            "source": "AvantLink US",
            "image": "http://i1.avlws.com/115/l580573.png",
            "salediscount": 26,
            "_id": 2175700244491303,
            "price": 6495
        },
        {
            "merchant": "Outdoorplay",
            "name": "Black Diamond Women's Solution Climbing Harness",
            "currency": "USD",
            "url": "http://classic.avantlink.com/click.php?p=199519&pw=@@@&pt=3&pri=60466&tt=df",
            "price": 6995,
            "finalprice": 4897,
            "source": "AvantLink US",
            "image": "http://i2.avlws.com/3229/l60466.png",
            "salediscount": 30,
            "_id": 6126100196451361,
            "brand": "Black Diamond"
        },
        {
            "merchant": "Outdoorplay",
            "name": "Petzl Women's Selena Rock Climbing Harness",
            "currency": "USD",
            "url": "http://classic.avantlink.com/click.php?p=199519&pw=@@@&pt=3&pri=60488&tt=df",
            "price": 6495,
            "finalprice": 5196,
            "source": "AvantLink US",
            "image": "http://i2.avlws.com/3229/l60488.png",
            "salediscount": 20,
            "_id": 6126100195377743,
            "brand": "Petzl"
        },
        {
            "merchant": "Eastern Mountain Sports",
            "name": "Petzl Women's Luna Climbing Harness",
            "source": "LinkShare US",
            "url": "http://click.linksynergy.com/link?id=@@@&offerid=303281.7092379756&type=15&murl=http%3A%2F%2Fwww.ems.com%2Fpetzl-womens-luna-climbing-harness%2F20188300018.html",
            "image": "http://www.ems.com/dw/image/v2/AAQU_PRD/on/demandware.static/-/Sites-vestis-master-catalog/default/dw039f2a0c/product/images/1313/562/1313562/1313562_407_main.jpg",
            "brand": "PETZL",
            "finalprice": 5247,
            "currency": "USD",
            "salediscount": 30,
            "_id": 8139700164302780,
            "price": 7495
        }
    ],
    "price_groups": [
        {
            "product_count": 15,
            "max": 7827,
            "min": 5495
        },
        {
            "product_count": 8,
            "max": 10160,
            "min": 7828
        },
        {
            "product_count": 2,
            "max": 12495,
            "min": 10161
        }
    ],
    "time": 4199,
    "networks": [
        {
            "product_count": 2,
            "source": "LinkShare US",
            "group": "LinkShare",
            "source_id": 4,
            "type": "products"
        },
        {
            "product_count": 23,
            "source": "AvantLink US",
            "group": "AvantLink",
            "source_id": 126,
            "type": "products"
        }
    ],
    "duplicates_count": 7,
    "result_count": 25
}
```

`POST https://api.datafeedr.com/search`

Search for products matching specific criteria.

See a list of [queryable Product fields](#product-fields).


### Request Properties

Property | Value | Type | Required
---|---|---|---
`query` | [`Query`](#query-object) Object. | `object`  | Yes
`sort` | An array of fields to sort results by.  Each field should be preceded by `+` for ascending or `-` for descending. Default: relevance | `["+price","..."]` | No
`fields` | Array of `Product` properties to include in the results. Default: all. | `["name","url","..."]` | No
`limit` | Number of results to return. Default: 20 | `integer` | No
`offset` | Offset (for paginating through the results). Default: 0 | `integer` | No
`string_ids` | Encode product ids as strings. Default: false | `boolean` | No
`price_groups` | Number of price groups. Default: 0 | `integer` | No
`exclude_duplicates` | 	 Combination of fields which should be checked for duplicate values, optionally contaning the OR <code>&#124;</code> operator. For example, <code>name image &#124; price</code> excludes products that have the same "name" and either "price" or "image". | `string` | No

### Response Properties

Property | Type | Description
---|---|---
`products` | array | Array of [`Product`](#product-properties) Objects.
`networks` | array | Array of [`Network`](#network-properties) Objects with `product_count` property updated to reflect the number of products included from this network in the search results.
`merchants` | array | Array of [`Merchant`](#merchant-properties) Objects with `product_count` property updated to reflect the number of products included from this merchant in the search results.
`length` | integer | Number of products returned.
`found_count` | integer | Total number of products matching the query.
`result_count` | integer | Number of products that can be retrieved from the server.
`duplicates_count` | integer | Number of products excluded due to the `exclude_duplicates` filter.
`status` | object | [`Status`](#status-properties) Object.
`time` | integer | Time spent processing the API request (in milliseconds).
`version` | string | The current version of the API.











## Search coupons

> Example Coupon Search Request

```shell
curl --request POST \
  --url https://api.datafeedr.com/search \
  --data '{
    "aid": "ACCESS_ID",
    "akey": "ACCESS_KEY",
    "query": [
        "source LIKE coupons",
        "merchant LIKE mountain|outdoor|rei|sports",
        "offerbegin >= 2018-01-01 00:00:00",
        "offerend < 2018-02-01 00:00:00"
    ],
    "fields": ["name", "offerbegin", "offerend", "offercode", "source", "brand", "url", "merchant"],
    "limit": 10
}'
```

```php
<?php

$endpoint = "https://api.datafeedr.com/search";

$data = json_encode([
    'aid'    => 'ACCESS_ID',
    'akey'   => 'ACCESS_KEY',
    'query'  => [
        'source LIKE coupons',
        'merchant LIKE mountain|outdoor|rei|sports',
        'offerbegin >= 2018-01-01 00:00:00',
        'offerend < 2018-02-01 00:00:00'
    ],
    'fields' => ['name', 'offerbegin', 'offerend', 'offercode', 'source', 'brand', 'url', 'merchant'],
    'limit'  => 10
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
    CURLOPT_POSTFIELDS     => $data,
    CURLOPT_HTTPHEADER     => array("Cache-Control: no-cache"),
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

```python
import requests

url = "https://api.datafeedr.com/search"

data = {
    "aid": "ACCESS_ID",
    "akey": "ACCESS_KEY",
    "query": [
        "source LIKE coupons",
        "merchant LIKE mountain|outdoor|rei|sports",
        "offerbegin >= 2018-01-01 00:00:00",
        "offerend < 2018-02-01 00:00:00"
    ],
    "fields": [
        "name",
        "offerbegin",
        "offerend",
        "offercode",
        "source",
        "brand",
        "url",
        "merchant"
      ],
    "limit": 10
}

response = requests.post(url, json=data)
print(response.json())
```

```javascript
var axios = require('axios');

var url = "https://api.datafeedr.com/search";

var data = {
    "aid": "ACCESS_ID",
    "akey": "ACCESS_KEY",
    "query": [
        "source LIKE coupons",
        "merchant LIKE mountain|outdoor|rei|sports",
        "offerbegin >= 2018-01-01 00:00:00",
        "offerend < 2018-02-01 00:00:00"
    ],
    "fields": [
        "name",
        "offerbegin",
        "offerend",
        "offercode",
        "source",
        "brand",
        "url",
        "merchant"
      ],
    "limit": 10
}

axios.post(url, data).then(function (response) {
    console.log(response.data)
});
```

> Example Coupon Search Response

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
        "request_count": 4380,
        "product_count": 456437575,
        "max_length": 100
    },
    "merchants": [
        {
            "product_count": 3,
            "merchant": "Eastern Mountain Sports",
            "merchant_id": 3591,
            "source_id": 8,
            "source": "ShareASale Coupons/Deals"
        },
        {
            "product_count": 2,
            "merchant": "MPG Sport",
            "merchant_id": 11014,
            "source_id": 8,
            "source": "ShareASale Coupons/Deals"
        },
        {
            "product_count": 4,
            "merchant": "Live Well Sports",
            "merchant_id": 34957,
            "source_id": 8,
            "source": "ShareASale Coupons/Deals"
        },
        {
            "product_count": 4,
            "merchant": "Mountain Hardwear",
            "merchant_id": 35721,
            "source_id": 120,
            "source": "Commission Junction Coupons/Deals"
        },
        {
            "product_count": 2,
            "merchant": "Steiner Sports",
            "merchant_id": 44795,
            "source_id": 8,
            "source": "ShareASale Coupons/Deals"
        },
        {
            "product_count": 1,
            "merchant": "Outdoor Tech",
            "merchant_id": 51686,
            "source_id": 9,
            "source": "PepperJam Coupons/Deals"
        },
        {
            "product_count": 1,
            "merchant": "All Outdoor",
            "merchant_id": 75030,
            "source_id": 1362,
            "source": "Awin UK Coupons/Deals"
        },
        {
            "product_count": 21,
            "merchant": "Academy Sports + Outdoor Affiliate",
            "merchant_id": 79604,
            "source_id": 120,
            "source": "Commission Junction Coupons/Deals"
        },
        {
            "product_count": 3,
            "merchant": "Road Runner Sports",
            "merchant_id": 94225,
            "source_id": 127,
            "source": "AvantLink US Coupons/Deals"
        }
    ],
    "version": "0.2",
    "total_found": 41,
    "length": 10,
    "found_count": 41,
    "products": [
        {
            "merchant": "Eastern Mountain Sports",
            "name": "Merchant 17328 - Eastern Mountain Sports - 30% off EMS Men's & Women's Techwick Base Layer! Ends 1/29 - Shop Now and Save!",
            "url": "http://www.shareasale.com/u.cfm?d=476153&m=17328&u=@@@",
            "source": "ShareASale Coupons/Deals",
            "offerbegin": "2018-01-27 00:00:00",
            "offerend": "2018-01-29 00:00:00",
            "_id": 359101729713890
        },
        {
            "merchant": "Eastern Mountain Sports",
            "name": "Merchant 17328 - Eastern Mountain Sports - Shop These Amazing Techwick Sales at EMS! Ends 1/29 - Shop Now and Save!",
            "url": "http://www.shareasale.com/u.cfm?d=476152&m=17328&u=@@@",
            "source": "ShareASale Coupons/Deals",
            "offerbegin": "2018-01-27 00:00:00",
            "offerend": "2018-01-29 00:00:00",
            "_id": 359102103894914
        },
        {
            "merchant": "Eastern Mountain Sports",
            "name": "Merchant 17328 - Eastern Mountain Sports - Up to 50% off EMS Men's & Women's Techwick Dual Thermo 1/4 Zip! Ends 1/29 - Shop Now and Save at EMS!",
            "url": "http://www.shareasale.com/u.cfm?d=476154&m=17328&u=@@@",
            "source": "ShareASale Coupons/Deals",
            "offerbegin": "2018-01-27 00:00:00",
            "offerend": "2018-01-29 00:00:00",
            "_id": 359102105856732
        },
        {
            "merchant": "MPG Sport",
            "name": "Merchant 65207 - MPG Sport - Sale Extended! Up To 72% Off Select Styles + free standard ground US shipping on all orders over $99. Valid 1/14/18-1/29/18",
            "url": "http://www.shareasale.com/u.cfm?d=474382&m=65207&u=@@@",
            "source": "ShareASale Coupons/Deals",
            "offerbegin": "2018-01-14 00:00:00",
            "offerend": "2018-01-29 00:00:00",
            "_id": 1101400170385066
        },
        {
            "merchant": "MPG Sport",
            "name": "Merchant 65207 - MPG Sport - Sale Extended! Up To 76% Off Select Styles + free standard ground US shipping on all orders over $99. Valid 1/14/18-1/29/18",
            "url": "http://www.shareasale.com/u.cfm?d=474383&m=65207&u=@@@",
            "source": "ShareASale Coupons/Deals",
            "offerbegin": "2018-01-14 00:00:00",
            "offerend": "2018-01-29 00:00:00",
            "_id": 1101400212035843
        },
        {
            "offercode": "NEWYEAR5",
            "merchant": "Live Well Sports",
            "name": "Merchant 41405 - Live Well Sports - New Year Sale: Save $5 off $100 at Live Well Sports and Live Well Stores",
            "url": "http://www.shareasale.com/u.cfm?d=472051&m=41405&u=@@@",
            "source": "ShareASale Coupons/Deals",
            "offerbegin": "2018-01-04 00:00:00",
            "offerend": "2018-01-31 00:00:00",
            "_id": 3495700341482322
        },
        {
            "offercode": "NEWYEAR10",
            "merchant": "Live Well Sports",
            "name": "Merchant 41405 - Live Well Sports - New Year Sale: Save $20 off $400 at Live Well Sports and Live Well Stores",
            "url": "http://www.shareasale.com/u.cfm?d=472053&m=41405&u=@@@",
            "source": "ShareASale Coupons/Deals",
            "offerbegin": "2018-01-04 00:00:00",
            "offerend": "2018-01-31 00:00:00",
            "_id": 3495700430050448
        },
        {
            "offercode": "NEWYEAR20",
            "merchant": "Live Well Sports",
            "name": "Merchant 41405 - Live Well Sports - New Year Sale: Save $10 off $200 at Live Well Sports and Live Well Stores",
            "url": "http://www.shareasale.com/u.cfm?d=472052&m=41405&u=@@@",
            "source": "ShareASale Coupons/Deals",
            "offerbegin": "2018-01-04 00:00:00",
            "offerend": "2018-01-31 00:00:00",
            "_id": 3495700910908973
        },
        {
            "offercode": "NEWYEARBIG5",
            "merchant": "Live Well Sports",
            "name": "Merchant 41405 - Live Well Sports - New Year Sale: Save 5% off $1,000 or more at Live Well Sports and Live Well Stores",
            "url": "http://www.shareasale.com/u.cfm?d=472054&m=41405&u=@@@",
            "source": "ShareASale Coupons/Deals",
            "offerbegin": "2018-01-04 00:00:00",
            "offerend": "2018-01-31 00:00:00",
            "_id": 3495701598840274
        },
        {
            "merchant": "Mountain Hardwear",
            "name": "Affiliate Exclusive! 60% Off Select Styles with promo code MHWWINTER60 at MountainHardwear.com! Valid 1/17-1/30.",
            "url": "http://www.anrdoezrs.net/click-@@@-13209172",
            "source": "Commission Junction Coupons/Deals",
            "offerbegin": "2018-01-16 21:00:00",
            "offerend": "2018-01-30 23:45:00",
            "_id": 3572100038651006
        }
    ],
    "time": 579,
    "networks": [
        {
            "product_count": 11,
            "source": "ShareASale Coupons/Deals",
            "group": "ShareASale",
            "source_id": 8,
            "type": "coupons"
        },
        {
            "product_count": 25,
            "source": "Commission Junction Coupons/Deals",
            "group": "Commission Junction",
            "source_id": 120,
            "type": "coupons"
        },
        {
            "product_count": 1,
            "source": "PepperJam Coupons/Deals",
            "group": "PepperJam",
            "source_id": 9,
            "type": "coupons"
        },
        {
            "product_count": 1,
            "source": "Awin UK Coupons/Deals",
            "group": "AffiliateWindow",
            "source_id": 1362,
            "type": "coupons"
        },
        {
            "product_count": 3,
            "source": "AvantLink US Coupons/Deals",
            "group": "AvantLink",
            "source_id": 127,
            "type": "coupons"
        }
    ],
    "result_count": 41
}
```

`POST https://api.datafeedr.com/search`

Search for coupons matching specific criteria.

This calls the same `search` endpoint as a product search. It just queries different  [fields](#product-fields) so that only coupons and deals are returned and regular products are ignored.

See a list of [queryable Product fields](#product-fields).


### Request Properties

Property | Value | Type | Required
---|---|---|---
`query` | [`Query`](#query-object) Object. | `object`  | Yes
`sort` | An array of fields to sort results by.  Each field should be preceded by `+` for ascending or `-` for descending. Default: relevance | `["+price","..."]` | No
`fields` | Array of `Product` properties to include in the results. Default: all. | `["name","url","..."]` | No
`limit` | Number of results to return. Default: 20 | `integer` | No
`offset` | Offset (for paginating through the results). Default: 0 | `integer` | No
`string_ids` | Encode product ids as strings. Default: false | `boolean` | No
`price_groups` | Number of price groups. Default: 0 | `integer` | No
`exclude_duplicates` | 	 Combination of fields which should be checked for duplicate values, optionally contaning the OR <code>&#124;</code> operator. For example, <code>name image &#124; price</code> excludes products that have the same "name" and either "price" or "image". | `string` | No

### Response Properties

Property | Type | Description
---|---|---
`products` | array | Array of [`Product`](#product-properties) Objects.
`networks` | array | Array of [`Network`](#network-properties) Objects with `product_count` property updated to reflect the number of products included from this network in the search results.
`merchants` | array | Array of [`Merchant`](#merchant-properties) Objects with `product_count` property updated to reflect the number of products included from this merchant in the search results.
`length` | integer | Number of products returned.
`found_count` | integer | Total number of products matching the query.
`result_count` | integer | Number of products that can be retrieved from the server.
`duplicates_count` | integer | Number of products excluded due to the `exclude_duplicates` filter.
`status` | object | [`Status`](#status-properties) Object.
`time` | integer | Time spent processing the API request (in milliseconds).
`version` | string | The current version of the API.


