# Authentication Feature

This document describes the basic authentication system implemented in the Mergington High School Activities application.

## Overview

The application now includes basic user authentication using session-based login with cookies. This is a simple demonstration of access control - users must be logged in to sign up for or unregister from activities.

## Features

### Backend (FastAPI)

- **In-memory user storage**: Two predefined users with username/password authentication
  - Teacher: username `teacher`, password `teachpass`, role `staff`
  - Student: username `student`, password `studpass`, role `student`
  
- **Session management**: Uses httpOnly cookies with 1-hour expiration
  - Sessions stored in-memory (will be lost on server restart)
  - Session IDs generated using Python's `secrets` module

- **API Endpoints**:
  - `POST /login` - Authenticate with username and password (returns user role)
  - `POST /logout` - Clear session and delete cookie
  - Modified endpoints that require authentication:
    - `POST /activities/{activity_name}/signup` - Requires valid session
    - `DELETE /activities/{activity_name}/unregister` - Requires valid session

### Frontend (JavaScript)

- **Login/Logout UI**: Appears in the header
  - Login form with username and password fields
  - After login, displays greeting with username and role
  - Logout button to clear session

- **Access Control**:
  - Sign Up button is disabled when not logged in
  - Attempting to sign up without authentication shows error message
  - Successfully logging in enables the Sign Up functionality

## Security Notes

⚠️ **This is a basic demonstration only!** It is NOT production-ready:

- Passwords are stored in plain text (should use hashing like bcrypt)
- No HTTPS requirement (cookies should use Secure flag in production)
- Sessions stored in memory (should use Redis or database)
- No rate limiting on login attempts
- No password complexity requirements
- No CSRF protection
- No persistent storage (all data lost on restart)

## Testing Credentials

You can test the application with either of these accounts:

- **Teacher Account**
  - Username: `teacher`
  - Password: `teachpass`
  - Role: `staff`

- **Student Account**
  - Username: `student`
  - Password: `studpass`
  - Role: `student`

## Screenshots

See the `screenshots/` directory for visual examples of:
1. Before login (disabled Sign Up button)
2. After login (enabled Sign Up button, showing user info)
3. Successful signup while authenticated
4. After logout (back to login form)
5. Teacher account logged in
