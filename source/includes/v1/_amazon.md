# Amazon Item Search


The `amazon_item_search` endpoint returns product data from Amazon matching your search.


## Amazon Product properties

The Amazon `Product` Object contains information about a single Product.


### Amazon `Product` Object Properties

The following properties can be found in the Amazon `Product` Object.

Property | Type | Description
---|---|---
`_id` | integer | Product ID (different than ASIN).
`asin` | string | [Amazon Standard Identification Number](https://en.wikipedia.org/wiki/Amazon_Standard_Identification_Number)
`brand` | string | Product brand.
`category` | string | Category field(s) product is in.
`currency` | string | Three letter ISO-4217 currency code.
`description` | string | Product description.
`finalprice` | integer | Lowest price of product (either sale or regular price) in least valued currency units (e.g cents).
`image` | string | Product image URL.
`merchant_id` | integer | Merchant ID.
`merchant`  | string | Merchant name.
`model` | string | Model number.
`name` | string | Product name.
`onsale` | integer | Indicates if product is on sale. 0=No, 1=Yes.
`price` | integer | Price of product in least valued currency units (e.g cents).
`salediscount` | integer | The percentage that price has been discounted in whole numbers.
`source_id` | integer | Affiliate network ID.
`source` | string | Affiliate network name.
`thumbnail` | string | Product image thumbnail.
`url` | string | Affiliate URL.



## Search Amazon products

> Example Amazon Product Search Request

```shell
curl --request POST \
  --url https://api.datafeedr.com/amazon_item_search \
  --data '{
    "aid": "ACCESS_ID",
    "akey": "ACCESS_KEY",
    "AssociateTag": "AMAZON_TRACKING_ID",
    "AWSAccessKeyId": "AMAZON_ACCESS_KEY",
    "AWSSecretKey": "AMAZON_SECRET_KEY",
    "SearchIndex": "SportingGoods",
    "Keywords": "osprey farpoint 55"
}'
```

```php
<?php

$url = "https://api.datafeedr.com/amazon_item_search";

$data = json_encode( [
    'aid'            => 'ACCESS_ID',
    'akey'           => 'ACCESS_KEY',
    'AssociateTag'   => 'AMAZON_TRACKING_ID',
    'AWSAccessKeyId' => 'AMAZON_ACCESS_KEY',
    'AWSSecretKey'   => 'AMAZON_SECRET_KEY',
    'SearchIndex'    => 'SportingGoods',
    'Keywords'       => 'osprey farpoint 55'
] );

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

url = "https://api.datafeedr.com/amazon_item_search"

data = {
    "aid": "ACCESS_ID",
    "akey": "ACCESS_KEY",
    "AssociateTag": "AMAZON_TRACKING_ID",
    "AWSAccessKeyId": "AMAZON_ACCESS_KEY",
    "AWSSecretKey": "AMAZON_SECRET_KEY",
    "SearchIndex": "SportingGoods",
    "Keywords": "osprey farpoint 55"
}

response = requests.post(url, json=data)
print(response.json())
```

```javascript
var axios = require('axios');

var url = "https://api.datafeedr.com/amazon_item_search";

var data = {
    "aid": "ACCESS_ID",
    "akey": "ACCESS_KEY",
    "AssociateTag": "AMAZON_TRACKING_ID",
    "AWSAccessKeyId": "AMAZON_ACCESS_KEY",
    "AWSSecretKey": "AMAZON_SECRET_KEY",
    "SearchIndex": "SportingGoods",
    "Keywords": "osprey farpoint 55"
};

axios.post(url, data).then(function (response) {
    console.log(response.data)
});
```

> Example Amazon Product Search Response

```json
{
    "total_found": 19,
    "status": {
        "network_count": 173,
        "plan_id": 10300,
        "user_id": 190,
        "max_total": 10000,
        "merchant_count": 58256,
        "max_requests": 100000,
        "bill_day": 16,
        "request_count": 9125,
        "product_count": 441097498,
        "max_length": 100
    },
    "found_count": 19,
    "products": [
        {
            "category": "Clothing, Shoes & Jewelry > Departments > Men > Shops; Clothing, Shoes & Jewelry > Departments > Luggage & Travel Gear > Backpacks > Casual Daypacks",
            "asin": "B019UTHYNC",
            "merchant_id": 7777,
            "name": "Osprey Farpoint 55 Travel Backpack",
            "merchant": "Amazon United States",
            "suid": "B019UTHYNC",
            "url": "https://www.amazon.com/Osprey-Farpoint-55-Travel-Backpack/dp/B019UTHYNC?SubscriptionId=AKIAJLHNSP4DNCDHN5HQ&tag=@@@&linkCode=xm2&camp=2025&creative=165953&creativeASIN=B019UTHYNC",
            "price": 16995,
            "brand": "Osprey",
            "finalprice": 16995,
            "_id": 777758772250847,
            "currency": "USD",
            "source": "Amazon United States",
            "image": "https://images-na.ssl-images-amazon.com/images/I/41i5ig38EJL.jpg",
            "salediscount": 0,
            "onsale": 0,
            "model": "10000291-P",
            "source_id": 7777,
            "thumbnail": "https://images-na.ssl-images-amazon.com/images/I/41i5ig38EJL._SL160_.jpg",
            "description": "Osprey's Far point 55 is the perfect companion for a long weekend. Feel free to add an extra sweater and a pair of waterproof boots; this pack is designed to handle loads up to 50 pounds. The Light Wire frame suspension transfers the load from harness to hip belt. A mesh back panel improves ventilation and the mesh on the harness and hip belt reduces chafing under load. The entire suspension stows away under a zippered panel creating a sleek silhouette for transport. Unzip the lockable sliders to access the main compartment. Inside there's a mesh pocket for small items. Dual compression straps keep cargo from shifting during transit. Outside you'll find a zippered front panel slash pocket to keep you organized and sewn attachment points to lash on extra gear. No matter how much you choose to carry, dual compression straps stabilize the load. The main Far point 55 pack comes with a detachable Far point daypack to carry the essential for a hike in the hills or an excursion downtown."
        },
        {
            "category": "Clothing, Shoes & Jewelry > Departments > Men > Shops; Clothing, Shoes & Jewelry > Departments > Luggage & Travel Gear > Backpacks > Casual Daypacks",
            "asin": "B00XN1T1NK",
            "merchant_id": 7777,
            "name": "Osprey Men's Atmos 50 AG Backpacks",
            "merchant": "Amazon United States",
            "suid": "B00XN1T1NK",
            "url": "https://www.amazon.com/Osprey-Mens-Atmos-50-Backpacks/dp/B00XN1T1NK?SubscriptionId=AKIAJLHNSP4DNCDHN5HQ&tag=@@@&linkCode=xm2&camp=2025&creative=165953&creativeASIN=B00XN1T1NK",
            "price": 13800,
            "brand": "Osprey",
            "finalprice": 13800,
            "_id": 777753704914444,
            "currency": "USD",
            "source": "Amazon United States",
            "image": "https://images-na.ssl-images-amazon.com/images/I/41mmJZPmFkL.jpg",
            "salediscount": 0,
            "onsale": 0,
            "model": "015250-705-3-LG-saParent",
            "source_id": 7777,
            "thumbnail": "https://images-na.ssl-images-amazon.com/images/I/41mmJZPmFkL._SL160_.jpg",
            "description": "FEATURES of the Osprey Atmos 50 AG Pack Floating, extendable top lid can be removed to save weight FlapJacket provides compression and protection for the main pack when the lid is removed Dual ice tool loops Removable sleeping pad straps provide secure gear attachment when needed Dual zippered front panel pockets provide quick access storage Adjustable harness allows you to easily adjust the torso length Compression straps stabilize pack loads Stow-on-the-Go trekking pole attachment makes for quick and easy storage Fit-on-the-Fly hipbelt extends hipbelt by 5 inches, giving you a custom fit Suspended mesh hip wrap for load transfer and comfort Anti-gravity backpanel made of lightweight mesh provides comfort and ventilation Internal compression Internal reservoir sleeve"
        },
        {
            "category": "Sports & Outdoors > Outdoor Recreation Features; Clothing, Shoes & Jewelry > Departments > Luggage & Travel Gear > Gym Bags",
            "asin": "B071YK4317",
            "merchant_id": 7777,
            "name": "OSPREY Porter 46 Travel",
            "merchant": "Amazon United States",
            "suid": "B071YK4317",
            "url": "https://www.amazon.com/Osprey-10001115-OSPREY-Porter-Travel/dp/B071YK4317?SubscriptionId=AKIAJLHNSP4DNCDHN5HQ&tag=@@@&linkCode=xm2&camp=2025&creative=165953&creativeASIN=B071YK4317",
            "price": 13000,
            "brand": "Osprey",
            "finalprice": 13000,
            "_id": 777764025911987,
            "currency": "USD",
            "source": "Amazon United States",
            "image": "https://images-na.ssl-images-amazon.com/images/I/41xWr+OiEeL.jpg",
            "salediscount": 0,
            "onsale": 0,
            "model": "10001115",
            "source_id": 7777,
            "thumbnail": "https://images-na.ssl-images-amazon.com/images/I/41xWr+OiEeL._SL160_.jpg",
            "description": "With padded sidewalls, convenient organization and a substantial suspension for backpack-style carry that disappears when checking bags, the Porter Series has set the standard for deluxe duffels. This season brings a relocated and dedicated zippered laptop and tablet pocket-and functional storage options for items both big and small-with multiple access points. When a duffel isn't enough and backpacking bags are too much, the Porter is the answer."
        },
        {
            "category": "Sports & Outdoors > Categories > Outdoor Recreation > Camping & Hiking > Backpacks & Bags; Sports & Outdoors > Outdoor Recreation Features",
            "asin": "B019UTHQEY",
            "merchant_id": 7777,
            "name": "Osprey Farpoint 40 Travel Backpack",
            "merchant": "Amazon United States",
            "suid": "B019UTHQEY",
            "url": "https://www.amazon.com/Osprey-Farpoint-40-Travel-Backpack/dp/B019UTHQEY?SubscriptionId=AKIAJLHNSP4DNCDHN5HQ&tag=@@@&linkCode=xm2&camp=2025&creative=165953&creativeASIN=B019UTHQEY",
            "price": 14584,
            "brand": "Osprey",
            "finalprice": 14584,
            "_id": 777701271729346,
            "currency": "USD",
            "source": "Amazon United States",
            "image": "https://images-na.ssl-images-amazon.com/images/I/411shEqQcWL.jpg",
            "salediscount": 0,
            "onsale": 0,
            "model": "10000297-P",
            "source_id": 7777,
            "thumbnail": "https://images-na.ssl-images-amazon.com/images/I/411shEqQcWL._SL160_.jpg",
            "description": "Osprey's far point 40 is perfect for a weekend getaway in the city or the wilderness. The lightwood frame suspension transfers the load from harness to hip belt. A mesh back panel improves ventilation and the mesh on the harness and hip belt reduces chafing under load. The entire suspension stows away under a zippered panel creating a sleek silhouette for transport. Unzip the lockable sliders to access the main compartment. Inside there's a mesh pocket for small items. Dual compression straps keep cargo from shifting during Transit. Outside you'll find a zippered front panel slash pocket to keep you organized and sewn attachment points to lash on extra gear. No matter how much you choose to carry, dual compression straps stabilize the load. The padded top and side handles give you purchase when you need to toss the far point 40 into the back of the bus."
        },
        {
            "category": "Sports & Outdoors > Categories > Outdoor Recreation > Camping & Hiking > Backpacks & Bags > Backpacking Packs > Hiking Daypacks; Sports & Outdoors > Outdoor Recreation Features",
            "asin": "B019UTI40Y",
            "merchant_id": 7777,
            "name": "Osprey Packs Farpoint 70 Travel Backpack",
            "merchant": "Amazon United States",
            "suid": "B019UTI40Y",
            "url": "https://www.amazon.com/Osprey-Packs-Farpoint-Travel-Backpack/dp/B019UTI40Y?SubscriptionId=AKIAJLHNSP4DNCDHN5HQ&tag=@@@&linkCode=xm2&camp=2025&creative=165953&creativeASIN=B019UTI40Y",
            "price": 18771,
            "brand": "Osprey",
            "finalprice": 18771,
            "_id": 777703788917358,
            "currency": "USD",
            "source": "Amazon United States",
            "image": "https://images-na.ssl-images-amazon.com/images/I/4150EVVTVIL.jpg",
            "salediscount": 0,
            "onsale": 0,
            "model": "10000285-P",
            "source_id": 7777,
            "thumbnail": "https://images-na.ssl-images-amazon.com/images/I/4150EVVTVIL._SL160_.jpg",
            "description": "From the streets of Buenos Aires to the foothills of the Andes, Osprey’s Farpoint 70 is ready for anything. Go ahead and fill it up with heavy mountain gear. The LightWire frame suspension transfers the load from harness to hipbelt. A mesh backpanel improves ventilation and the mesh on the harness and hipbelt reduces chafing under load. The entire suspension stows away under a zippered panel creating a sleek silhouette for transport. Unzip the lockable sliders to access the main compartment. Inside there’s a mesh pocket for small items. Dual compression straps keep cargo from shifting during transit. Outside you’ll find a zippered front panel slash pocket to keep you organized and sewn attachment points to lash on extra gear. No matter how much you choose to carry, StraightJacket compression straps stabilize the load. The main Farpoint 70 pack comes with a detachable Farpoint day pack, perfect for use on trips to the local market or to recon your route from the high ridge above base camp."
        },
        {
            "category": "Electronics > Categories > Computers & Accessories > Laptop Accessories > Bags, Cases & Sleeves > Backpacks",
            "asin": "B019UTI8W8",
            "merchant_id": 7777,
            "name": "Osprey Packs Farpoint 80 Travel Backpack",
            "merchant": "Amazon United States",
            "suid": "B019UTI8W8",
            "url": "https://www.amazon.com/Osprey-Packs-Farpoint-Travel-Backpack/dp/B019UTI8W8?SubscriptionId=AKIAJLHNSP4DNCDHN5HQ&tag=@@@&linkCode=xm2&camp=2025&creative=165953&creativeASIN=B019UTI8W8",
            "price": 14000,
            "brand": "Osprey",
            "finalprice": 14000,
            "_id": 777772448139997,
            "currency": "USD",
            "source": "Amazon United States",
            "image": "https://images-na.ssl-images-amazon.com/images/I/51I9ltXCZOL.jpg",
            "salediscount": 0,
            "onsale": 0,
            "model": "10000279-P",
            "source_id": 7777,
            "thumbnail": "https://images-na.ssl-images-amazon.com/images/I/51I9ltXCZOL._SL160_.jpg",
            "description": "Osprey's far point 80 is the right size for a long trip when you need one pack to transport everything from the airport to the back and beyond. Go ahead and fill it up. The lightwood frame suspension transfers the load from harness to hip belt. A mesh back panel improves ventilation and the mesh on the harness and hip belt reduces chafing under load. The entire suspension stows away under a zippered panel creating a sleek silhouette for transport. Unzip the lockable sliders to access the main compartment. Inside there's a mesh pocket for small items. A compartment with floating divider allows separate storage options and dual compression straps keep cargo from shifting during Transit. Outside the pack, you'll find a zippered front panel slash pocket to keep your organized and sewn attachment points to add extra gear. No matter how much you choose to carry, straightjacket compression straps stabilize the load. There are also loops to anchor an optional osprey day Lite day pack if you would like the convenience of a small satellite pack for short forays."
        },
        {
            "category": "Sports & Outdoors > Categories > Outdoor Recreation > Camping & Hiking > Backpacks & Bags > Backpacking Packs > Internal Frame Backpacks; Sports & Outdoors > Outdoor Recreation Features",
            "asin": "B017P6F3NU",
            "merchant_id": 7777,
            "name": "Osprey Women's Aura 65 AG Backpacks",
            "merchant": "Amazon United States",
            "suid": "B017P6F3NU",
            "url": "https://www.amazon.com/Osprey-Womens-Aura-65-Backpacks/dp/B017P6F3NU?SubscriptionId=AKIAJLHNSP4DNCDHN5HQ&tag=@@@&linkCode=xm2&camp=2025&creative=165953&creativeASIN=B017P6F3NU",
            "price": 13995,
            "finalprice": 13995,
            "_id": 777711206462598,
            "currency": "USD",
            "source": "Amazon United States",
            "salediscount": 0,
            "onsale": 0,
            "model": "025265-706-3-WM",
            "source_id": 7777,
            "brand": "Osprey",
            "description": "FEATURES of the Osprey Women's Aura 65 AG Pack Adjustable harness Compression straps Dual zippered front panel pockets Fit-on-the-Fly hipbelt FlapJacket Internal compression Internal reservoir sleeve Removable floating top lid Removable sleeping pad straps Sleeping bag compartment Stow-on-the-Go trekking pole attachment Tool attachment"
        },
        {
            "category": "Sports & Outdoors > Categories > Outdoor Recreation > Camping & Hiking > Backpacks & Bags > Backpacking Packs > Hydration Packs; Sports & Outdoors > Outdoor Recreation Features",
            "asin": "B073QQR4C1",
            "merchant_id": 7777,
            "name": "Osprey Packs Fairview 40 Travel Backpack",
            "merchant": "Amazon United States",
            "suid": "B073QQR4C1",
            "url": "https://www.amazon.com/Osprey-Packs-Fairview-Travel-Backpack/dp/B073QQR4C1?SubscriptionId=AKIAJLHNSP4DNCDHN5HQ&tag=@@@&linkCode=xm2&camp=2025&creative=165953&creativeASIN=B073QQR4C1",
            "price": 14284,
            "brand": "Osprey",
            "finalprice": 14284,
            "_id": 777713351217328,
            "currency": "USD",
            "source": "Amazon United States",
            "image": "https://images-na.ssl-images-amazon.com/images/I/41rtJQfnanL.jpg",
            "salediscount": 0,
            "onsale": 0,
            "model": "10001133",
            "source_id": 7777,
            "thumbnail": "https://images-na.ssl-images-amazon.com/images/I/41rtJQfnanL._SL160_.jpg",
            "description": "KEY FEATURES Traditional backpack construction helps you support and carry the heaviest loads Stowaway Harness and Hipbelt can be zipped away when not in use to prevent snags and hangups Lightweight 210D Nylon Ripstop construction doesnt compromise on durability thanks to 600D Packcloth reinforcement in high wear areas The Osprey Fairview 40 Womens Bag is how you bring backcountry tech on every adventure you go on even the ones that never leave the city The LightWire? frame supports and distributes just like your trail pack would and the Atilon Foam harness and hipbelt keep you comfortable even under heavy loads But when its time to turn your bag over to the baggage handlers at the airport or if you just want a more standard looking piece of luggage simply zip shut the back panel for a sleek snag free carrying option SPECSVolume Liters 40"
        },
        {
            "category": "Clothing, Shoes & Jewelry > Departments > Luggage & Travel Gear > Backpacks",
            "asin": "B00U3N8NAI",
            "merchant_id": 7777,
            "name": "Osprey UltraLight Raincover",
            "merchant": "Amazon United States",
            "suid": "B00U3N8NAI",
            "url": "https://www.amazon.com/Osprey-234102-514-1-LG-P-UltraLight-Raincover/dp/B00U3N8NAI?SubscriptionId=AKIAJLHNSP4DNCDHN5HQ&tag=@@@&linkCode=xm2&camp=2025&creative=165953&creativeASIN=B00U3N8NAI",
            "price": 2400,
            "brand": "Osprey",
            "finalprice": 2400,
            "_id": 777760229864481,
            "currency": "USD",
            "source": "Amazon United States",
            "image": "https://images-na.ssl-images-amazon.com/images/I/51qQRM7RKnL.jpg",
            "salediscount": 0,
            "onsale": 0,
            "model": "234102-514-1-LG-P",
            "source_id": 7777,
            "htmldescription": "Features:<br /><ul><li>Osprey raincover</li><li>Designed to protect 75-110 litre pack</li><li>Crafted with a fully taped lightweight fabric</li><li>Packs down into its own stuffsack</li><li>Reflective graphic printing</li><li><b>Volume Range:</b> 75-110 litres</li><li><b>Weight:</b> 0.1kg</li><li>Pack is securely locked into place with a lightweight wrap around cinch strap and secure hip belt and harness attachment</li></ul><br />",
            "thumbnail": "https://images-na.ssl-images-amazon.com/images/I/51qQRM7RKnL._SL160_.jpg",
            "description": "Features:\nOsprey raincover\nDesigned to protect 75-110 litre pack\nCrafted with a fully taped lightweight fabric\nPacks down into its own stuffsack\nReflective graphic printing\nVolume Range: 75-110 litres\nWeight: 0.1kg\nPack is securely locked into place with a lightweight wrap around cinch strap and secure hip belt and harness attachment"
        },
        {
            "category": "Clothing, Shoes & Jewelry > Departments > Luggage & Travel Gear > Gym Bags > Sports Duffels",
            "asin": "B00OKE6GEQ",
            "merchant_id": 7777,
            "name": "Osprey Porter 65 Travel Duffel Bag",
            "merchant": "Amazon United States",
            "suid": "B00OKE6GEQ",
            "url": "https://www.amazon.com/Osprey-Porter-Travel-Duffel-Bag/dp/B00OKE6GEQ?SubscriptionId=AKIAJLHNSP4DNCDHN5HQ&tag=@@@&linkCode=xm2&camp=2025&creative=165953&creativeASIN=B00OKE6GEQ",
            "price": 10000,
            "brand": "Osprey",
            "finalprice": 10000,
            "_id": 777706568763210,
            "currency": "USD",
            "source": "Amazon United States",
            "image": "https://images-na.ssl-images-amazon.com/images/I/31P2Dh6D1gL.jpg",
            "salediscount": 0,
            "onsale": 0,
            "model": "877257037116-PARENT",
            "source_id": 7777,
            "thumbnail": "https://images-na.ssl-images-amazon.com/images/I/31P2Dh6D1gL._SL160_.jpg",
            "description": "With comfortable shoulder straps and waist belt that quickly tuck away when not needed, the Osprey Porter 65 conversion pack effortlessly distills the essence of a travel pack into its lightest, cleanest form for travelers who prefer to keep things simple. Updated with better organization features and a padded laptop compartment."
        }
    ],
    "version": "0.2",
    "time": 179,
    "result_count": 10
}
```

`POST https://api.datafeedr.com/amazon_item_search`

<aside class="notice">
This request does require your <code>AWSSecretKey</code> which is used to sign the request. We do not store your key in any way.
</aside>


### Request Properties

Property | Value | Type | Required
---|---|---|---
`AssociateTag` | [More information](https://docs.aws.amazon.com/AWSECommerceService/latest/DG/CommonRequestParameters.html) | `string`  | Yes
`AWSAccessKeyId` | [More information](https://docs.aws.amazon.com/AWSECommerceService/latest/DG/CommonRequestParameters.html) | `string` | Yes
`AWSSecretKey` | [More information](https://docs.aws.amazon.com/AWSECommerceService/latest/DG/ViewingCredentials.html) | `string` | Yes
Search Parameter | At least one [search parameter](https://docs.aws.amazon.com/AWSECommerceService/latest/DG/ItemSearch.html#ItemSearch-rp). | `string` | Yes
`SearchIndex` | [More information](https://docs.aws.amazon.com/AWSECommerceService/latest/DG/localevalues.html) | `string` | No
`ItemPage` | Offset (for paginating through results). Default: 1 | `integer` | No
`Locale` | `CA` `CN` `DE` `ES` `FR` `IT` `JP` `UK` or `US`. Default: `US` | `string` | No
`Sort` | One of the following [sort values](https://docs.aws.amazon.com/AWSECommerceService/latest/DG/APPNDX_SortValuesArticle.html)| `string` | No

### Response Properties

Property | Type | Description
---|---|---
`products` | array | Array of Amazon [`Product`](#amazon-product-properties) Objects.
`found_count` | integer | Total number of products matching the query.
`result_count` | integer | Number of products that can be retrieved from the server.
`status` | object | [`Status`](#status-properties) Object.
`time` | integer | Time spent processing the API request (in milliseconds).
`version` | string | The current version of the API.
