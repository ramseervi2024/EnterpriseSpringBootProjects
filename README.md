# Enterprise Spring Boot Projects

A collection of production-style Java Spring Boot applications built from scratch to develop and demonstrate practical backend engineering skills, enterprise application architecture, REST API development, security, database design, business logic, testing, and deployment concepts.

This repository contains three independent full-stack Spring Boot projects. Each project includes a REST API backend and a Thymeleaf-based web interface so that backend functionality can be developed, tested, and visually verified in parallel.

---

## 📌 Repository Purpose

The purpose of this repository is to build realistic enterprise applications rather than simple CRUD demonstrations.

The projects focus on:

* Java backend development
* Spring Boot
* REST API development
* Spring Security
* JWT authentication
* BCrypt password encryption
* Role-Based Access Control
* JPA/Hibernate
* MySQL
* Business logic
* Database transactions
* Validation
* Exception handling
* Pagination
* Filtering
* Sorting
* Audit logging
* Thymeleaf
* Unit testing
* Integration testing
* Swagger/OpenAPI
* Redis
* Docker
* AWS
* Production-oriented architecture

The repository is also designed to support deep technical interview preparation by documenting the reasoning behind architectural and business decisions.

---

# 📂 Repository Structure

```text
EnterpriseSpringBootProjects/
│
├── README.md
├── ProjectGuide.md
│
├── 01-Enterprise-Commerce/
│   ├── ProjectGuide.md
│   ├── README.md
│   ├── pom.xml
│   └── src/
│
├── 02-MultiTenant-SaaS/
│   ├── ProjectGuide.md
│   ├── README.md
│   ├── pom.xml
│   └── src/
│
├── 03-FinTech-Wallet/
│   ├── ProjectGuide.md
│   ├── README.md
│   ├── pom.xml
│   └── src/
│
├── shared/
│   ├── interview-notes/
│   ├── architecture/
│   ├── database/
│   └── api-docs/
│
└── docs/
    ├── java/
    ├── spring-boot/
    ├── spring-security/
    ├── jpa-hibernate/
    ├── mysql/
    ├── redis/
    ├── docker/
    └── aws/
```

---

# 🚀 Projects

## 01 — Enterprise Commerce Platform

A production-style B2B/B2C commerce and order management platform.

### Core Modules

* User Management
* Authentication
* Authorization
* Role Management
* Vendor Management
* Product Management
* Category Management
* Inventory
* Cart
* Wishlist
* Address Management
* Coupons
* Pricing
* Tax
* Orders
* Order Items
* Payments
* Refunds
* Notifications
* Audit Logs
* Admin Dashboard
* Vendor Dashboard
* Buyer Dashboard

### Roles

```text
ADMIN
VENDOR
BUYER
```

### Key Backend Concepts

* JWT Authentication
* BCrypt Password Encryption
* RBAC
* REST APIs
* DTO Architecture
* JPA/Hibernate
* Transactions
* Inventory Concurrency
* Pagination
* Dynamic Filtering
* Payment Processing
* Order State Management
* Audit Logging

---

# 02 — Multi-Tenant SaaS Project Management Platform

A SaaS platform where multiple organizations can manage teams, projects and tasks while maintaining organization-level data isolation.

### Core Modules

* Organization Management
* User Management
* Team Management
* Roles
* Permissions
* Projects
* Tasks
* Task Comments
* Attachments
* Invitations
* Notifications
* Activity Timeline
* Audit Logs
* Dashboard
* Search
* Filtering
* Pagination

### Key Backend Concepts

* Multi-Tenancy
* Organization Data Isolation
* RBAC
* JWT
* Refresh Tokens
* Permission Management
* REST APIs
* Database Relationships
* Audit Trails
* Scheduled Jobs
* Redis
* WebSocket Notifications

---

# 03 — FinTech Wallet & Transaction Platform

A financial transaction platform focused on secure money movement, transactional consistency, concurrency, idempotency and auditability.

### Core Modules

* User Management
* Authentication
* KYC
* Wallet Management
* Wallet Balance
* Add Money
* Withdraw
* Wallet-to-Wallet Transfer
* Transactions
* Ledger
* Payments
* Refunds
* Transaction Limits
* Transaction Status
* Reconciliation
* Notifications
* Audit Logs
* Admin Dashboard

### Key Backend Concepts

* ACID Transactions
* `@Transactional`
* Optimistic Locking
* Pessimistic Locking
* Idempotency
* Transaction State Management
* Ledger Design
* Concurrency Control
* Financial Audit Trails
* JWT Security
* RBAC

---

# 🛠 Technology Stack

## Backend

| Technology         | Purpose                        |
| ------------------ | ------------------------------ |
| Java 17+           | Programming Language           |
| Spring Boot        | Backend Framework              |
| Spring MVC         | REST/Web Layer                 |
| Spring Data JPA    | Persistence                    |
| Hibernate          | ORM                            |
| Spring Security    | Authentication & Authorization |
| JWT                | Stateless Authentication       |
| BCrypt             | Password Encryption            |
| Jakarta Validation | Request Validation             |
| Maven              | Build Management               |

