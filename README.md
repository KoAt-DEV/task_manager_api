# Task Manager API

A secure REST API for task management built with FastAPI, featuring JWT authentication, PostgreSQL database integration, and comprehensive testing.

## Features

- **User Authentication**: JWT-based authentication with secure password hashing
- **Task Management**: Full CRUD operations for tasks
- **User Isolation**: Users can only access their own tasks
- **Secure**: Password hashing with bcrypt, environment variable configuration
- **Database**: PostgreSQL integration with SQLAlchemy ORM
- **Testing**: Comprehensive test suite with pytest and separate test database

## Tech Stack

- **Backend**: FastAPI
- **Database**: PostgreSQL
- **ORM**: SQLAlchemy
- **Authentication**: JWT (JSON Web Tokens)
- **Password Hashing**: bcrypt via passlib
- **Testing**: pytest, TestClient
- **Environment Management**: python-dotenv

## Project Structure

task-manager/
├── main.py          # Main application file with API endpoints

├── test.py          # Comprehensive test suite

├── requirements.txt # Python dependencies

├── .env             # Environment variables (not included in repo)

└── README.md        # This file

## Installation

1. **Clone the repository**
   ```bash
   git clone <https://github.com/KoAt-DEV/task_manager_api>
   cd task-manager
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Set up PostgreSQL databases**
   - Create a main database for the application
   - Create a separate test database for running tests

4. **Configure environment variables**
   
   Create a `.env` file in the root directory:
   ```env
   DB_USERNAME=your_db_username
   DB_PASSWORD=your_db_password
   DB_HOST=localhost
   DB_PORT=5432
   DB_NAME=your_main_database_name
   TEST_DB_NAME=your_test_database_name
   SECRET_KEY=your_super_secret_jwt_key
   ```

## Usage

### Starting the Server

```bash
uvicorn main:app --reload
```

The API will be available at `http://localhost:8000`

### API Documentation

Once the server is running, visit:
- **Swagger UI**: `http://localhost:8000/docs`
- **ReDoc**: `http://localhost:8000/redoc`

### API Endpoints

#### Authentication
- `POST /register` - Register a new user
- `POST /token` - Login and get access token

#### Tasks
- `POST /tasks/` - Create a new task
- `GET /tasks` - Get all tasks for authenticated user
- `GET /tasks/{task_id}` - Get specific task by ID
- `PUT /tasks/{task_id}` - Update a task
- `DELETE /tasks/{task_id}` - Delete a task

## Testing

Run the test suite:

```bash
pytest test.py -v
```

### Test Coverage

The test suite covers:
- User registration and authentication
- Task creation, retrieval, updating, and deletion
- User isolation (users cannot access other users' tasks)
- Error handling for non-existent resources
- Invalid authentication attempts

## Database Schema

### Users Table
- `id`: Primary key (Integer)
- `username`: Unique username (String)
- `hashed_password`: Bcrypt hashed password (String)

### Tasks Table
- `id`: Primary key (Integer)
- `title`: Task title (String)
- `description`: Task description (String)
- `completed`: Task completion status (Boolean)
- `owner`: Username of task owner (String)

## Security Features

- **Password Hashing**: Uses bcrypt for secure password storage
- **JWT Tokens**: Secure token-based authentication with 30-minute expiration
- **User Isolation**: Users can only access their own tasks
- **Environment Variables**: Sensitive data stored in environment variables

## License

This project is open source and available under the [MIT License](LICENSE).

## Troubleshooting

### Common Issues

- **Database Connection Error**: Ensure PostgreSQL is running and credentials in `.env` are correct
- **JWT Token Invalid**: Check if token has expired (30-minute lifetime)
- **Import Errors**: Make sure all dependencies are installed

### Environment Setup

Make sure your `.env` file is properly configured and not committed to version control. Add `.env` to your `.gitignore` file.

## Future Enhancements

- Task due dates and reminders
- Email notifications