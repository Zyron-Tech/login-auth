# API Documentation: User Login

## Endpoint:
**URL**: `/login.php`


## Description:
This endpoint allows users to log in to the system by providing their **email** and **password**. Upon successful authentication, a **token** is generated and returned, which can be used for subsequent authenticated requests.

## Request Headers:

- **Content-Type**: `application/json`
- **Authorization**: (Not required for this endpoint, but the token should be passed in the headers for protected routes after login)

## Request Body:
The request should include a JSON body with the following fields:

| Field     | Type   | Description                                    | Required |
|-----------|--------|------------------------------------------------|----------|
| email     | string | The user's email address                       | Yes      |
| password  | string | The user's password                            | Yes      |

### Example Request Body:
```json
{
    "email": "johndoe@example.com",
    "password": "123456"
}
```
## Response:
The response will be a JSON object with one of the following structures based on the request outcome:

1. Success (200 OK):
If the email and password match a registered user, a successful response will be returned with the user's information and a generated token.

Example Response (Success):
```
{
    "message": "Login successful",
    "user": {
        "id": 1,
        "email": "johndoe@example.com"
    },
    "token": "a1b2c3d4e5f6789012345678"
}
```
2. Error: Invalid Email Format (400 Bad Request):
If the email is not in a valid format.

Example Response (Invalid Email Format):
```
{
    "error": "Invalid email format"
}
```
3. Error: Missing Fields (400 Bad Request):
If either email or password is missing in the request.

Example Response (Missing Fields):
```
{
    "error": "Email and Password are required"
}
```
4. Error: Email Does Not Exist (404 Not Found):
If the email does not exist in the system.

Example Response (Email Not Found):
```
{
    "error": "Email does not exist"
}
```
5. Error: Incorrect Password (401 Unauthorized):
If the password provided does not match the stored password for the provided email.

Example Response (Incorrect Password):
```
{
    "error": "Incorrect password"
}
```
6. Error: Database Connection Failure (500 Internal Server Error):
If there is a problem connecting to the database.

Example Response (Database Error):
```
{
    "error": "Database connection failed"
}
```
