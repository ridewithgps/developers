# Ride with GPS public API

Welcome to the Ride with GPS public API documentation.

Any feedback or question, please contact [developers@ridewithgps.com](mailto:developers@ridewithgps.com).

## Versioning

Our current (and only) API version is `v1` and is available at the `http://ridewithgps.com/api/v1` namespace. Only major, incompatible changes will trigger a version upgrade. We will add new endpoints and keys to existing responses without a version upgrade.

## Formats

The API supports only JSON for requests and responses. To specify JSON, you can either add a `content-type: application/json` header to your requests, or add a `.json` extension to the endpoints you call. The documentation specifies URLs with a `.json` extension.

## API client and authentication

An API client is required for all API requests. To create an API client associated with your user account, go to the [developers tab](https://ridewithgps.com/settings/developers) of your account settings.

Once the API client is created, an API key (`<api_key>`) will be assigned to it.

The prefered method to authenticate is with **OAuth**, which you can configure from your API client management page.

The API also support Basic authentication, using your `<api_key>` for the username and user assigned tokens for the password.

[Read more about authentication](authentication.md)

## API endpoints

The API has endpoints for:

* [Users](endpoints/users.md)
* [Routes](endpoints/routes.md)
* [Trips](endpoints/trips.md)
* [Sync](endpoints/sync.md)

## Webhooks

If you use OAuth for authenticating your users with Ride with GPS, you can also select to receive webhooks. They are sent whenever one of your users manages an asset in their library.

[Read more about webhooks](webhooks.md)

## Responses

API responses always contain a root key named after the requested resource(s):

```javascript
// 200 - OK
{
  "route": {
    "id": 1,
    "name": "Loop around the house",
    // ...
  }
}
```

### Pagination

Some requests (like the routes index request at `/api/v1/routes.json`) support a `?page=<page>` query parameter for pagination. Pagination meta data is included in the response:

```javascript
// GET /api/v1/routes.json?page=1
// 200 - OK
{
  "routes": [
    // ...
  ],
  "meta": {
    "pagination": {
      "record_count": 207,
      "page_count": 11,
      "next_page_url": "https://ridewithgps.com/api/v1/routes.json?page=2"
    }
  }
}
```

* A `null` value of `next_page_url` indicates that you have reached the last page of results.

## Error responses

Successfull requests are responded with either a `200 - OK` or `201 - Created` http status code.

When reporting an error, the API responds with one of the following status codes:

* `404 - Not Found` - the requested resource cannot be found
* `400 - Bad Request` - malformed request
* `401 - Not Authorized` - authentication is required and has failed
* `403 - Forbidden` - authenticated user lacks required permissions
* `500 - Internal Server Error` - an unexpected condition was encountered

In case of errors, the response body also includes a descriptive error message:

```javascript
// 401 - Not Authorized
{
  "error": "Failed to authenticate the user"
}
```
