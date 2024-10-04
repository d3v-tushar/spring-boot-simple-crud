# Spring Boot MySQL CRUD Application

This project is a simple CRUD (Create, Read, Update, Delete) application built with Spring Boot and MySQL.

## Prerequisites

- Java 17 or later
- Maven
- Docker and Docker Compose

## Project Structure

```plaintext
src
├── main
│   ├── java
│   │   └── com
│   │       └── bhalow
│   │           └── api
│   │               ├── controller
│   │               │   └── UserController.java
│   │               ├── model
│   │               │   └── User.java
│   │               ├── repository
│   │               │   └── UserRepository.java
│   │               └── ApiApplication.java
│   └── resources
│       ├── application.properties
│       ├── static
│       └── templates
└── test
    └── java
        └── com
            └── bhalow
                └── api
                    └── ApiApplicationTests.java
```

## Running the Application

### Step 1: Start MySQL Database

We use Docker Compose to run the MySQL database. Make sure you have Docker and Docker Compose installed on your system.

1. Create a `docker-compose.yml` file in the root of your project with the following content:

   ```yaml
   version: '3.1'
   services:
     db:
       image: mysql:8.0
       restart: always
       environment:
         MYSQL_ROOT_PASSWORD: rootpassword
         MYSQL_DATABASE: userdb
         MYSQL_USER: user
         MYSQL_PASSWORD: password
       ports:
         - "3306:3306"
   ```

2. Run the following command to start the MySQL container:

   ```bash
   docker-compose up -d
   ```

   This will start the MySQL database in detached mode.

### Step 2: Run the Spring Boot Application

Once the database is up and running, you can start the Spring Boot application:

```bash
mvn spring-boot:run
```

The application should now be running and connected to the MySQL database.

## Testing the Application

You can use curl or any API testing tool like Postman to test the CRUD operations. Here are some example curl commands:

1. Create a user:

   ```bash
   curl -X POST http://localhost:8080/api/users -H "Content-Type: application/json" -d '{"name":"John Doe","email":"john@example.com"}'
   ```

2. Get all users:

   ```bash
   curl http://localhost:8080/api/users
   ```

3. Get a specific user (replace {id} with actual id):

   ```bash
   curl http://localhost:8080/api/users/{id}
   ```

4. Update a user (replace {id} with actual id):

   ```bash
   curl -X PUT http://localhost:8080/api/users/{id} -H "Content-Type: application/json" -d '{"name":"Jane Doe","email":"jane@example.com"}'
   ```

5. Delete a user (replace {id} with actual id):

   ```bash
   curl -X DELETE http://localhost:8080/api/users/{id}
   ```

## Stopping the Application

To stop the Spring Boot application, press `Ctrl + C` in the terminal where it's running.

To stop and remove the Docker containers, run:

```bash

docker-compose down

```

This will stop and remove the MySQL container
