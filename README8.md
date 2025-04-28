# Library Management System RESTful API

This is a RESTful API for a library management system, built using Node.js and Express.js. It allows users to manage books and includes user authentication and file upload capabilities.

## Features

### Library Management System
* Add new books (title, author, genre, year of publication).
* Update book details.
* Delete books from the collection.
* Fetch a list of books with pagination and filtering by genre and author.
* User authentication system to restrict access to certain API routes.

### File Upload and Management System
* Upload files (images, PDFs, etc.).
* View the list of uploaded files.
* Download specific files.
* Delete specific files.

## Technologies Used
* Node.js
* Express.js
* bcrypt (for password hashing)
* multer (for file uploads)

## Setup Instructions

**Step 1: Save the Code**

* Save the provided code (e.g., in a file named `server.js`) in your VS Code editor.

**Step 2: Install Dependencies**

* Open the integrated terminal in VS Code (`Terminal` \> `New Terminal`).
* Navigate to your project directory using the `cd` command.
* Run the following command to install the required Node.js packages:

    ```bash
    npm install express body-parser bcrypt multer
    ```
    This command downloads and installs the `express`, `body-parser`, `bcrypt`, and `multer` libraries.

**Step 3: Create the `uploads` Directory**

* The code is configured to save uploaded files in a directory named `uploads` at the root of your project.
* In your VS Code Explorer (the file tree on the left):
    * Right-click on the root of your project.
    * Select `New Folder`.
    * Name the folder `uploads`.

**Step 4: Run the Node.js Server**

* In the VS Code terminal, start the server by running:
    ```bash
    node server.js
    ```
* You should see the message `Server listening on port 3000`, indicating that the API is running. Keep this terminal window open while testing the API.

**Step 5: Test the API Endpoints with Postman**

* Open Postman to test the API endpoints.

### A. User Registration (POST /register)
    * **Method:** POST
    * **URL:** http://localhost:3000/register
    * **Body (raw/JSON):**
        ```json
        {
            "username": "newuser",
            "password": "securepassword"
        }
        ```
    * **Expected Response (201 Created):**
        ```json
        {
            "message": "User registered successfully!"
        }
        ```

### B. User Login (POST /login)
    * **Method:** POST
    * **URL:** http://localhost:3000/login
    * **Body (raw/JSON):**
        ```json
        {
            "username": "newuser",
            "password": "securepassword"
        }
        ```
    * **Expected Response (200 OK):**
        ```json
        {
            "message": "Login successful!",
            "token": "DUMMY_TOKEN"
        }
        ```
    * **Note:** This API uses a static `"DUMMY_TOKEN"` for simplicity. In a real application, implement proper JWT (JSON Web Token) generation and verification.

### C. Add New Book (POST /books)
    * **Method:** POST
    * **URL:** http://localhost:3000/books
    * **Headers:**
        * `Authorization`: `Bearer DUMMY_TOKEN`
    * **Body (raw/JSON):**
        ```json
        {
            "title": "The Great Gatsby",
            "author": "F. Scott Fitzgerald",
            "genre": "Classic",
            "year": 1925
        }
        ```
    * **Expected Response (201 Created):** The JSON representation of the new book.

### D. Update Book (PUT /books/:id)
    * **Method:** PUT
    * **URL:** http://localhost:3000/books/1 (Replace `1` with the book ID)
    * **Headers:**
        * `Authorization`: `Bearer DUMMY_TOKEN`
    * **Body (raw/JSON):**
        ```json
        {
            "year": 1926
        }
        ```
    * **Expected Response (200 OK):** The JSON representation of the updated book.

### E. Delete Book (DELETE /books/:id)
    * **Method:** DELETE
    * **URL:** http://localhost:3000/books/1 (Replace `1` with the book ID)
    * **Headers:**
        * `Authorization`: `Bearer DUMMY_TOKEN`
    * **Expected Response (204 No Content):** (Empty response body)

### F. Get Books (GET /books)
    * **Method:** GET
    * **URL:** http://localhost:3000/books
    * **Query Parameters (Optional):**
        * Pagination: `page=2&limit=5`
        * Filter by Genre: `genre=Classic`
        * Filter by Author: `author=F. Scott Fitzgerald`
        * Combine Filters: `genre=Classic&author=F. Scott Fitzgerald&page=1&limit=2`
    * **Expected Response (200 OK):**
        ```json
        {
            "books": [ /* Array of books */ ],
            "currentPage": 1,
            "totalPages": 1,
            "totalItems": 1
        }
        ```

### G. Upload File (POST /upload)
    * **Method:** POST
    * **URL:** http://localhost:3000/upload
    * **Headers:**
        * `Authorization`: `Bearer DUMMY_TOKEN`
    * **Body (form-data):**
        * Key: `file`, Value: (Select a file)
    * **Expected Response (200 OK):**
        ```json
        {
            "message": "File uploaded successfully!",
            "filename": "file-timestamp-random.ext",
            "path": "/uploads/file-timestamp-random.ext"
        }
        ```

### H. View Files (GET /files)
    * **Method:** GET
    * **URL:** http://localhost:3000/files
    * **Headers:**
        * `Authorization`: `Bearer DUMMY_TOKEN`
    * **Expected Response (200 OK):**
        ```json
        {
            "files": ["file1.ext", "file2.pdf"]
        }
        ```

### I. Download File (GET /files/:filename)
    * **Method:** GET
    * **URL:** http://localhost:3000/files/file1.ext (Replace `file1.ext` with the filename)
    * **Headers:**
        * `Authorization`: `Bearer DUMMY_TOKEN`
    * **Expected Response (200 OK):** The file should be downloaded.

### J. Delete File (DELETE /files/:filename)
    * **Method:** DELETE
    * **URL:** http://localhost:3000/files/file1.ext (Replace `file1.ext` with the filename)
    * **Headers:**
        * `Authorization`: `Bearer DUMMY_TOKEN`
    * **Expected Response (200 OK):**
        ```json
        {
            "message": "File deleted successfully!"
        }
        ```