## Database

* MySQL
* JPA/Hibernate
* SQL
* Database Indexing
* Foreign Keys
* Constraints
* Transactions

## Frontend

* Thymeleaf
* HTML
* CSS
* JavaScript
* Bootstrap

Thymeleaf is intentionally used in all projects so that the backend APIs and business logic can be verified through a functional web interface.

## Development & Testing

* IntelliJ IDEA
* Postman
* Swagger/OpenAPI
* JUnit 5
* Mockito
* MockMvc
* Git
* GitHub

## Infrastructure

* Docker
* Redis
* AWS

---

# 🏗 Architecture

The projects primarily follow a layered enterprise architecture.

```text
                    Client
                      │
             ┌────────┴────────┐
             │                 │
        Thymeleaf           REST API
             │                 │
             └────────┬────────┘
                      │
                 Controller
                      │
                      ▼
                   DTO
                      │
                      ▼
                  Service
                      │
                      ▼
                 Repository
                      │
                      ▼
                   JPA
                      │
                      ▼
                  Database
```

Supporting components:

```text
Security
   │
JWT
   │
Spring Security
   │
Authorization


Exception Handling
   │
GlobalExceptionHandler


Validation
   │
Jakarta Validation


Documentation
   │
Swagger / OpenAPI


Caching
   │
Redis


Testing
   │
JUnit / Mockito / MockMvc
```

---

# 🔐 Security Architecture

All projects implement secure authentication and authorization.

```text
Registration
     │
     ▼
Password Validation
     │
     ▼
BCrypt Hashing
     │
     ▼
Database
```

Login:

```text
Username / Email + Password
             │
             ▼
    AuthenticationManager
             │
             ▼
       UserDetailsService
             │
             ▼
       Password Verification
             │
             ▼
          JWT Token
```

Authenticated API request:

```text
HTTP Request
     │
     ▼
JWT Authentication Filter
     │
     ▼
JWT Validation
     │
     ▼
SecurityContext
     │
     ▼
Authorization
     │
     ▼
Controller
```

Passwords are never stored as plaintext.

---

# 🌐 REST API Standards

The applications use RESTful API design.

Example:

```text
POST   /api/v1/auth/register
POST   /api/v1/auth/login
POST   /api/v1/auth/refresh

GET    /api/v1/products
GET    /api/v1/products/{id}
POST   /api/v1/products
PUT    /api/v1/products/{id}
DELETE /api/v1/products/{id}

GET    /api/v1/orders
GET    /api/v1/orders/{id}
POST   /api/v1/orders
PUT    /api/v1/orders/{id}/cancel
```

APIs should support appropriate:

* HTTP methods
* HTTP status codes
* Request DTOs
* Response DTOs
* Validation
* Authentication
* Authorization
* Pagination
* Sorting
* Filtering
* Error handling

---

# 🗄 Database Philosophy

Database design is treated as an important part of application architecture.

Each project should contain:

```text
Requirements
     ↓
Domain Model
     ↓
ER Diagram
     ↓
Tables
     ↓
Relationships
     ↓
Indexes
     ↓
Constraints
     ↓
Application
```

Important database practices include:

* Normalization
* Foreign keys
* Unique constraints
* Indexes
* Proper data types
* Audit timestamps
* Transaction management
* Referential integrity

---

# 🧠 Business Logic

The projects intentionally contain realistic business workflows.

Example:

```text
Cart
 ↓
Checkout
 ↓
Validate User
 ↓
Validate Products
 ↓
Validate Inventory
 ↓
Calculate Price
 ↓
Apply Discount
 ↓
Calculate Tax
 ↓
Create Order
 ↓
Reserve Inventory
 ↓
Create Payment
 ↓
Clear Cart
 ↓
Send Notification
```

The objective is to understand the complete lifecycle of a business operation instead of implementing isolated CRUD APIs.

---

# 🧪 Testing Strategy

Testing is performed at multiple levels.

### Unit Testing

Tests individual business logic and service methods.

```text
Service
   ↓
JUnit + Mockito
```

### Controller Testing

Tests:

* Request validation
* HTTP status codes
* Authentication
* Authorization
* Response structure
* Error handling

### Integration Testing

Tests important application flows across multiple layers.

```text
Controller
    ↓
Service
    ↓
Repository
    ↓
Database
```

---

# 📖 Documentation

Each project contains its own documentation.

```text
ProjectGuide.md
README.md
API Documentation
Database Documentation
Architecture Documentation
Interview Notes
```

The root-level:

```text
ProjectGuide.md
```

contains the common development rules and instructions that AI coding assistants must follow across the entire repository.

---

# 🤖 AI Development Workflow

AI coding assistants working on this repository should follow:

```text
Read Root ProjectGuide.md
          ↓
Read Project ProjectGuide.md
          ↓
Understand Existing Code
          ↓
Understand Requirement
          ↓
Design Solution
          ↓
Implement
          ↓
Test
          ↓
Update Documentation
          ↓
Verify Existing Functionality
```

