# Library Catalogue rest test api

a simple rest api for managing a book catalogue.

## Entities :

### Book
- `id` - UUID (auto-generated)
- `title` - string (required)
- `author` - string (required) 
- `isbn` - string (unique)
- `year` - integer
- `category` - string
- `available` - boolean
- `createdAt` - timestamp

## API Endpoints

### Books Collection

  GET  `/books`  List all books | Auth? No 
  POST  `/books` | Create new book | Auth? Yes 
  GET  `/books/{id}` | Get book by ID | Auth? No 
  PUT `/books/{id}` | Update book | Auth? Yes 
  DELETE  `/books/{id}` | Delete book | Auth? Yes 

## Authentication
- JWT Bearer tokens
- Required for POST, PUT, DELETE operations

## Status Codes
- 200 - Success
- 201 - Created
- 400 - Bad Request
- 401 - Unauthorized
- 404 - Not Found
- 500 - Server Error
