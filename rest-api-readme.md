# REST API Specification

## Functional Requirements
- Manage books (add, view, update, delete)
- Search and filter books
- Secure modification operations

## Non-Functional Requirements  
- A super fast response time (won't make u wait for too long)
- JWT authentication
- Pagination for large datasets
- Basic caching

## API Endpoints :

### Authentication
**POST /auth/login**
```http
POST /auth/login
Content-Type: application/json

{
  "username": "user",
  "password": "password123"
}

Response: 200 OK
{
  "token": "jwt-token",
  "expiresIn": 3600
}

Responose: 200 OK

{
  "token": "whatever901802810...",
  "expiresIn": 60
}

```
** The GET Request: **
```http
GET /books?page=1&category=fiction&available=true&limit=10
Response: 200 OK

{
  "data": [
    {
      "id": "book-123456",
      "title": "The Hobbit",
      "author": "J.R.R. Tolkien",
      "isbn": "978-0547928227",
      "year": 1937,
      "category": "Fantasy",
      "available": true,
      "links": {
        "self": "/books/book-123",
        "borrow": "/books/book-123/borrow"
      }
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 10,
    "total": 45
  }
}
```
** GET Specific Book by ID : **
GET /books/{id} - Get specific book
```http
Request: GET /books/book-123
Response: 200 OK

{
  "id": "book-123456",
  "title": "The Hobbit",
  "author": "J.R.R. Tolkien",
  "isbn": "123-429479",
  "year": 1937,
  "category": "Fantasy",
  "available": true
}
```

** The POST Request: **
```http
Request: POST /books
Authorization: Bearer <token>
Content-Type: application/json

{
  "title": "The Hobbit",
  "author": "J.R.R. Tolkien",
  "isbn": "123-429479",
  "year": 1937,
  "category": "Fantasy"
}

Response: 201 Created
{
  "id": "book-123456",
  "title": "The Hobbit",
  "author": "J.R.R. Tolkien",
  "isbn": "123-429479", 
  "year": 1937,
  "category": "Fantasy",
  "available": true,
  "links": {
    "self": "/books/book-123456"
  }
}
```
** PUT Request : **
PUT /books/{id} - Update book
```http

Request: http PUT /books/book-123456
Authorization: Bearer <token>
Content-Type: application/json

{
  "title": "The Hobbit - Updated Edition",
  "available": false
}
Response: 200 OK

{
  "id": "book-123",
  "title": "The Hobbit - Unavailable Edition (Super Rare)",
  "author": "J.R.R. Tolkien",
  "isbn": "123-429479",
  "year": 1937,
  "category": "Fantasy",
  "available": false
}
```
** The Delete Request : **
DELETE /books/{id} - Delete book

```http
Request: http DELETE /books/book-123
Authorization: Bearer <token>

Response: 204 No Content
(No response body)
```
  ## Richardson Maturity Model                               
  HATEOAS implemented (links in responses)
  
  ## Pagination                                              
  All list endpoints support:                               
  - `page` (default: 1)                                     
  - `limit` (default: 20, max: 100)


  ## Caching                                                 
  - GET /books - Cache 5 minutes                            
  - GET /books/{id} - Cache 10 minutes
  - POST/PUT/DELETE - No cache                              
