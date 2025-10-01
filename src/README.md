# Mergington High School Activities API

A super simple FastAPI application that allows students to view and sign up for extracurricular activities.

## Features

- View all available extracurricular activities
- User authentication (login/logout)
- Sign up for activities (requires authentication)
- Unregister from activities (requires authentication)

## Getting Started

1. Install the dependencies:

   ```
   pip install -r requirements.txt
   ```

2. Run the application:

   ```
   cd src
   uvicorn app:app --reload
   ```

3. Open your browser and go to:
   - Web UI: http://localhost:8000
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

## Authentication

The application now requires authentication to sign up for or unregister from activities.

### Test Users

| Username | Password  | Role    |
| -------- | --------- | ------- |
| teacher  | teachpass | staff   |
| student  | studpass  | student |

### Login

Use the login form in the web UI or send a POST request to `/login`:

```bash
curl -X POST "http://localhost:8000/login" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "username=teacher&password=teachpass"
```

## API Endpoints

| Method | Endpoint                                                          | Description                                                         | Auth Required |
| ------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- | ------------- |
| POST   | `/login`                                                          | Login with username and password                                    | No            |
| POST   | `/logout`                                                         | Logout and clear session                                            | No            |
| GET    | `/activities`                                                     | Get all activities with their details and current participant count | No            |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Sign up for an activity                                             | Yes           |
| DELETE | `/activities/{activity_name}/unregister?email=student@mergington.edu` | Unregister from an activity                                      | Yes           |

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
