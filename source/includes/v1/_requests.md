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
	"aid": "ACCESS_ID",
	"akey": "ACCESS_KEY",
	"query": [
		"name LIKE rock climbing harness"
	]
}'
```

```php
<?php

$endpoint = "https://api.datafeedr.com/search";

$data = json_encode([
    'aid'   => 'ACCESS_ID',
    'akey'  => 'ACCESS_KEY',
    'query' => [
        'name LIKE rock climbing harness'
    ]
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
        "name LIKE rock climbing harness"
    ]
}

response = requests.post(url, json=data)
print(response.json())
```

Here is an example of a simple product search Request which includes an **ACCESS ID** and an **ACCESS KEY** and a [`Query`](#query-object) Object containing one [Condition](#conditions).
