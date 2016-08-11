# API Responses

## Client Errors

### Sending invalid JSON  

```javascript
HTTP/1.1 400 Bad Request
Content-Length: 35

{
  "message":  "Problems parsing JSON",
  "timestamp": 1470904557245
}

```

### Sending invalid fields

```javascript
HTTP/1.1 422 Unprocessable Entity
{
  "message": "Validation Failed",
  "errors": [
    {
      "resource": "SubjectOfInterest",
      "field": "description",
      "violation": "size.toolarge"
    },
    ...
  ],
  "timestamp": 1470904557245
}
```
### Requesting a non-existing resource

```javacript
HTTP/1.1 404 404 Not Found
{
  "message": "Resource not found",
  "timestamp": 1470904557245
}
```

## Authentication 
1. Authenticating with invalid credentials

```javascript
HTTP/1.1 401 Unauthorized

{
  "message": "Bad credentials",
  "timestamp": 1470904557245
}
```

