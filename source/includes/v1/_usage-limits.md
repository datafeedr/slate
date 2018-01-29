# Usage Limits

The number of API Requests you are allowed to make per billing cycle is determined by your Datafeedr subscription plan.

We have different subscription plans for different needs.

A **billing cycle** is 1 month.


## How to find your API Usage

Every successful API Request will return a `Status` object which will contain the following useful properties:

- `request_count` - This is the total number of API Requests you have made since the start of your billing cycle.

- `max_requests` - This is the total number of API Requests you are allowed to make during a billing cycle.


## Billing & API Usage

```json
{
	"type": 3,
	"error": 301,
	"message": "Request limit exceeded"
}
```

If your `request_count` reaches the `max_requests` amount before your billing cycle rolls over, your account **will not** incur any additional charges.

If you use all of your available API Requests for the current billing cycle, a `400` error will be returned along with the following `Error` object on all subsequent API Requests until a new billing cycle starts or your subscription is upgraded to accommodate the additional Requests needed.
