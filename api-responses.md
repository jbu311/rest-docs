# API Responses

## Client Errors

### Sending invalid JSON  

```javascript
HTTP/1.1 400 Bad Request

{
  "error":  "Problems parsing JSON",
  "code": <Custom code>,
  "timestamp": 1470904557245
}

```
### Sending invalid fields

```javascript
HTTP/1.1 422 Unprocessable Entity

{
  "error": "Validation Failed",
  "code": <Custom code>,
  "message": [
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

```javascript
HTTP/1.1 404 Not Found

{
  "error": "Resource not found",
  "code": <Custom code>,
  "timestamp": 1470904557245
}
```
## Authentication 
1. Authenticating with invalid credentials

```javascript
HTTP/1.1 401 Unauthorized

{
  "error": "Bad credentials",
  "code": <Custom code>,
  "timestamp": 1470904557245
}
```

## Pagination

```javascript
GET /api/v1/subject_of_interests?offset=0&limit=20

HTTP/1.1 200 OK

{
  data: {
    "href": <String - the URL of the current request>,
    "items": <An array of objects	- the requested data>,
    "next": <String - URL to next page, null if none>,
    "prev": <String - URL to previous page, null if none>,
    "offset": <Integer - the request offset>,
    "limit": <Integer - the maximum number inf the response>,
    "total": <Integer - the total of number of items to return>
  }
}
```

### Requesting a non-existing page

```javascript
GET /api/v1/subject_of_interests?offset=1000&limit=20

HTTP/1.1 404 Not Found

{
  "error": "Page not found",
  "code": <Custom code>,
  "timestamp": 1470904557245
}

```

## Requesting a single resource 

```javascript
GET /api/v1/subject_of_interests/:id

HTTP/1.1 200 OK

{
  data: {
    "id" <UUID>,
    "description": "RESTful API"
  }
}

```



