# Bookshelf API – Dicoding Submission

Backend Bookshelf API built as a Dicoding submission using Node.js and @hapi/hapi.  
This project exposes RESTful endpoints to manage book data (create, read, update, delete) following Dicoding’s specification.

## Features

- Add a new book with validation
- Get all books (with optional query filters)
- Get a single book by ID
- Update a book by ID
- Delete a book by ID
- Response format aligned with Dicoding’s Bookshelf API requirements
- Basic error handling for invalid input

## Tech Stack

- **Language:** JavaScript (Node.js)
- **Framework:** @hapi/hapi
- **Runtime:** Node.js

## API Endpoints

All routes are defined in `routes.js` and handled by functions in `handler.js`.

### 1. Add a New Book

**Method:** `POST`  
**Path:** `/books`  
**Handler:** `addBookHandler`

**Description:** Add a new book to the bookshelf.

**Example request body:**

```json
{
  "name": "Clean Code",
  "year": 2008,
  "author": "Robert C. Martin",
  "summary": "A handbook of agile software craftsmanship.",
  "publisher": "Prentice Hall",
  "pageCount": 464,
  "readPage": 100,
  "reading": true
}
````

---

### 2. Get All Books

**Method:** `GET`
**Path:** `/books`
**Handler:** `getAllBooksHandler`

**Description:** Get a list of all books.

Typically supports query parameters (depending on your implementation):

* `name` – filter by book name (partial match)
* `reading` – filter by reading status (`0` or `1`)
* `finished` – filter by finished status (`0` or `1`)

---

### 3. Get Book by ID

**Method:** `GET`
**Path:** `/books/{id}`
**Handler:** `getBookByIdHandler`

**Description:** Get detailed information of a single book by its ID.

---

### 4. Update Book by ID

**Method:** `PUT`
**Path:** `/books/{id}`
**Handler:** `editBookByIdHandler`

**Description:** Update an existing book’s data by its ID.

Request body structure is usually similar to the `POST /books` payload.

---

### 5. Delete Book by ID

**Method:** `DELETE`
**Path:** `/books/{id}`
**Handler:** `deleteBookByIdHandler`

**Description:** Delete a book from the bookshelf by its ID.

---

## Getting Started

### Prerequisites

* Node.js (recommended: latest LTS)
* npm or pnpm installed
* API testing tool, for example:

  * Postman, or
  * REST Client (VS Code extension)

### Installation

Clone this repository:

```bash
git clone https://github.com/RenathaPutri/submission-dicoding-bookselfAPITest.git
cd submission-dicoding-bookselfAPITest
```

Install dependencies:

```bash
npm install
# or
pnpm install
```

### Running the Server

Start the server:

```bash
npm start
# or, if you run it manually:
node src/server.js
```

> Update the file path above if your server file has a different name or location.

By default, the server usually runs on:

```text
http://localhost:5000
```

(or replace with the actual port you configured in `server.js`.)

## Project Structure

> Update this section if your structure is slightly different, but this is the typical setup for this submission.

```txt
submission-dicoding-bookselfAPITest/
  src/
    server.js       # Hapi server setup & plugin registration
    routes.js       # All route definitions (methods, paths, handlers)
    handler.js      # Handler functions for each route
    books.js        # In-memory data storage for books
  package.json
  README.md
```

* **`routes.js`**
  Exports an array of route objects:

  ```js
  const {
    addBookHandler,
    getAllBooksHandler,
    getBookByIdHandler,
    editBookByIdHandler,
    deleteBookByIdHandler,
  } = require('./handler');

  const routes = [
    {
      method: 'POST',
      path: '/books',
      handler: addBookHandler,
    },
    {
      method: 'GET',
      path: '/books',
      handler: getAllBooksHandler,
    },
    {
      method: 'GET',
      path: '/books/{id}',
      handler: getBookByIdHandler,
    },
    {
      method: 'PUT',
      path: '/books/{id}',
      handler: editBookByIdHandler,
    },
    {
      method: 'DELETE',
      path: '/books/{id}',
      handler: deleteBookByIdHandler,
    },
  ];

  module.exports = routes;
  ```

* **`handler.js`**
  Contains the logic for each route: adding, listing, getting by ID, editing, and deleting books.

* **`books.js`**
  Stores the books data in memory (typically an array), used as a simple data store for this submission.

## Validation & Error Handling

The API usually implements the following validations:

* **Book name is required**
  If `name` is missing, the API returns a `fail` response with an appropriate message.

* **`readPage` cannot be greater than `pageCount`**
  If `readPage > pageCount`, the API returns a `fail` response.

Common response format:

```json
{
  "status": "success | fail | error",
  "message": "Description of the result",
  "data": {
    // optional, depending on the context
  }
}
```

Check `handler.js` for the exact logic and messages.

## Testing the API

You can test the endpoints using:

* **Postman**
  Create a collection and add requests for each endpoint:

  * `POST /books`
  * `GET /books`
  * `GET /books/{id}`
  * `PUT /books/{id}`
  * `DELETE /books/{id}`

* **REST Client (VS Code)**
  Create a `.rest` or `.http` file with sample requests and execute them directly in VS Code.

Make sure the server is running before you send any request.

## Roadmap / Possible Improvements

* Replace in-memory `books.js` with a real database (PostgreSQL, MongoDB, etc.)
* Add automated tests (Jest/Mocha) for handlers and routes
* Add pagination for `GET /books`
* Add Swagger/OpenAPI documentation for easier API exploration
* Add authentication and role-based access for book management

## License

This project is created as part of a Dicoding submission.
You can add a license (e.g. `MIT`) if you plan to extend or reuse this project in the future.

## Maintainer

* Renatha Putri
  GitHub: [@RenathaPutri](https://github.com/RenathaPutri)
