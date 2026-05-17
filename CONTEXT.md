# Project: Website Uptime Monitor API

## Overview

Build a production-style backend project using FastAPI.

The application allows users to:

- register/login
- create website monitors
- periodically check websites
- store uptime logs
- retrieve uptime history

This project is intended for a junior backend engineer portfolio and internship applications.

The codebase must be:
- clean
- modular
- beginner-friendly
- production-inspired
- scalable enough for learning

---

# Tech Stack

## Backend
- Python 3.12+
- FastAPI
- SQLAlchemy ORM
- PostgreSQL (Supabase)
- Alembic migrations
- JWT Authentication
- Pydantic
- APScheduler
- httpx

## Deployment
- Docker
- Render or Railway

---

# Main Functional Requirements

## Authentication

Users should be able to:
- register
- login
- receive JWT access token

Use:
- hashed passwords
- JWT bearer auth

Endpoints:
- POST /auth/register
- POST /auth/login
- GET /auth/me

---

# Monitor Management

Authenticated users can:

- create monitors
- list monitors
- delete monitors

Each monitor contains:
- id
- user_id
- url
- created_at

Endpoints:
- POST /monitors
- GET /monitors
- DELETE /monitors/{id}

---

# Background Monitoring

Use APScheduler background jobs.

Every 2 minutes:
- fetch all monitors
- send HTTP request using httpx
- measure response time
- determine UP/DOWN status
- save monitoring log

A monitor log contains:
- id
- monitor_id
- status_code
- is_up
- response_time_ms
- checked_at

---

# Monitoring Logs

Endpoints:
- GET /monitors/{id}/logs

Should return:
- latest logs
- newest first

---

# Database Design

## users table

Fields:
- id
- email
- hashed_password
- created_at

## monitors table

Fields:
- id
- user_id
- url
- created_at

Relationship:
- one user has many monitors

## monitor_logs table

Fields:
- id
- monitor_id
- status_code
- is_up
- response_time_ms
- checked_at

Relationship:
- one monitor has many logs

---

# Project Structure

Use clean modular architecture.

Example structure:

app/
    main.py

    api/
        routes/

    core/
        config.py
        security.py

    db/
        session.py
        base.py

    models/

    schemas/

    services/

    repositories/

    utils/

    jobs/

---

# Important Technical Requirements

## SQLAlchemy

Use:
- Declarative models
- Relationships
- Async SQLAlchemy if possible
- Proper session management

## Pydantic

Separate:
- request schemas
- response schemas

## Authentication

Use:
- OAuth2PasswordBearer
- JWT tokens
- password hashing with passlib

## Environment Variables

Use .env file.

Store:
- DATABASE_URL
- SECRET_KEY
- JWT settings

---

# Error Handling

Add proper:
- HTTP status codes
- exception handling
- validation errors

---

# Documentation

Enable:
- Swagger docs
- OpenAPI docs

---

# Alembic

Set up Alembic migrations properly.

Commands should work:
- alembic revision --autogenerate
- alembic upgrade head

---

# Docker

Create:
- Dockerfile
- docker-compose.yml

The project should run with:
docker compose up

---

# Code Quality

Requirements:
- clean naming
- comments only where needed
- beginner-readable
- avoid overengineering
- use service layer
- separate business logic from routes

---

# Deliverables

Generate:
- complete backend code
- requirements.txt
- .env.example
- README.md
- API route examples
- setup instructions

---

# Additional Notes

This is NOT an enterprise project.
Keep it realistic for a junior backend internship portfolio.

Focus on:
- correctness
- architecture
- readability
- backend fundamentals

Avoid:
- microservices
- kubernetes
- unnecessary complexity
- advanced caching systems