# Project: SpringBoot - API for Doctors and Patients Management

This project is a REST API built with **Spring Boot**. The objective of the project is to manage the registration of doctors and patients for a fictional medical clinic, as well as provide endpoints to manipulate this information.

## Features

The application offers various features that allow:

1.  **Doctors Management**:
    
    -   Registration of doctors.
    -   Listing of doctors with pagination.
    -   Updating doctors' information.
    -   Logical deletion of doctors (soft delete).
2.  **Patients Management**:
    
    -   Registration of patients.
    -   Listing of patients with pagination.
3.  **Validations and Error Handling**:
    
    -   Validation of data such as email, phone, CRM, ZIP code, among others.
    -   Appropriate error responses, returning HTTP 400 or 404 when necessary.
4.  **Authentication and Security**:
    
    -   Authentication using JWT (JSON Web Token).
    -   Access control to the endpoints.

## Main Technologies Used

-   **Java 17**: Programming language used for development.
-   **Spring Boot**: Framework for agile application development.
-   **Spring Data JPA**: For database abstraction and manipulation.
-   **Bean Validation**: For data validation using annotations.
-   **Spring Security**: For API authentication and security.
-   **Lombok**: To reduce boilerplate code.
-   **H2 Database**: In-memory database for development and testing.
-   **JUnit and Mockito**: For automated testing.

## Project Structure

The project follows a well-defined layered architecture:

1.  **`controller`**:
    
    -   Layer that manages the API endpoints.
    -   Contains methods to handle doctors, patients, and authentication.
2.  **`domain`**:
    
    -   Contains the main system entities such as `Doctor`, `Patient`, and `Address`.
    -   Also includes repositories (interfaces extending `JpaRepository`) and DTO classes for client-server communication.
3.  **`infra`**:
    
    -   API configurations.
    -   Implementations for security and JWT authentication.
    -   Global error handling.

## Available Endpoints

### Authentication

#### **POST /login**

Endpoint for user authentication in the system.

-   **Request**:


``` json
  {
     "login": "exampleuser",
     "password": "examplepassword"
  }
```
- **Resposta**:
    - HTTP 200 (OK):
``` json
    {
      "token": "jwt-generated-by-api"
    }
```


-   HTTP 401 (Unauthorized): If credentials are incorrect.

### Doctors

#### **POST /doctors**

Registers a new doctor in the system.

-   **Request**:


``` json
  {
    "name": "example",
  "email": "example@voll.med",
  "crm": "example",
  "phone": "example",
  "specialty": "example",
  "address": {
    "street": "example",
    "neighborhood": "example",
    "zipCode": "example",
    "city": "example",
    "state": "example",
    "number": "example",
    "complement": "example"
    }
  }
```

-   **Responses**:
    -   **201 (Created)**: Doctor successfully registered.
    -   **400 (Bad Request)**: When provided data is invalid.

#### **GET /doctors**

Lists all registered doctors with pagination.

-   **Optional URL Parameters**:
    
    -   `page`: Page number (default: 0).
    -   `size`: Page size (default: 10).
    -   `sort`: Sorting field (e.g., name, email).
-   **Response**:
    


``` json
  {
    "content": [
      {
      	 "id": 1,
      	 "name": "example",
      	 "email": "example@voll.med",
      	 "crm": "example",
      	 "phone": "example",
      	 "specialty": "example"
      },
      {
         "id": 2,
      	 "name": "example",
      	 "email": "example@voll.med",
      	 "crm": "example",
      	 "phone": "example",
      	 "specialty": "example"
      }
    ],
    "totalElements": 2,
    "totalPages": 1,
    "number": 0,
    "size": 10
  }
```

#### **PUT /doctors/{id}**

Updates information of a registered doctor.

-   **Request**:


``` json
  {
        "name": "example",
  	"phone": "example"
  }
```

-   **Response**:
    -   **200 (OK)**: Doctor's data successfully updated.
    -   **404 (Not Found)**: If the doctor is not found.

#### **DELETE /doctors/{id}**

Deletes a doctor from the system (soft delete).

-   **Response**:
    -   **204 (No Content)**: Deletion successfully performed.
    -   **404 (Not Found)**: If the doctor is not found.

### Patients

#### **POST /patients**

Registers a new patient in the system.

-   **Request**:


``` json
  {
    "name": "Example Name",
    "email": "exampleemail@gmail.com",
    "phone": "example",
    "cpf": "example",
    "address": {
    "street": "example",
    "neighborhood": "example",
    "zipCode": "example",
    "city": "example",
    "state": "example",
    "number": "example",
    "complement": "example"
    }
  }
```


-   **Responses**:
    -   **201 (Created)**: Patient successfully registered.
    -   **400 (Bad Request)**: When provided data is invalid.

#### **GET /patients**

Lists all registered patients with pagination.

-   **Optional URL Parameters**:
    -   `page`: Page number (default: 0).
    -   `size`: Page size (default: 10).

## Environment Setup

1.  **Prerequisites**:
    
    -   Java 17 installed.
    -   Maven installed.
2.  **Steps**:
    
    1.  Clone the repository:

bash


`git@github.com:GiovanneSilva/Consulta-Medico-API-SpringBoot.git` 

2.  Run the project:

bash


`./mvnw spring-boot:run` 

3.  The server will be available at:

arduino


`http://localhost:8080` 

## Automated Tests

The project implements integration tests using JUnit 5 and MockMvc to validate the endpoints.

-   To run the tests, execute:

bash


`./mvnw test` 

## License

This project is licensed under the MIT License.
