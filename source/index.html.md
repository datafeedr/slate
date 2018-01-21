---
title: API Reference

// language_tabs:
//   - php: PHP

toc_footers:
  - <a href='http://www.datafeedr.com/pricing' target='_blank'>Sign Up for a Datafeedr API Key</a>
  - <a href='https://github.com/lord/slate' target='_blank'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

The Datafeedr API enables you to directly query our database of 100s of millions of affiliate products from dozen of affiliate networks. Additionally, you can also query 1,000s of coupons or even use our API to query the Amazon API directly.

Currently, the API only supports [JSON](http://en.wikipedia.org/wiki/JSON) as a request and response format.

We currently have one PHP API client library. It can be downloaded [here](https://apidocs.datafeedr.com/php/datafeedr.zip).

All code examples (in the right column) are written for the PHP API client library.
	
# Authentication

```php
<?php

// Require PHP API client library.
require( 'path/to/php/api/client/library/datafeedr.php' );

// Initialize API Connection.
$access_id  = 'QadowZjaABR7Z44PmXKn8NsXA';
$secret_key = 'wnQFCbYtoAvLpZqmXvbPmTWePTXZdW4BdfojXbmQMwirC2i8yfMoUf6jcQZWZEcz';
$api        = new DatafeedrApi( $access_id, $secret_key );
```

> Be sure to replace the **Access ID** and **Secret Key** with your [API keys](https://members.datafeedr.com/).

Authenticate your account when using the API by including your **Access ID** and **Secret Key** in each request. You can purchase and access your API keys in our [member's area](https://members.datafeedr.com/).

Your API keys carry many privileges, so be sure to keep them secret!

To use your API keys, you need only call \Stripe\Stripe::setApiKey() with your key. The PHP library will then automatically send this key in each request.

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

