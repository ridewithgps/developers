# User endpoints

## GET /api/v1/users/current.json

Returns details about the authenticated user.

**Request**

* **Method**: `GET`
* **URL**: `https://ridewithgps.com/api/v1/users/current.json`
* **Authentication**: [Required](../authentication.md)

**Example Response**

```javascript
{
  "user": {
    "id": 1,
    "email": "bob@example.com",
    "name": "Bob",
    "created_at": "2024-01-17T01:45:09Z",
    "updated_at": "2024-06-11T21:11:16Z"
  }
}
```
