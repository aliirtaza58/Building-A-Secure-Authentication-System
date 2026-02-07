
# Streamlit Authentication App

A Streamlit web application with user authentication and role-based access control connecting with the previous project's Database Functions

## Overview

This application provides user login and registration functionality with secure password storage. Users can register for an account, log in, and access a protected dashboard based on their role.

## Project Structure

```
.
├── Home.py                 # Login and registration page
├── app.py                  # Streamlit component examples
├── pages/
│   └── 1_Dashboard.py     # Dashboard (requires authentication)
└── app/
    └── data/
        ├── db.py          # Database connection
        └── users.py       # User authentication functions

```

## Installation

Install required dependencies:

```bash
pip install streamlit bcrypt pandas

```

## Running the Application

```bash
streamlit run Home.py

```

Access the application at `http://localhost:8501`

## Main Workflow

### User Registration

1.  Navigate to the Register tab
2.  Enter a username and password
3.  Confirm the password
4.  Click Register to create the account

The system checks for:

-   Empty fields
-   Password match confirmation
-   Existing username

Passwords are hashed using bcrypt before storage.

### User Login

1.  Enter username and password on the Login tab
2.  Click Login
3.  System verifies credentials against the database
4.  On success, user is redirected to the Dashboard

### Session Management

The application maintains session state for:

-   `logged_in`: Authentication status
-   `username`: Current user
-   `role`: User role for access control

Sessions persist across page navigation within the application.

### Database Functions

**Authentication (`app/data/users.py`)**

-   `verify_user(username, password)`: Validates credentials
-   `get_user_role(username)`: Returns user role
-   `insert_user(username, hashed_password)`: Creates new user
-   `get_user_by_username(username)`: Checks username existence

**Database (`app/data/db.py`)**

-   `connect_database()`: Establishes connection

## Database Requirements

The application requires a users table with:

-   `username` (unique)
-   `password` (hashed)
-   `role`

## Security

-   Passwords are hashed with bcrypt and salt
-   Protected routes check authentication state
-   Session state prevents unauthorized access
