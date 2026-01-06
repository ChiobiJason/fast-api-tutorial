# FastAPI Tutorial

A simple FastAPI tutorial demonstrating basic REST API endpoints with CRUD operations.

## Features

- FastAPI framework for building APIs
- Pydantic models for data validation
- RESTful endpoints for managing items
- Automatic API documentation with Swagger UI

## Prerequisites

- Python 3.7+
- pip (Python package manager)

## Installation

1. Clone or navigate to this repository:

```bash
cd "fast-api tutorial"
```

2. Install FastAPI and Uvicorn:

```bash
pip install fastapi uvicorn
```

## Running the Application

Start the FastAPI server using Uvicorn:

```bash
uvicorn main:app --reload
```

The `--reload` flag enables auto-reload during development.

The API will be available at:

- **API**: http://localhost:8000
- **Interactive API Docs (Swagger UI)**: http://localhost:8000/docs
- **Alternative API Docs (ReDoc)**: http://localhost:8000/redoc

## API Endpoints

### 1. Root Endpoint

- **URL**: `/`
- **Method**: `GET`
- **Description**: Returns a simple greeting
- **Response**:
  ```json
  {
    "Hello": "world"
  }
  ```

### 2. Create Item

- **URL**: `/items`
- **Method**: `POST`
- **Description**: Creates a new item and adds it to the list
- **Request Body**:
  ```json
  {
    "text": "string",
    "is_done": false
  }
  ```
- **Response**: Returns the updated list of all items

### 3. List Items

- **URL**: `/items`
- **Method**: `GET`
- **Description**: Retrieves a list of items with optional limit
- **Query Parameters**:
  - `limit` (optional, default: 10): Maximum number of items to return
- **Response**: Array of items
  ```json
  [
    {
      "text": "APPLE",
      "is_done": false
    },
    ...
  ]
  ```

### 4. Get Item by ID

- **URL**: `/items/{item_id}`
- **Method**: `GET`
- **Description**: Retrieves a specific item by its index
- **Path Parameters**:
  - `item_id` (integer): The index of the item to retrieve
- **Response**:
  ```json
  {
    "text": "APPLE",
    "is_done": false
  }
  ```
- **Error Response** (404): If item_id is out of range
  ```json
  {
    "detail": "Item with id {item_id} not found"
  }
  ```

## Example Usage

### Using cURL

**Get root endpoint:**

```bash
curl http://localhost:8000/
```

**Create a new item:**

```bash
curl -X POST "http://localhost:8000/items" \
  -H "Content-Type: application/json" \
  -d '{"text": "GRAPE", "is_done": false}'
```

**List items (with limit):**

```bash
curl "http://localhost:8000/items?limit=5"
```

**Get item by ID:**

```bash
curl http://localhost:8000/items/0
```

### Using Python requests

```python
import requests

# Get root
response = requests.get("http://localhost:8000/")
print(response.json())

# Create item
new_item = {"text": "GRAPE", "is_done": False}
response = requests.post("http://localhost:8000/items", json=new_item)
print(response.json())

# List items
response = requests.get("http://localhost:8000/items?limit=5")
print(response.json())

# Get item by ID
response = requests.get("http://localhost:8000/items/0")
print(response.json())
```

## Data Model

### Item

- `text` (string, required): The text content of the item
- `is_done` (boolean, optional, default: false): Whether the item is completed

## Interactive API Documentation

FastAPI automatically generates interactive API documentation. Once the server is running, visit:

- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc

These interfaces allow you to test all endpoints directly from your browser.

## Project Structure

```
fast-api tutorial/
├── main.py          # FastAPI application and endpoints
└── README.md        # This file
```

## Notes

- The items list is stored in memory and will reset when the server restarts
- Item IDs correspond to list indices (0-based)
- The initial items list contains 10 fruit names
