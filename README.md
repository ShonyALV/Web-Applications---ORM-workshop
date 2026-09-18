# FastAPI ORM Workshop

A small FastAPI + SQLAlchemy example application used for demonstrating common ORM patterns (CRUD, relationships, nested queries) and a simple CLI client for interacting with the API.

## Project structure

Top-level repository layout (the repository root folder is named "WEB APPLICATIONS - ORM"):

```text
WEB APPLICATIONS - ORM/
├── README.md
├── docker-compose.yml
└── fastapi-orm-workshop/
    ├── server/
    │   ├── __init__.py
    │   ├── database.py
    │   ├── models.py
    │   ├── schemas.py
    │   └── main.py
    ├── client/
    │   ├── client.py
    │   └── data/
    │       └── order.json
    └── venv/
```

Inside `fastapi-orm-workshop/` (project root):

- `server/` — FastAPI application and SQLAlchemy models
  - `server/main.py` — API routes
  - `server/database.py` — DB connection and session
  - `server/models.py` — ORM models
  - `server/schemas.py` — Pydantic schemas
- `client/` — simple CLI client and example JSON (`client/data/order.json`)
- `venv/` — optional local virtual environment (not committed)


## Features

- Customers, Products, Orders, and OrderItems models
- CRUD endpoints for customers and products
- Nested order retrieval and updating order status
- Small interactive CLI client to exercise the API

## Prerequisites

- Python 3.10+ (recommended)
- MySQL server (or use the provided `docker-compose.yml`)
- Recommended Python packages: `fastapi`, `uvicorn`, `sqlalchemy`, `pymysql`, `requests`

## Quick start

Option A — run with Docker Compose (provides a MySQL instance):

```bash
# Create a .env with DB_NAME, DB_USER, DB_PASSWORD, DB_PORT (for example 3306)
docker-compose up -d
```

Option B — run locally with an existing MySQL server:

1. Create a Python virtual environment and install dependencies:

```bash
python -m venv .venv
source .venv/bin/activate
pip install fastapi uvicorn sqlalchemy pymysql requests
```

2. Update the database connection in [server/database.py](server/database.py) (the `DATABASE_IP` and connection string) to point to your MySQL host, or set up a local container via Docker Compose.

## Running the API server

Start the FastAPI app with Uvicorn from the repository root:

```bash
uvicorn server.main:app --reload
```

The API will be available at `http://127.0.0.1:8000` and the interactive docs at `http://127.0.0.1:8000/docs`.

## Using the client

There is a simple interactive client at [client/client.py](client/client.py) that makes requests to the API.

```bash
# from repo root
python client/client.py
```

By default the client expects the API at `http://127.0.0.1:8000`. Edit `BASE_URL` in `client/client.py` if needed.

## Important configuration notes

- The database connection is defined in `server/database.py`. Update `DATABASE_IP` or the `DATABASE_URL` string to match your MySQL server address and credentials.
- The included `docker-compose.yml` defines a `db` service; set the environment variables `DB_NAME`, `DB_USER`, `DB_PASSWORD`, and `DB_PORT` before running it.

## API Endpoints (summary)

- `GET /` — API root
- `POST /customers` — create customer
- `GET /customers` — list customers
- `GET /customers/{id}` — get customer
- `PUT /customers/{id}` — update customer
- `DELETE /customers/{id}` — delete customer
- `POST /products` — create product
- `GET /products` — list products
- `GET /products/{id}` — get product
- `PUT /products/{id}` — update product
- `DELETE /products/{id}` — delete product
- `POST /orders` — create order (used by client JSON upload)
- `GET /orders/{id}` — get order
- `PUT /orders/{id}/status` — update order status
- `DELETE /orders/{id}` — delete order
- `GET /customers/{id}/orders` — get a customer with their orders

## Authors

- Jhony Penaherrera — https://github.com/ShonyALV
- Demian Viteri — https://github.com/demivn15
- Alejandro Ortiz — https://github.com/Aleortz
