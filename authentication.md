# Authentication

Most requests made to the API must be authenticated. The API supports 2 shemes for authentication: OAuth and Basic Authentication.

We strongly recommend that you use OAuth. Use basic authentication if you are the only user of your application.

## Oauth authentication

Ride with GPS is an OAuth provider, and we recommend that you use OAuth if you plan authenticate users others than yourself. The workflow is secure, and does not require users to share their Ride with GPS password with you.

### Configuration

From the [developer settings page](https://ridewithgps.com/settings/developers) of your account, create or update an API client and specify one or more Redirect URIs (`redirect_uri`) pointing to endpoints you own. Your API client will then be setup for OAuth and its management page will display your OAuth client ID (`client_id`) and secret (`client_secret`). Never share those with anyone.

### Authorization flow

### 1. Authorize

Your application links your user to the authorization web page hosted on the Ride with GPS website:

```html
<a href="https://ridewithgps.com/oauth/authorize
  ?client_id=[client_id]
  &redirect_uri=[redirect_uri]
  &response_type=code">
  Login on Ride with GPS
</a>
```

Where:

* `redirect_uri` must match one of the OAuth recirect URIs configured for your API Client
* `client_id` is the OAuth client ID for your API Client

The user will be presented with the following interface:

![OAuth Authorize interface](images/oauth_authorize.png)

Once the user clicks the `Authorize` button, they are redirected to `redirect_uri` with an access grant:

```
[redirect_uri]?code=[access_grant]
```

### 2. Exchange the `acess_grant` for an `access_token`

Using the access grant that was sent to your `redirect_uri`, your application fetches the `access_token`:

**Request**

* **Method**: `POST`
* **URL**: `https://ridewithgps.com/oauth/token.json`

**Request body**

```javascript
{
  "grant_type": "authorization_code",
  "code": "[access_grant]",
  "client_id": "[client_id]",
  "client_secret": "[client_secret]",
  "redirect_uri": "[redirect_uri]"
}
```
> [!NOTE]
> `redirect_uri` in request body must match the one used in the first step above.

**Example Response**

```javascript
{
  "access_token": "Qnpa6Bif4gF9s6uU5YwjtxbaP3UzQxgfArDP7HXZj_5",
  "token_type": "Bearer",
  "scope": "user",
  "created_at": 1725551509,
  "user_id": 1
}
```

* `user_id` is the Ride with GPS assigned id for the user who completed the autorization flow.
* `access_token` is the token to use OAuth for authentication:

```
// header
Authorization: Bearer [access_token]
```

### 3. Make OAuth authenticated requests

Your application can then make requests on the Ride with GPS API with the `Authorization` header to authenticate as your user. For example to get more details about the user who just completed the OAuth flow:

```
GET https://ridewithgps.com/api/v1/users/current.json
// header
Authorization: Bearer [access_token]
```

## Basic authentication

### 1. Get an authentication token for your account

Knowing your email and password, get an authentication token associated with your API key.

**Request**

* **Method**: `POST`
* **URL**: `https://ridewithgps.com/api/v1/auth_tokens.json`
* **Authentication**: Not required
* **Header**: `x-rwgps-api-key: [api_key]`

**Request body**

```javascript
{
  user: {
    email: "[your_email]",
    password: "[your_password]"
  }
}
```

**Example Response**

```javascript
// 201 - Created
{
  "auth_token": {
    "auth_token": "c0cc78875f250604f9abac97712e314c",
    "api_key": "2704a8df",
    "created_at": "2024-09-05T05:47:53Z",
    "updated_at": "2024-09-05T05:47:53Z",
    "user": {
      "id": 1,
      "email": "bob@example.com",
      "name": "Bob",
      "created_at": "2024-01-17T01:45:09Z",
      "updated_at": "2024-09-04T17:18:52Z"
    }
  }
}
```

### 2. Make Basic authenticated requests

You can then authenticate with Basic authentication, using your `api_key` for the username and `auth_token` for the password and base64 encode them:

```
// header
Authorization: Basic base64encode("[api_key]:[auth_token]")
```

Alternatively, you can also authenticate with the following headers:

```
// headers
x-rwgps-api-key: [api_key]
x-rwgps-auth-token: [auth_token]
```

## Convert legacy Basic tokens to OAuth access tokens

The `GET /oauth_access_token.json` endpoint issues OAuth `access_token`s for the `auth_token`s your application might have stored for your users. Use this endpoint to migrate to OAuth without requiring your users to authorize your application with Ride with GPS again.

The endpoint requires authenticating with the `auth_token` for which a OAuth `access_token` is to be issued, which is done by adding the following headers to the request:

**Request**

* **Method**: `GET`
* **URL**: `http://ridewithgps.com/oauth_access_token.json`
* **Authentication**: None
* **Headers**:
  * `x-rwgps-auth-token: [auth_token]`
  * `x-rwgps-api-key: [api_key]`

**Example response**

If your `api_key` has been configured to support OAuth, the response contains the `access_token`:

```javascript
{
  "access_token": "fJO-dk2RE4gkKyVhRY9xzgBiQjSFZXEpA3UbMFlHVXk",
  "token_type": "Bearer",
  "scope": "user",
  "created_at": 1725911852
  "rwgps_user_id": 1
}
```

* The request is idempotent, it will respond with the same `access_token` when repeated.
* `auth_token` remains valid for authentication after a corresponding OAuth `access_token` has been issued.

To authenticate requests with the OAuth `access_token`, add it as a header of your requests:

```
Authorization: Bearer [access_token]
```