The AI should not blindly generate large amounts of code.

Each feature should be implemented incrementally and tested before moving to the next feature.

---

# 📚 Learning Progression

The projects are intentionally ordered by increasing backend complexity.

```text
Project 1
Enterprise Commerce
        │
        ▼
Spring Boot Fundamentals
REST APIs
Security
JPA
Business Logic
Transactions
        │
        ▼
Project 2
Multi-Tenant SaaS
        │
        ▼
Architecture
Multi-Tenancy
RBAC
Permissions
Scalability
        │
        ▼
Project 3
FinTech Wallet
        │
        ▼
Transactions
Concurrency
Idempotency
Ledger
Consistency
```

---

# 🎯 Interview Preparation

For every major feature, the repository should document:

### What?

What does the feature do?

### Why?

Why was the particular design selected?

### How?

How does the implementation work?

### Alternatives?

What other approaches could have been used?

### Edge Cases?

What can go wrong?

### Testing?

How is the functionality tested?

### Interview Questions?

What questions can be asked about the implementation?

Example:

```text
Feature: Order Creation

Interview Questions:

1. Why did you use @Transactional?
2. How do you prevent duplicate orders?
3. How do you handle inventory concurrency?
4. What happens if payment fails?
5. What happens if the database transaction rolls back?
6. How do you handle external API failures?
7. Why are DTOs used?
8. How would you optimize this API?
9. How would you scale this module?
10. How would you monitor failures?
```

---

# ⚠️ Important Principle

These projects are designed for **learning, technical practice and interview preparation**.

The implementation should be understood thoroughly before being described in any professional context.

The repository should distinguish between:

```text
Implemented
```

```text
Practiced
```

```text
Studied
```

```text
Conceptually Understood
```

Do not invent production metrics, clients, incidents, team sizes or business results.

The goal is to develop genuine understanding of enterprise Spring Boot development.

---

# 🚦 Getting Started

## 1. Clone the repository

```bash
git clone <repository-url>
cd EnterpriseSpringBootProjects
```

## 2. Read the project guides

Start with:

```text
ProjectGuide.md
```

Then open the guide for the project you want to work on.

## 3. Configure MySQL

Create the required database for the selected project.

Example:

```sql
CREATE DATABASE enterprise_commerce;
```

## 4. Configure environment variables

Example:

```text
DB_URL
DB_USERNAME
DB_PASSWORD
JWT_SECRET
```

Never commit secrets to Git.

## 5. Start the application

```bash
./mvnw spring-boot:run
```

or:

```bash
mvn spring-boot:run
```

## 6. Open the application

Example:

```text
http://localhost:8081
```

## 7. Test REST APIs

Use:

```text
Swagger UI
Postman
```

---

# 📌 Development Rule

Always build features incrementally.

```text
Requirement
    ↓
Database
    ↓
Entity
    ↓
Repository
    ↓
DTO
    ↓
Service
    ↓
Controller
    ↓
Security
    ↓
Thymeleaf UI
    ↓
Tests
    ↓
Swagger
    ↓
Documentation
```

Do not skip directly from requirement to a large generated codebase.

---

# 🔮 Future Improvements

Potential future enhancements include:

* Redis caching
* Docker Compose
* AWS deployment
* CI/CD
* Kafka
* Microservices
* API Gateway
* Service Discovery
* Distributed tracing
* Centralized logging
* Prometheus
* Grafana
* Elasticsearch
* Cloud storage
* Message queues

These should be introduced only when they solve an actual architectural requirement.

---

# ⭐ Repository Goal

The final repository should demonstrate a complete understanding of:

```text
Java
  +
Spring Boot
  +
Spring Security
  +
JWT
  +
JPA/Hibernate
  +
MySQL
  +
REST APIs
  +
Business Logic
  +
Transactions
  +
Thymeleaf
  +
Testing
  +
Redis
  +
Docker
  +
AWS
```

The primary goal is not the number of APIs or lines of code.

The goal is to understand how a real backend application is:

```text
Designed
    ↓
Developed
    ↓
Secured
    ↓
Tested
    ↓
Documented
    ↓
Deployed
    ↓
Maintained
```

---

## 📌 Current Projects

| #  | Project                      | Main Focus                               | Status         |
| -- | ---------------------------- | ---------------------------------------- | -------------- |
| 01 | Enterprise Commerce Platform | E-commerce, REST, Security, Transactions | 🚧 In Progress |
| 02 | Multi-Tenant SaaS            | Multi-tenancy, RBAC, Architecture        | ⏳ Planned      |
| 03 | FinTech Wallet               | Transactions, Concurrency, Idempotency   | ⏳ Planned      |

---

**Repository:** `EnterpriseSpringBootProjects`

**Primary Framework:** Spring Boot

**UI:** Thymeleaf

**Database:** MySQL

**Security:** Spring Security + JWT + BCrypt

**Build Tool:** Maven
