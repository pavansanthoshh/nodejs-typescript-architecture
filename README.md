
 ## Project Directory Structure
 ```
├── src
│   ├── server.ts
│   ├── app.ts
│   ├── config.ts
│   ├── auth
│   │   ├── apikey.ts
│   │   ├── authUtils.ts
│   │   ├── authentication.ts
│   │   ├── authorization.ts
│   │   └── schema.ts
│   ├── core
│   │   ├── ApiError.ts
│   │   ├── ApiResponse.ts
│   │   ├── JWT.ts
│   │   └── Logger.ts
│   ├── database
│   │   ├── index.ts
│   │   ├── model
│   │   │   ├── ApiKey.ts
│   │   │   ├── Blog.ts
│   │   │   ├── Keystore.ts
│   │   │   ├── Role.ts
│   │   │   └── User.ts
│   │   └── repository
│   │       ├── ApiKeyRepo.ts
│   │       ├── BlogRepo.ts
│   │       ├── KeystoreRepo.ts
│   │       ├── RoleRepo.ts
│   │       └── UserRepo.ts
│   ├── helpers
│   │   ├── asyncHandler.ts
│   │   ├── role.ts
│   │   └── validator.ts
│   ├── routes
│   │   └── v1
│   │       ├── access
│   │       │   ├── login.ts
│   │       │   ├── logout.ts
│   │       │   ├── schema.ts
│   │       │   ├── signup.ts
│   │       │   └── token.ts
│   │       ├── blog
│   │       │   ├── blogDetail.ts
│   │       │   ├── blogList.ts
│   │       │   ├── editor.ts
│   │       │   ├── schema.ts
│   │       │   └── writer.ts
│   │       ├── index.ts
│   │       └── profile
│   │           ├── schema.ts
│   │           └── user.ts
│   └── types
│       └── app-request.d.ts
├── tests
│   ├── auth
│   │   ├── apikey
│   │   │   ├── mock.ts
│   │   │   └── unit.test.ts
│   │   ├── authUtils
│   │   │   ├── mock.ts
│   │   │   └── unit.test.ts
│   │   ├── authentication
│   │   │   ├── mock.ts
│   │   │   └── unit.test.ts
│   │   └── authorization
│   │       ├── mock.ts
│   │       └── unit.test.ts
│   ├── core
│   │   └── jwt
│   │       ├── mock.ts
│   │       └── unit.test.ts
│   ├── routes
│   │   └── v1
│   │       ├── blog
│   │       │   ├── blogDetail
│   │       │   │   ├── mock.ts
│   │       │   │   └── unit.test.ts
│   │       │   └── writer
│   │       │       ├── mock.ts
│   │       │       └── unit.test.ts
│   │       ├── login
│   │       │   ├── integration.test.ts
│   │       │   ├── mock.ts
│   │       │   └── unit.test.ts
│   │       └── signup
│   │           ├── mock.ts
│   │           └── unit.test.ts
│   ├── .env.test
│   └── setup.ts
├── addons
│   └── init-mongo.js
├── keys
│   ├── private.pem
│   └── public.pem
├── .env
├── .gitignore
├── .dockerignore
├── .eslintrc
├── .eslintignore
├── .prettierrc
├── .prettierignore
├── .travis.yml
├── .vscode
│   └── launch.json
├── Dockerfile
├── docker-compose.yml
├── package-lock.json
├── package.json
├── jest.config.js
└── tsconfig.json
 ```
 
 ## Directory Traversal for Signup API call
 `/src → server.ts → app.ts → /routes/v1/index.ts → /auth/apikey.ts → schema.ts → /helpers/validator.ts → asyncHandler.ts → /routes/v1/signup.ts → schema.ts → /helpers/validator.ts → asyncHandler.ts → /database/repository/UserRepo.ts → /database/model/User.ts → /core/ApiResponses.ts`
 
 ## API Examples
* Signup
    * Method and Headers
    ```
    POST /v1/signup/basic HTTP/1.1
    Host: localhost:3000
    x-api-key: GCMUDiuY5a7WvyUNt9n3QztToSHzK7Uj
    Content-Type: application/json
    ```
    * Request Body
    ```json
    {
        "name" : "pavansanthosh",
        "email": "pavansanthosh@gmail.com",
        "password": "changeit",
        "profilePicUrl": "https://avatars1.githubusercontent.com/u/11065002?s=460&u=1e8e42bda7e6f579a2b216767b2ed986619bbf78&v=4"
    }
    ```
    * Response Body: 200
    ```json
    {
      "statusCode": "10000",
      "message": "Signup Successful",
      "data": {
        "user": {
          "_id": "5e7c9d32307a223bb8a4b12b",
          "name": "pavansanthoshpeddinti",
          "email": "pavansanthoshpeddinti@gmail.com",
          "roles": [
            "5e7b8acad7aded2407e078d7"
          ],
          "profilePicUrl": "https://avatars1.githubusercontent.com/u/11065002?s=460&u=1e8e42bda7e6f579a2b216767b2ed986619bbf78&v=4"
        },
        "tokens": {
          "accessToken": "some_token",
          "refreshToken": "some_token"
        }
      }
    }
    ```
    * Response Body: 400
    ```json
    {
      "statusCode": "10001",
      "message": "Bad Parameters"
    }
    ```
* Profile Private
    * Method and Headers
    ```
    GET /v1/profile/my HTTP/1.1
    Host: localhost:3000
    x-api-key: GCMUDiuY5a7WvyUNt9n3QztToSHzK7Uj
    Content-Type: application/json
    Authorization: Bearer <your_token_received_from_signup_or_login>
    ```
    * Response Body: 200
    ```json
    {
      "statusCode": "10000",
      "message": "success",
      "data": {
        "name": "pavansanthosh",
        "profilePicUrl": "https://avatars1.githubusercontent.com/u/11065002?s=460&u=1e8e42bda7e6f579a2b216767b2ed986619bbf78&v=4",
        "roles": [
          {
            "_id": "5e7b8acad7aded2407e078d7",
            "code": "LEARNER"
          },
          {
            "_id": "5e7b8c22d347fc2407c564a6",
            "code": "WRITER"
          },
          {
            "_id": "5e7b8c2ad347fc2407c564a7",
            "code": "EDITOR"
          }
        ]
      }
    }
    ```
