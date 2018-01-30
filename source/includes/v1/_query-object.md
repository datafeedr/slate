# Query Object

```json
"query": [
  "condition 1",
  "condition 2",
  "condition 3"
]
```

The Datafeedr API provides a powerful and robust search syntax through the use of the `Query` Object.

A `Query` Object is an array of single **Conditions**.


## Conditions

Conditions make it possible to build complex and powerful search queries.

- Conditions are essentially "filters".
- Each Condition is a single filter.
- All Conditions are of the type `string`.
- All Conditions are *AND*'d together.

### Condition Format

Conditions take the form: `field operator argument(optional)`.

- `field` - An `Object` property name or `ANY` to use any field. [See Fields](#fields)
- `operator` - Depends on the field type. [See Operators](#search-operators)
- `argument` - Depends on the field type. Sometimes optional.

Below are a few examples of multiple conditions in a `Query` Object.

*See the [API Reference](#api-reference) for specific examples of the `Query` Object in use.*

### Condition Example #1 - AND'd Conditions

```json
"query": [
	"name LIKE farpoint 55",
	"brand LIKE osprey",
	"onsale = 1"
]
```

In this example we have 3 Conditions. The Request will return records that match the following Conditions:

- Product name contains the terms "farpoint 55"
- and Product brand contains the term "osprey"
- and Product is on sale.



### Condition Example #2 - Multiple Conditions, Same Field

```json
"query": [
	"ANY LIKE petzl climbing harness",
	"price > 10000",
	"price < 20000"
]
```

You can also include multiple Conditions for the same field.

In this example we have 2 Conditions on the same field. The Request will return records that match the following Conditions:

- ANY field contains the terms "petzl climbing harness"
- and Product price is greater than 100.00
- and Product price is less than 200.00.


### Condition Example #3 - Missing "positive" Condition

```json
"query": [
	"name !LIKE farpoint",
	"source_id !IN 6, 126"
]
```

<aside class="warning">
This Request is invalid.
</aside>

Every `Query` Object should contain at least one "positive" search.

In this example we have 2 Conditions but both are "negative". The Request will fail because it doesn't contain at least one "positive" Condition.


## Fields

As stated [above](#condition-format), Conditions take the form:

`field operator argument(optional)`.

At this time, the [`Merchant`](#merchant-properties) Object and [`Product`](#product-properties) Object properties can be used as the `field` values in a Condition.

### Merchant Fields

> Example of Merchant field usage

```json
"query": [
  "name LIKE magazines|=books",
  "source LIKE coupons",
  "source_id !IN 123",
  "product_count > 5"
]
```

The following [`Merchant`](#merchant-properties) Object fields (properties) can be used in a Condition.

Field | Type | [Query Type](#query-types)
---|---|---
`id` | integer | **INT**
`name` | string | **TEXT**
`source` | string | **TEXT**
`source_id` | integer | **INT**
`product_count`  | integer | **INT**

### Product Fields


> Example of Product field usage

```json
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
]
```

The following [`Product`](#product-properties) Object fields (properties) can be used in a Condition.

<aside class="notice">
Not all <code>Product</code> fields listed below exist for every product.
</aside>

Field | Type | [Query Type](#query-types)
---|---|---
`id` | integer | **INT**
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


## Search Operators

> Search operator examples

```json
"query": [
  "any !LIKE mens",
  "name LIKE climbing harness",
  "brand LIKE petzl",
  "description LIKE big|large",
  "tags LIKE climbing",
  "category LIKE rock climbing",
  "currency = USD",
  "finalprice <= 20000",
  "onsale = 1",
  "direct_url !EMPTY",
  "salediscount > 15",
  "image !EMPTY",
  "time_updated > 2018-01-25 00:00:00",
  "source_id IN 126 3 6",
  "merchant_id IN 1312 94836 12927"
]
```

Search operators make it possible to perform specific types of queries on fields. Which operator you choose depends on the allowed [Query Type(s)](#query-types) for that field.

Operator | Meaning | Argument | Example
---|---|---|---
`EMPTY` | field is empty | none, must be omitted | `saleprice EMPTY`
`!EMPTY`| field is not empty | none, must be omitted | `image !EMPTY`
`LIKE` | fulltext match | fulltext query | `name LIKE iphone`
`!LIKE` | fulltext not match | fulltext query | `brand !LIKE apple`
`=` | strictly equal | `string`, `integer`, `timestamp` | `currency = USD`
`!=` | strictly not equal | `string`, `integer`, `timestamp` | `currency != CAD`
`>` | more than | `integer`, `timestamp` | `price > 10000`
`>=` | more or equal | `integer`, `timestamp` | `salediscount >= 25`
`<` | less than | `integer`, `timestamp` | `finalprice < 10000`
`<=` | less or equal | `integer`, `timestamp` | `offerbegin <= 2018-01-11 00:00:00`
`IN` | one of | comma-separated list of integers | `merchant_id IN 123, 456`
`!IN` | neither of | comma-separated list of integers | `source_id !IN 321, 654`


## Query Types

[`Merchant`](#merchant-properties) & [`Product`](#product-properties) Objects have many properties that can be queried. See a list of all [supported fields](#fields).

The [search operator](#search-operators) you use depends on the type of field you are querying against.

For example, the `LIKE` search operator can be applied to the "**name**" property but the `IN` operator cannot because the `IN` operator only works with integer fields.

The table below defines which [search operator](#search-operators) work with which Query Types.

Query Type | [Search Operators](#search-operators)
---|---
**TEXT** | `LIKE` `!LIKE` `=` `!=`
**INT** | `=` `!=` `>` `>=` `<` `<=` `IN` `!IN`
**DATE** | `=` `!=` `>` `>=` `<` `<=`
**EMPTY** | `EMPTY`  `!EMPTY`

*All dates are stored in the format `YYYY-MM-DD HH:MM:SS` in UTC*

## Fulltext Queries

> Fulltext query examples

```json
"query": [
  "ANY LIKE shoe",
  "name LIKE female|woman !mens running shoe",
  "name LIKE ^Red =shoe for walking|running",
  "description LIKE cheap|inexpensive|affordable",
  "brand LIKE =nike"
]
```

Fields that have a [Query Type](#query-types) of **TEXT** are also available for fulltext search queries.

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
Quorum | `"dog cat bird"/~2` | Returns records where at least 2 words match.

### Case Sensitivity

All fulltext searches are case-insensitive therefore `Shoe` and `shoe` produce the same results.

### Stemming

Unless you're using the exact word operator `=`, the fulltext search also matches similar words. For example, `name LIKE nice` also returns products whose name contains `nicely` or `nicer`.
