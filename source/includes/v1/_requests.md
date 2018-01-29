# Requests

When making Requests to the Datafeedr API please ensure your Request meets these requirements:

1. **HTTPS Only** - The Datafeedr API will only respond to secured communication over HTTPS. HTTP Requests will be sent a Response containing a `400` HTTP status code.

1. **POST Only** - All Requests to the API should be `POST` Requests.

1. **JSON Only** - All Request parameters should be in [JSON](https://en.wikipedia.org/wiki/JSON) format.

1. **Body Only** - All Request parameters should be sent in the `body` of the `POST`.


## Request Properties

All Requests require an **ACCESS ID** and an **ACCESS KEY**. See [Requirements](#requirements).

Property | Type | Description
---|---|---
`aid` | string | Datafeedr API ACCESS ID.
`akey` | string | Datafeedr API ACCESS KEY.

## Request Example

```shell
curl --request POST \
	--url https://api.datafeedr.com/search \
	--data '{
	"aid": "ACCESS ID",
	"akey": "ACCESS KEY",
	"query": [
		"name LIKE rock climbing harness"
	]
}'
```

Here is an example of a simple product search request which includes an **ACCESS ID** and an **ACCESS KEY** and a `Query` Object containing one condition.
