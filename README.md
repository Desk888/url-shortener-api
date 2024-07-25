# URL Shortener API

Welcome to the URL Shortener API. This API allows you to shorten URLs, redirect to the original URLs, manage shortened URLs, and delete them.

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [API Endpoints](#api-endpoints)
  - [Create a Short URL](#create-a-short-url)
  - [Redirect to Original URL](#redirect-to-original-url)
  - [Get URL Info](#get-url-info)
  - [Delete Short URL](#delete-short-url)
- [Database](#database)
- [Configuration](#configuration)
- [License](#license)

## Installation

1. Clone the repository:
    ```sh
    git clone https://github.com/yourusername/url-shortener-api.git
    cd url-shortener-api
    ```

2. Create a virtual environment and activate it:
    ```sh
    python -m venv env
    source env/bin/activate  # On Windows use `env\Scripts\activate`
    ```

3. Install the dependencies:
    ```sh
    pip install -r requirements.txt
    ```

4. Set up a PostgreSQL database name "url-shortener"

## Usage

To run the application, use the following command:
```sh
uvicorn main:app --reload
```

This will start the FastAPI server on `http://127.0.0.1:8000`.

## API Endpoints

### Create a Short URL

- **Endpoint:** `/url`
- **Method:** `POST`
- **Request Body:**
    ```json
    {
        "target_url": "https://example.com"
    }
    ```
- **Response:**
    ```json
    {
        "url": "http://127.0.0.1:8000/<short_url_key>",
        "admin_url": "http://127.0.0.1:8000/admin/<secret_key>"
    }
    ```
- **Description:** Creates a shortened URL and returns the shortened URL and an admin URL for managing the short URL.

### Redirect to Original URL

- **Endpoint:** `/{url_key}`
- **Method:** `GET`
- **Response:** Redirects to the original URL.
- **Description:** Redirects to the original URL using the shortened URL key.

### Get URL Info

- **Endpoint:** `/admin/{secret_key}`
- **Method:** `GET`
- **Response:**
    ```json
    {
        "target_url": "https://example.com",
        "clicks": 10
    }
    ```
- **Description:** Retrieves information about the shortened URL, including the original URL and the number of clicks.

### Delete Short URL

- **Endpoint:** `/admin/{secret_key}`
- **Method:** `DELETE`
- **Response:**
    ```json
    {
        "detail": "URL deleted successfully"
    }
    ```
- **Description:** Deletes the shortened URL using the admin secret key.

## Database

The database is set up using SQLAlchemy. The database URL should be configured in the `config.py` file and '.env' (You need to create this one). Here's a quick overview of the database setup:

1. **Database Configuration:**
    - Configure your database URL in the `config.py` file.
    - Configure your database URL in the '.env' file.

2. **Models:**
    - The database model is already defined in the `models.py` file.

3. **CRUD Operations:**
    - Implement the necessary CRUD operations in the `crud.py` file.
  
