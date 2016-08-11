# API Responses

## Client Errors

### Sending invalid JSON  

```javascript
HTTP/1.1 400 Bad Request
{
  "error": {
    "mesage":  "Problems parsing JSON"
    "code": <Custom code>,
    "timestamp": 1470904557245
  }
}

```
### Sending invalid fields

```javascript
HTTP/1.1 422 Unprocessable Entity
{
  "error": {
    "message": "Validation Failed",
    "code": <Custom code>,
    "details": [
      {
        "resource": "SubjectOfInterest",
        "field": "description",
        "violation": "size.toolarge"
      },
    ...
    ],
    "timestamp": 1470904557245
  }
}  
```
### Requesting a non-existing resource

```javascript
HTTP/1.1 404 Not Found
{
  "error": {
    "message": "Resource not found",
    "code": <Custom code>,
    "timestamp": 1470904557245
  }
}
```
## Authentication 
1. Authenticating with invalid credentials

```javascript
HTTP/1.1 401 Unauthorized
{
  "error": {
    "message": "Bad credentials",
    "code": <Custom code>,
    "timestamp": 1470904557245
  }
}
```

## Pagination

```javascript
GET /api/v1/subject_of_interests?offset=0&limit=20

HTTP/1.1 200 OK
{
  "meta": {
    "href": <String - the URL of the current request>
    "next": <String - URL to next page, null if none>,
    "prev": <String - URL to previous page, null if none>,
    "offset": <Integer - the request offset>,
    "limit": <Integer - the maximum number inf the response>,
    "total": <Integer - the total of number of items to return>
  }
  "data": {
    "items": <An array of objects - the requested data>
  }
}
```

### Requesting a non-existing page

```javascript
GET /api/v1/subject_of_interests?offset=1000&limit=20

HTTP/1.1 404 Not Found
{
  "error" {
    "mesasge": "Page not found",
    "code": <Custom code>,
    "timestamp": 1470904557245
  }
}

```

## CRUD on a single resource 

### Create a resource


```javascript
POST /api/v1/subject_of_interests

// Success
HTTP/1.1 201 Created
{
  "data": {
    "id": <UUID>
    ...
  }
}  

// Error
HTTP/1.1 422 Unprocesable Entity
"error": {
    "message": "Validation Failed",
    "code": <Custom code>,
    "details": [
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

## Read a resource

```javascript
GET /api/v1/subject_of_interests/:id

// Success
HTTP/1.1 200 OK
{
  data: {
    "id" <UUID>,
    "description": "RESTful API"
  }
}

// Error
HTTP/1.1 404 Not Found
{
  "error": {
    "message": "Resource not found",
    "code": <Custom code>,
    "timestamp": 1470904557245
  }
}
```

### Update a resource entirely

```javascript
PUT /api/v1/subject_of_interests/:id

// Success
HTTP/1.1 200 Created
{
  "data": {
    "id": <UUID>
    ...
  }
}  

// Error
HTTP/1.1 422 Unprocesable Entity
{
  "error": {
    "message": "Validation Failed",
    "code": <Custom code>,
    "details": [
      {
        "resource": "SubjectOfInterest",
        "field": "description",
        "violation": "size.toolarge"
      },
    ...
    ],
    "timestamp": 1470904557245
}

// Or error
HTTP/1.1 404 Not Found
{
  "error": {
    "message": "Resource not found",
    "code": <Custom code>,
    "timestamp": 1470904557245
  }
}
```

## Delete a resource

```javascript
DELETE /api/v1/subject_of_interests/:id

// Success
HTTP/1.1 204 No Content

// Error
HTTP/1.1 404 Not Found
{
  "error": {
    "message": "Resource not found",
    "code": <Custom code>,
    "timestamp": 1470904557245
  }
}
```



