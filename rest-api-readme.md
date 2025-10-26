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

## API Endpoints

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
