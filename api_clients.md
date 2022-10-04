# API Clients

You need an API Client in order to interact with the Ride With GPS API.

```
x-rwgps-api-key: <api_key>
```

## API Versions

Some of our endpoints support versioning, returning different JSON based on the specified version. When you setup your API client, you can choose the default version to use for the response. You can overwrite the default version on a per request basis by including a `x-rwgps-api-version` header in your request:

```
x-rwgps-api-version: 1
```

We currently support versions `0`, `1` and `2`. We recommend you use the latest versions (`2`).
