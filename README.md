
## API Endpoints

### 1. **User Registration**
- **Endpoint**: `/api/register`
- **Method**: `POST`
- **Description**: Registers a new user in the system.
- **Request Body**:
    ```json
    {
      "username": "string",
      "password": "string",
      "email": "string"
    }
    ```
- **Response**:
    - `200 OK`: Registration successful
    - `400 Bad Request`: Missing or invalid data

### 2. **User Login**
- **Endpoint**: `/api/login`
- **Method**: `POST`
- **Description**: Logs in a user and returns a JWT token for authentication.
- **Request Body**:
    ```json
    {
      "username": "string",
      "password": "string"
    }
    ```
- **Response**:
    - `200 OK`: Successful login, returns JWT token
    - `401 Unauthorized`: Invalid credentials

### 3. **Enter Quiz Code**
- **Endpoint**: `/api/enterquizcode`
- **Method**: `POST`
- **Description**: Allows a user to enter a quiz code to begin the quiz.
- **Request Body**:
    ```json
    {
      "quizcode": "string"
    }
    ```
- **Response**:
    - `200 OK`: Quiz code accepted, quiz starts
    - `400 Bad Request`: Invalid quiz code

### 4. **Submit Quiz**
- **Endpoint**: `/api/submitquiz`
- **Method**: `POST`
- **Description**: Submits the user's answers and calculates the result.
- **Request Body**:
    ```json
    {
      "quizcode": "string",
      "answers": [
        { "questionId": 1, "selectedOption": 1 },
        { "questionId": 2, "selectedOption": 3 },
        ...
      ]
    }
    ```
- **Response**:
    - `200 OK`: Submission successful, returns result
    - `400 Bad Request`: Invalid data or incomplete answers

### 5. **View Results**
- **Endpoint**: `/api/result`
- **Method**: `GET`
- **Description**: Retrieves the results of the quiz for a specific user.
- **Query Parameters**:
    - `username`: The username of the user
- **Response**:
    - `200 OK`: Returns result data
    - `404 Not Found`: No result found for the user

### 6. **View Leaderboard**
- **Endpoint**: `/api/leaderboard`
- **Method**: `GET`
- **Description**: Retrieves the leaderboard for the quiz, sorted by score.
- **Response**:
    - `200 OK`: Returns a list of top users and their scores
    - `400 Bad Request`: Invalid request parameters

### 7. **View Answer Key**
- **Endpoint**: `/api/viewanswers`
- **Method**: `GET`
- **Description**: Allows the user to view their selected answers for a quiz.
- **Query Parameters**:
    - `username`: The username of the user
    - `quizcode`: The quiz code of the quiz attempted
- **Response**:
    - `200 OK`: Returns the answers and the questions the user attempted
    - `404 Not Found`: User or quiz not found

## Authentication

All endpoints (except for `register` and `login`) require a valid JWT token for access. To obtain a token, users must log in via the `/api/login` endpoint.

Include the JWT token in the `Authorization` header as a Bearer token:

