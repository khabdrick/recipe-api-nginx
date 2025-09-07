# Recipe API

A comprehensive RESTful API for managing cooking recipes built with FastAPI and PostgreSQL. This API provides full CRUD operations for recipes with advanced features like search, filtering, pagination, and statistics.

## Features

- **Full CRUD Operations**: Create, read, update, and delete recipes
- **Async/Await Support**: All endpoints are asynchronous for better performance
- **Advanced Search**: Search recipes by title, ingredient, cuisine, or difficulty
- **Pagination**: Efficient pagination for large recipe collections
- **Data Validation**: Robust input validation using Pydantic models
- **OpenAPI Documentation**: Auto-generated interactive API documentation
- **Statistics Endpoint**: Get insights about your recipe collection
- **Docker Support**: Easy deployment with Docker and Docker Compose

## Technology Stack

- **FastAPI**: Modern, fast web framework for building APIs
- **PostgreSQL**: Robust relational database
- **SQLAlchemy**: Async ORM for database operations
- **Pydantic**: Data validation and serialization
- **asyncpg**: Async PostgreSQL driver
- **Docker**: Containerization for easy deployment

## Project Structure

```
recipe-api/
├── main.py              # Main FastAPI application
├── requirements.txt     # Python dependencies
├── docker-compose.yml   # Docker Compose configuration
├── Dockerfile          # Docker image configuration
└── README.md           # Project documentation
```

## Quick Start

### Method 1: Using Docker Compose (Recommended)

1. **Clone or create the project directory**:
   ```bash
   mkdir recipe-api
   cd recipe-api
   ```

2. **Create all the necessary files** (main.py, requirements.txt, docker-compose.yml, Dockerfile)

3. **Start the application**:
   ```bash
   docker-compose up -d
   ```

4. **Access the API**:
   - API Base URL: http://localhost:8000
   - Interactive Documentation: http://localhost:8000/docs
   - Alternative Documentation: http://localhost:8000/redoc

### Method 2: Local Development Setup

1. **Prerequisites**:
   - Python 3.11+
   - PostgreSQL 12+

2. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

3. **Set up PostgreSQL database**:
   ```sql
   CREATE DATABASE recipedb;
   CREATE USER user WITH PASSWORD 'password';
   GRANT ALL PRIVILEGES ON DATABASE recipedb TO user;
   ```

4. **Set environment variable**:
   ```bash
   export DATABASE_URL="postgresql+asyncpg://user:password@localhost:5432/recipedb"
   ```

5. **Run the application**:
   ```bash
   uvicorn main:app --reload
   ```

## API Endpoints

### Recipe Management

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/` | API information |
| POST | `/recipes/` | Create a new recipe |
| GET | `/recipes/` | Get all recipes (with pagination and filters) |
| GET | `/recipes/{recipe_id}` | Get a specific recipe |
| PUT | `/recipes/{recipe_id}` | Update a recipe |
| DELETE | `/recipes/{recipe_id}` | Delete a recipe |

### Search & Statistics

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/recipes/search/by-ingredient` | Search recipes by ingredient |
| GET | `/recipes/stats` | Get recipe statistics |

## API Usage Examples

### Create a Recipe

```bash
curl -X POST "http://localhost:8000/recipes/" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Spaghetti Carbonara",
    "description": "Classic Italian pasta dish",
    "ingredients": "spaghetti, eggs, pancetta, parmesan cheese, black pepper",
    "instructions": "1. Cook pasta. 2. Fry pancetta. 3. Mix eggs and cheese. 4. Combine everything.",
    "prep_time": 10,
    "cook_time": 15,
    "servings": 4,
    "difficulty": "Medium",
    "cuisine": "Italian"
  }'
```

### Get All Recipes with Filtering

```bash
curl "http://localhost:8000/recipes/?cuisine=Italian&difficulty=Medium&limit=5"
```

### Search by Ingredient

```bash
curl "http://localhost:8000/recipes/search/by-ingredient?ingredient=cheese"
```

### Get Recipe Statistics

```bash
curl "http://localhost:8000/recipes/stats"
```

## Recipe Data Model

```json
{
  "id": 1,
  "title": "Recipe Title",
  "description": "Recipe description (optional)",
  "ingredients": "List of ingredients",
  "instructions": "Cooking instructions",
  "prep_time": 30,
  "cook_time": 45,
  "servings": 4,
  "difficulty": "Easy|Medium|Hard",
  "cuisine": "Cuisine type",
  "created_at": "2024-01-01T12:00:00",
  "updated_at": "2024-01-01T12:00:00"
}
```

## Configuration

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `DATABASE_URL` | PostgreSQL connection string | `postgresql+asyncpg://user:password@localhost/recipedb` |

### Query Parameters

- **Pagination**: `skip` (offset) and `limit` (page size)
- **Search**: `search` (title search), `cuisine`, `difficulty`
- **Limits**: Maximum limit per request is 100

## Development

### Running Tests

```bash
# Install test dependencies
pip install pytest pytest-asyncio httpx

# Run tests (create test files as needed)
pytest
```

### Code Style

The project follows Python best practices:
- Type hints for better code documentation
- Async/await for all database operations
- Pydantic models for data validation
- Comprehensive error handling



## API Documentation

Once the server is running, you can access:

- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc
- **OpenAPI JSON**: http://localhost:8000/openapi.json
