# Affiliate Links

## Inserting affiliate ID

<aside class="notice">
You must insert your affiliate ID into the URL to get credit for any referrals.
</aside>

> Example of "url" and "ref_url" fields in a Product Object.

```json
"name": "Black Diamond Women's Solution Climbing Harness",
"url": "http://classic.avantlink.com/click.php?p=199519&pw=@@@&pt=3&pri=60466&tt=df",
"ref_url": "http://classic.avantlink.com/click.php?p=199519&pw=@@@&pt=3&pri=60466&tt=df&ctc=###",
"source": "AvantLink US",
"source_id": 126,
```

In order to get credit for any sales you refer to a merchant you **MUST** insert your affiliate ID into the `url` or `ref_url` field of a [`Product`](#product-properties).

A `Product` Object will contain a `url` field and usually a `ref_url` field.

Both fields contain URLs with the characters `@@@` in the URL. You must replace `@@@` with your affiliate ID from the respective affiliate network. Replacing `@@@` is 	**REQUIRED**.

If an affiliate network allows sub-tracking, then a `ref_url` field will also be present and the URL in that field will contain the `###` characters. This can be used to pass additional tracking data to the affiliate network. Replacing `###` with a sub-tracking value is **OPTIONAL**.

If you do not need to do sub-tracking the you should use the `url` field.

If you need help finding your affiliate IDs, check [our documentation](https://datafeedrapi.helpscoutdocs.com/category/183-networks-merchants).




## Zanox Affiliate IDs

Zanox handles affiliate IDs differently than most other affiliate networks.

Instead of providing a static affiliate ID that can simply be inserted into your URLs, an affiliate ID must be dynamically generated.

You must get your Zanox `zmid` value for each Zanox merchant.

The `@@@` characters in the URL are replaced with the `zmid` value.

See the [Get Zanox affiliate ID](#get-zanox-affiliate-id) section to learn how to get your Zanox `zmid` value to insert in your product URLs.




## Performance Horizon Affiliate IDs

Performance Horizon handles affiliate IDs differently than most other affiliate networks.

Instead of providing a static affiliate ID that can simply be inserted into your URLs, an affiliate ID must be dynamically generated.

You must get your Performance Horizon `camref` value for each Performance Horizon merchant.

The `@@@` characters in the URL are replaced with the `camref` value.

See the [Get Performance Horizon camref](#get-performance-horizon-camref) section to learn how to get your Performance Horizon `camref` value to insert in your product URLs.

