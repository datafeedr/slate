# Query Object

The Datafeedr API provides a powerful and robust search syntax through the use of the `Query` Object.

A `Query` Object is an array of single **conditions**.


## Conditions

Conditions make it possible to build complex and powerful search queries.

Conditions are `string`s of single "filters". All conditions are *AND*'d together.

### Condition Format

Conditions take the form: `field operator argument(optional)`.

- `field` - An `Object` property name or `ANY` to use any field.
- `operator` - Depends on the field type.
- `argument` - Depends on the field type. Sometimes optional.

Below are a few examples of multiple conditions in a `Query` Object.

*See the [API Reference](#api-reference) for specific examples of the `Query` Object in use.*

### Condition Example #1 - AND'd Conditions

```json
[
	"name LIKE farpoint 55",
	"brand LIKE osprey",
	"onsale = 1"
]
```

In this example we have 3 conditions. The Request will return records that match the following conditions:

- Product name contains the terms "farpoint 55"
- and Product brand contains the term "osprey"
- and Product is on sale.



### Condition Example #2 - Multiple Conditions, Same Field

```json
[
	"description LIKE petzl climbing harness",
	"price > 10000",
	"price < 20000"
]
```

You can also include multiple conditions for the same field.

In this example we have 2 conditions on the same field. The Request will return records that match the following conditions:

- Product description contains the terms "petzl climbing harness"
- and Product price is greater than 100.00
- and Product price is less than 200.00.


### Condition Example #3 - Missing "positive" Condition

```json
[
	"name !LIKE farpoint",
	"source_id !IN 6, 126"
]
```

<aside class="warning">
This Request is invalid.
</aside>

Every `Query` Object should contain at least one "positive" search.

In this example we have 2 conditions but both are "negative". The Request will fail because it doesn't contain at least one "positive" search.


## Fields

As stated [above](#condition-format), conditions take the form:

`field operator argument(optional)`.

At this time, the `Merchant` Object and `Product` Object properties can be used as the `field` values in a condition.

### Merchant Fields

The following fields (properties) of the `Merchant` Object can be used in a condition.

Field | Type | [Search Type](#search-types)
---|---|---
`_id` | integer | **INT**
`name` | string | **TEXT**
`source` | string | **INT**
`source_id` | integer | **TEXT**
`product_count`  | integer | **INT**

### Product Fields

The following fields (properties) of the `Product` Object can be used in a condition.

<aside class="notice">
Not all <code>Product</code> fields listed below exist for every product.
</aside>

Field | Type | [Search Type](#search-types)
---|---|---
`_id` | integer | **INT**
`brand` | string | **TEXT**
`category` | string | **TEXT**
`color` | string | **TEXT**
`currency` | string | **TEXT**
`description` | string | **TEXT**
`direct_url` | string | **EMPTY**
`ean` | string | **TEXT**
`finalprice` | integer | **INT**
`gender` | string | **TEXT**
`htmldescription` | string | **EMPTY**
`image` | string | **EMPTY**
`isbn` | string | **TEXT**
`merchant_id` | integer | **INT**
`merchant`  | string | **TEXT**
`name` | string | **TEXT**
`offerbegin` | timestamp | **DATE**
`offercode` | string | **EMPTY**, **TEXT**
`offerend` | timestamp | **DATE**
`onsale` | integer | **INT**
`price` | integer | **INT**
`salediscount` | integer | **INT**
`saleprice` | integer | **EMPTY**, **INT**
`size` | string | **TEXT**
`sku` | string | **TEXT**
`source_id` | integer | **INT**
`source` | string | **TEXT**
`tags` | string | **TEXT**
`thumbnail` | string | **EMPTY**
`time_updated` | timestamp | **DATE**
`upc` | string | **TEXT**


## Operators

> Search operator examples

```json
"any !LIKE mens"
"name LIKE climbing harness"
"brand LIKE petzl"
"description LIKE big|large"
"tags LIKE climbing"
"category LIKE rock climbing"
"currency = USD"
"finalprice <= 20000"
"onsale = 1"
"direct_url !EMPTY"
"salediscount > 15"
"image !EMPTY"
"time_updated > 2018-01-25 00:00:00"
"source_id IN 126 3 6"
"merchant_id IN 1312 94836 12927"
```

Search operators make it possible to perform specific types of queries on fields.

Operator | Meaning | [Search Type](#search-types) | Argument
---|---|---|---
`EMPTY` | field is empty | **EMPTY** | none, must be omitted
`!EMPTY`| field is not empty | **EMPTY** | none, must be omitted
`LIKE` | fulltext match | **TEXT** | fulltext query
`!LIKE` | fulltext not match | **TEXT** | fulltext query
`=` | strictly equal | **TEXT**, **INT**, **DATE** | `string`, `integer`, `timestamp`
`!=` | strictly not equal | **TEXT**, **INT**, **DATE** | `string`, `integer`, `timestamp`
`>` | more than | **INT**, **DATE** | `integer`, `timestamp`
`>=` | more or equal | **INT**, **DATE** | `integer`, `timestamp`
`<` | less than | **INT**, **DATE** | `integer`, `timestamp`
`<=` | less or equal | **INT**, **DATE** | `integer`, `timestamp`
`IN` | one of | **INT** | comma-separated list of integers
`!IN` | neither of | **INT** | comma-separated list of integers


## Search Types

`Merchant` & `Product` Objects have multiple properties that can be queried.

The search operator you use depends on the type of field you are querying against.

For example, the `LIKE` search operator can be applied to the "name" property but the `IN` operator cannot because the `IN` operator only works with some integer fields.

The table below defines which Search Operators work with which Search Types.

Search Type | Search Operators (See usage above)
---|---
**TEXT** | `LIKE` `!LIKE` `=` `!=`
**INT** | `=` `!=` `>` `>=` `<` `<=` `IN` `!IN`
**DATE** | `=` `!=` `>` `>=` `<` `<=`
**EMPTY** | `EMPTY`  `!EMPTY`

*All dates are stored in the format `YYYY-MM-DD HH:MM:SS`.*

## Fulltext Queries

> Fulltext query examples

```json
"ANY LIKE shoe"
"name LIKE female|woman !mens running shoe"
"name LIKE ^Red =shoe for walking|running"
"description LIKE cheap|inexpensive|affordable"
"brand LIKE =nike"
```

Fields that have a [search type](#search-types) of **TEXT** are available for fulltext search queries.

By default, when searching a text field, all words are *AND*'d together.

For example, the following condition will return all records where the name contains the word "mens" AND "climbing" AND "harness".

`
name LIKE mens climbing harness
`

You can build more powerful search queries using the following operators:

Operator | Example | Meaning
---|---|---
AND | `dog cat` | Return records matching "dog" AND "cat". (Default)
OR | <code>dog&#124;cat</code> | Return records matching "dog" OR "cat".
Phrasal | `"large dogs"` | Return records matching the phrase "large dogs".
Exact | `=running` | Return records matching the exact word "running".
NOT | `!walking` | Exclude records matching "walking".
NOT plus OR | <code>!dog&#124;cat</code> | Exclude records matching "dog" OR "cat".
Starts With | `^black` | Return records where field starts with "black".
Ends With | `white$` | Return records where field ends with "white".
Quorum | `"dog cat bird"/2` | Returns records where at least 2 words match.

### Case Sensitivity

All fulltext searches are case-insensitive therefore `Shoe` and `shoe` produce the same results.

### Stemming

Unless you're using the exact word operator `=`, the fulltext search also matches similar words. For example, `name LIKE nice` also returns products whose name contains `nicely` or `nicer`.
