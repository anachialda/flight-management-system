# Flight Management System

A web application built with Spring Boot for managing flights, airplanes, passengers, tickets, luggage, employees, notice boards, and flight assignments.

This project was developed for the **Advanced Programming Methods (MAP)** course at **Babeș-Bolyai University**.

---

<img width="1438" height="769" alt="Screenshot 2026-03-11 at 10 57 55" src="https://github.com/user-attachments/assets/30630a80-ba7c-4806-97bb-7122d3711005" />
<img width="1219" height="769" alt="Screenshot 2026-03-11 at 10 58 22" src="https://github.com/user-attachments/assets/6dc82c33-a509-41e3-b12a-e8ab56fcfc6d" />
<img width="886" height="573" alt="Screenshot 2026-03-11 at 10 59 32" src="https://github.com/user-attachments/assets/cd2314ea-09a6-4221-8704-347395f4d800" />


## Tech Stack

**Backend**
- Java 17
- Spring Boot
- Spring Web
- Spring Data JPA
- Hibernate
- Spring Validation

**Database**
- MySQL

**Frontend**
- Thymeleaf
- Bootstrap
- HTML / CSS

**Build Tool**
- Maven

---

## Project Structure

The application is organized into several layers:

- **model** – entity classes and enums that define the domain
- **repository** – Spring Data JPA repositories used for database access
- **service** – business logic, filtering logic, and validation rules
- **controller** – web controllers responsible for handling HTTP requests
- **config** – application initialization and configuration

This structure separates database access, business logic, and request handling.

---

## Main Entities

The core domain entities are:

- Flight  
- Airplane  
- Passenger  
- Ticket  
- Luggage  
- AirlineEmployee  
- AirportEmployee  
- NoticeBoard  
- FlightAssignment  

Supporting enums and base types include:

- Role  
- Department  
- Designation  
- Status  
- Staff  
- Identifiable  

These entities are connected through relational mappings implemented with JPA.

---

## Application Features

The system provides management functionality for airline-related data.

Main capabilities include:

- CRUD operations for the core entities
- relational mapping between entities
- filtering using Spring Data JPA Specifications
- database-level sorting
- in-memory sorting for derived values

---

## Filtering

Dynamic filtering is implemented using **Spring Data JPA Specifications**.

Examples include:

**Flights**
- filter by flight id
- filter by flight status
- filter by departure interval

**Tickets**
- filter by ticket id
- filter by passenger name
- filter by flight name

**Passengers**
- filter by id
- filter by name
- filter by currency

**Luggage**
- filter by id
- filter by ticket id
- filter by status

**Airplanes**
- filter by id
- filter by airplane number
- filter by flight count interval

Filtering logic is implemented in the service layer using `Specification`.

---

## Sorting

Two types of sorting are used:

### Database Sorting
Spring Data `Sort` is used for fields that exist directly in the database.

### In-Memory Sorting
Some values are derived and therefore sorted in memory.

Examples:

- passengers sorted by **number of tickets**
- airplanes sorted by **number of flights**

---

## Business Rules Implemented

Several domain rules are enforced inside the service layer:

- a flight cannot arrive before its departure time
- arrival and departure times cannot be equal
- the same seat cannot be booked twice on the same flight
- a passenger with future flights cannot be deleted
- luggage must be associated with an existing ticket
- airplane ids must remain unique
- airplane numbers must remain unique
- entity ids are validated for uniqueness during creation

These checks help keep the domain data consistent.

---

## Database Initialization

The project includes a `DataInitializer` class that implements `CommandLineRunner`.

When the application starts:

1. existing records are cleared
2. sample data is inserted into the database

The initializer populates tables such as:

- airplanes
- notice boards
- passengers
- airline employees
- airport employees
- flights
- tickets
- flight assignments
- luggage

This allows the application to be tested immediately without manual data entry.

---

## Running the Project

### Prerequisites

You need:

- Java 17 or higher
- Maven
- MySQL running locally

---

### Database Configuration

Configure the database connection in `application.properties`.

Example configuration:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/flightDB?createDatabaseIfNotExist=true&useSSL=false&serverTimezone=UTC
spring.datasource.username=root
spring.datasource.password=YOUR_PASSWORD

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true


Start the Application

Build and run the project:

mvn clean install
mvn spring-boot:run

Then open the application in your browser:

http://localhost:8080



Notes:

- the application uses server-side rendering with Thymeleaf

- the project includes a simple /api/hello endpoint for testing the application

- the database is seeded automatically at startup through CommandLineRunner



Authors:
- Ana Chialda
- Andreea Maria Badiu




