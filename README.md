# User API - Spring Boot (STS)

A simple REST API that accepts username, email, and password, stores the password as a BCrypt hash, and retrieves users by ID or username.

## Requirements
- JDK 21
- Spring Tool Suite (STS) or another Java IDE
- Maven (STS can use the bundled Maven integration)

## Import into STS
1. Extract `UserApiSpringBoot.zip`.
2. Open STS.
3. Choose **File → Import → Maven → Existing Maven Projects**.
4. Select the extracted `UserApiSpringBoot` folder and finish.
5. Wait for Maven dependencies to download.
6. Open `UserApiApplication.java`, then choose **Run As → Spring Boot App**.

## API endpoints

### 1. Create a user
`POST http://localhost:8080/user`

Header: `Content-Type: application/json`

Body:
```json
{
  "username": "jayadeep",
  "email": "jayadeep@example.com",
  "password": "StrongPass123"
}
```

Example response (`201 Created`):
```json
{
  "id": 1,
  "username": "jayadeep",
  "email": "jayadeep@example.com"
}
```

### 2. Retrieve user by ID
`GET http://localhost:8080/user/1`

### 3. Retrieve user by username
`GET http://localhost:8080/user/username/jayadeep`

The API intentionally does not return the password. The database stores a BCrypt password hash, not the raw password.

## Test using Postman
1. Start the application.
2. Create a request, select **POST**, and enter `http://localhost:8080/user`.
3. Under **Body → raw → JSON**, paste the create-user JSON above and click **Send**.
4. Copy the returned `id`.
5. Create a **GET** request to `http://localhost:8080/user/1` or `http://localhost:8080/user/username/jayadeep`.

## Notes
- Uses an H2 in-memory database for easy local testing. Records disappear when the app stops.
- For a real deployment, add authentication/authorization, rate limiting, and a persistent database.
- Passwords are not returned by the retrieval endpoints.
