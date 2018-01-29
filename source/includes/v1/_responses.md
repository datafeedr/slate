# Responses

Each Response sent from the Datafeedr API server will meet these requirements:

1. **JSON Only** - Responses to every Request are sent in [JSON](https://en.wikipedia.org/wiki/JSON) format.

1. **Include HTTP Status Codes** - Responses will contain appropriate [HTTP status codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).


## Successful Responses

Every successful API Request will return a `200` HTTP staus code and include the following properties in the Response in addition to any queried data.

### Response Properties

The common properties returned after making any successful API Request are the following.

Property | Type | Description
---|---|---
`status` | object | `Status` Object (see below).
`time` | integer | Time spent processing the API request (in milliseconds).
`version` | string | The current version of the API.

### Response Example

```json
{
    "status": {
        "network_count": 173,
        "plan_id": 1500,
        "user_id": 100,
        "max_total": 10000,
        "merchant_count": 57898,
        "max_requests": 100000,
        "bill_day": 21,
        "request_count": 2951,
        "product_count": 449069504,
        "max_length": 100
    },
    "version": "0.2",
    "time": 0
}
```

This is an example of what a successful request looks like.


## Unsuccessful Responses

Every unsuccessful API Request will return a `4xx` or `5xx` HTTP status code along with an `Error` object. See [Error Codes](#error-codes) for debugging.

### Response Properties

The default properties of an `Error` object are the following.

Property | Type| Description
---|---|---
`type` | integer| Error type (see **Error Types** table below).
`error` | integer | Error code.
`message` | string | Error message.
`details`| string | Error details.


### Response Example:

```json
{
	"type": 2,
	"error": 202,
	"message": "Invalid access id",
	"details": ""
}
```

This is an example of what a unsuccessful request might look like.


### Error Types

Error types correspond to the type of error encountered during the Request.

Code | Description
---|---
1 | Invalid request error.
2 | Access error.
3 | Limit error.
4 | Malformed query error.
7 | External APIs (Performance Horizon, Zanox) error.
9 | Other error.
