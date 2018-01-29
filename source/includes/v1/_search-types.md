# Search Types

`Product` & `Merchant` Objects have multiple properties that can be used to filter your results.

For example, the `Product` Objects contain a "name" and "price" property which can be queried like this:

```
"name LIKE rock climbing shoes"
"price >= 10000"
```

The search operator you use depends on the type of field you are querying against.

For example, the `LIKE` search operator can be applied to the "name" property but the `IN` operator cannot because the `IN` operator only works with some integer fields.

Likewise, the `<=` operator will work for the "price" property but the `LIKE` property will not because "price" is an integer, not a string. 

Object Properties in the [API Reference](#api-reference) will contain a **Search Type** column indicating the type of search that is available for the property. If no Search Type is listed, the property is not searchable.

The table below defines which Search Operators work with which Search Types.

Search Type | Search Operators (See usage above)
---|---
**TEXT** | `LIKE` `!LIKE` `=` `!=`
**INT** | `=` `!=` `>` `>=` `<` `<=` `IN` `!IN`
**DATE** | `=` `!=` `>` `>=` `<` `<=`
**EMPTY** | `EMPTY`  `!EMPTY`

*All dates are stored in the format `YYYY-MM-DD HH:MM:SS`.*