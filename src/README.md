# Mergington High School Activities API

A super simple FastAPI application that allows students to view and sign up for extracurricular activities.

## Features

- View all available extracurricular activities
- Sign up for activities

## Admin (developer) notes

This project includes a minimal admin authentication flow (JWT) for developer convenience.

- Login: POST `/admin/token` (form fields `username` and `password`) — returns a Bearer token.
- Protected dashboard: GET `/admin/dashboard` (requires `Authorization: Bearer <token>`).

Environment variables:

- `ADMIN_USERNAME` — admin username (default: `admin`).
- `ADMIN_PASSWORD` — admin password (default: `admin`). For production set a strong password or a bcrypt hash (passlib-compatible).
- `SECRET_KEY` — optional, auto-generated if missing.

Note: These defaults are intentionally permissive for local development. Rotate credentials and supply a secure `SECRET_KEY` before deploying.

## Getting Started

1. Install the dependencies:

   ```
   pip install fastapi uvicorn
   ```

2. Run the application:

   ```
   python app.py
   ```

3. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

## API Endpoints

| Method | Endpoint                                                          | Description                                                         |
| ------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- |
| GET    | `/activities`                                                     | Get all activities with their details and current participant count |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Sign up for an activity                                             |

## Data Model

The application uses a simple data model with meaningful identifiers:

1. **Activities** - Uses activity name as identifier:

   - Description
   - Schedule
   - Maximum number of participants allowed
   - List of student emails who are signed up

2. **Students** - Uses email as identifier:
   - Name
   - Grade level

All data is stored in memory, which means data will be reset when the server restarts.
