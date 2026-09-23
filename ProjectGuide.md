# Enterprise Spring Boot Projects — Master Project Guide

## 1. PURPOSE

This repository contains three production-style Java Spring Boot projects created for deep Spring Boot learning, backend development practice, architecture understanding, REST API development, security, database design, business logic, testing, and interview preparation.

The projects must be developed as realistic enterprise applications.

The objective is NOT to create simple CRUD demonstrations.

Every project should contain realistic:

* Business requirements
* Database relationships
* Business rules
* REST APIs
* Authentication
* Authorization
* JWT security
* Password encryption
* Validation
* Exception handling
* Transactions
* Pagination
* Filtering
* Sorting
* Audit logging
* API documentation
* Thymeleaf UI
* Testing
* Production-oriented architecture

---

# 2. PROJECTS

## Project 1 — Enterprise Commerce Platform

Folder:

`01-Enterprise-Commerce`

Purpose:

Build a realistic B2B/B2C commerce and order management platform.

Major modules:

* Authentication
* User management
* Role management
* Product management
* Category management
* Vendor management
* Inventory
* Cart
* Wishlist
* Address
* Coupons
* Pricing
* Tax
* Orders
* Order items
* Payments
* Refunds
* Notifications
* Audit logs
* Admin dashboard
* Vendor dashboard
* Buyer dashboard

Roles:

* ADMIN
* VENDOR
* BUYER

---

## Project 2 — Multi-Tenant SaaS Project Management Platform

Folder:

`02-MultiTenant-SaaS`

Purpose:

Build a SaaS application where multiple organizations can use the same application while maintaining data isolation.

Major modules:

* Organization
* User
* Team
* Role
* Permission
* Project
* Task
* Task comments
* Attachments
* Notifications
* Activity logs
* Invitations
* Dashboard
* Search
* Filtering
* Pagination
* Audit logs

Roles should include appropriate organization-level and project-level permissions.

---

## Project 3 — FinTech Wallet & Transaction Platform

Folder:

`03-FinTech-Wallet`

Purpose:

Build a financial transaction platform focused on transaction consistency, security, concurrency, idempotency and auditability.

Major modules:

* Authentication
* User
* KYC
* Wallet
* Wallet balance
* Add money
* Withdraw
* Wallet transfer
* Transactions
* Ledger
* Payment
* Refund
* Transaction limits
* Transaction status
* Reconciliation
* Notifications
* Audit logs
* Admin dashboard

Important concepts:

* ACID transactions
* `@Transactional`
* Concurrency control
* Optimistic locking
* Pessimistic locking where appropriate
* Idempotency
* Transaction state management
* Financial audit trail

---

# 3. COMMON TECHNOLOGY STACK

All three projects should use the following stack unless there is a documented reason to change it.

## Backend

* Java 17+
* Spring Boot
* Spring MVC
* Spring Data JPA
* Hibernate
* Spring Security
* JWT
* Jakarta Validation
* Maven
* Lombok where appropriate

## Database

Primary database:

* MySQL

Use:

* Proper normalization
* Foreign keys
* Indexes
* Unique constraints
* Appropriate column types
* Timestamps
* Audit fields

## UI

Use:

* Thymeleaf
* HTML
* CSS
* JavaScript
* Bootstrap where useful

The UI must consume/use the same backend business logic.

Do NOT duplicate business logic inside Thymeleaf controllers.

Business logic belongs in the service layer.

## API

Use:

* REST
* JSON
* HTTP status codes
* DTOs
* Validation
* Pagination
* Filtering
* Sorting

## Documentation

Use:

* Swagger/OpenAPI
* README.md
* ProjectGuide.md
* API documentation
* Architecture documentation

## Testing

Use:

* JUnit 5
* Mockito
* Spring Boot Test
* MockMvc
* Integration tests where appropriate

## Tools

* IntelliJ IDEA
* MySQL
* Postman
* Git
* Docker
* Swagger UI

---

# 4. ARCHITECTURE

Use a clean layered architecture.

Preferred structure:

```text
controller
    ↓
service
    ↓
repository
    ↓
database
```

Supporting layers:

```text
config
security
dto
entity
mapper
exception
specification
util
audit
```

Example:

```text
src/main/java/com/company/project/

├── config/
├── controller/
├── dto/
│   ├── request/
│   └── response/
├── entity/
├── repository/
├── service/
├── service/impl/
├── security/
├── exception/
├── mapper/
├── specification/
├── audit/
└── util/
```

---

# 5. CONTROLLER RULES

Controllers must remain thin.

Controllers should:

* Receive HTTP requests
* Validate request DTOs
* Call services
* Return responses
* Handle HTTP-specific concerns

Controllers must NOT contain complex business logic.

BAD:

```java
if (product.getStock() > 0) {
    product.setStock(product.getStock() - 1);
}
```

inside controller.

GOOD:

```java
orderService.createOrder(request);
```

Business logic belongs inside the service layer.

---

# 6. SERVICE RULES

Services contain business logic.

Example:

```text
createOrder()
    ↓
validateUser()
    ↓
validateCart()
    ↓
validateInventory()
    ↓
calculatePrice()
    ↓
applyDiscount()
    ↓
calculateTax()
    ↓
reserveInventory()
    ↓
createOrder()
    ↓
createPayment()
```

Use `@Transactional` whenever multiple database operations must succeed or fail atomically.

---

# 7. REPOSITORY RULES

Use Spring Data JPA.

Repositories should handle database access only.

Do not put business rules inside repositories.

Use:

* JpaRepository
* derived queries
* JPQL
* native SQL only when justified
* Specifications for dynamic filtering
* projections where appropriate

---

# 8. ENTITY RULES

Entities must represent database persistence models.

Every appropriate entity should have:

```text
id
createdAt
updatedAt
createdBy
updatedBy
```

Use appropriate relationships:

* One-to-One
* One-to-Many
* Many-to-One
* Many-to-Many

Avoid blindly using `EAGER` fetching.

Prefer `LAZY` relationships unless there is a documented reason otherwise.

Avoid circular JSON serialization.

Do not expose JPA entities directly from REST APIs.

Use DTOs.

---

# 9. DTO RULES

Use separate request and response DTOs.

Example:

```text
ProductCreateRequest
ProductUpdateRequest
ProductResponse
```

Do not expose:

* Password
* Password hash
* Internal security fields
* Sensitive database fields

through API responses.

---

# 10. SECURITY

All projects must implement Spring Security.

Authentication:

```text
Register
    ↓
Password validation
    ↓
BCrypt hashing
    ↓
Database
```

Login:

```text
Username/email + password
        ↓
AuthenticationManager
        ↓
UserDetailsService
        ↓
Password verification
        ↓
JWT generation
```

Protected request:

```text
HTTP Request
    ↓
JWT Filter
    ↓
Validate JWT
    ↓
Extract user
    ↓
Set SecurityContext
    ↓
Authorization
    ↓
Controller
```

---

# 11. PASSWORD SECURITY

Passwords must NEVER be stored as plain text.

Use BCrypt:

```java
PasswordEncoder passwordEncoder =
        new BCryptPasswordEncoder();
```

Store only the BCrypt hash.

Never return password information in API responses.

---

# 12. JWT

Implement:

* Access token
* Refresh token
* Token expiration
* JWT validation
* Authentication filter
* Role-based authorization

Example:

```http
Authorization: Bearer <token>
```

Use role-based authorization such as:

```java
@PreAuthorize("hasRole('ADMIN')")
```

when appropriate.

---

# 13. AUTHORIZATION

Authentication answers:

> Who are you?

Authorization answers:

> What are you allowed to do?

Example:

```text
ADMIN
    → manage users
    → manage products
    → manage orders

VENDOR
    → manage own products
    → view own orders

BUYER
    → browse products
    → manage cart
    → create orders
```

Authorization must be enforced on the backend.

Never rely only on Thymeleaf UI visibility.

---

# 14. VALIDATION

Use Jakarta Validation.

Examples:

```java
@NotBlank
@Email
@Size
@Min
@Max
@NotNull
@Positive
```

Example:

```java
public class RegisterRequest {

    @NotBlank
    private String name;

    @Email
    @NotBlank
    private String email;

    @Size(min = 8)
    private String password;
}
```

Validation errors must return a consistent API response.

---

# 15. GLOBAL EXCEPTION HANDLING

Every project must have:

```text
GlobalExceptionHandler
```

Handle common exceptions such as:

* ResourceNotFoundException
* BadRequestException
* UnauthorizedException
* AccessDeniedException
* ValidationException
* DuplicateResourceException
* BusinessException

Use:

```java
@RestControllerAdvice
```

Return consistent responses.

Example:

```json
{
  "success": false,
  "message": "Product not found",
  "data": null
}
```

---

# 16. STANDARD API RESPONSE

Use a consistent response structure where appropriate.

Success:

```json
{
  "success": true,
  "message": "Product created successfully",
  "data": {}
}
```

Error:

```json
{
  "success": false,
  "message": "Product not found",
  "data": null
}
```

Do not force this wrapper onto responses where standard HTTP semantics are more appropriate.

---

# 17. PAGINATION

Large collections must not return unlimited records.

Use:

```text
page
size
sort
```

Example:

```http
GET /api/products?page=0&size=20&sort=name,asc
```

Response should contain pagination metadata.

---

# 18. DYNAMIC FILTERING

Where business requirements justify it, support:

* keyword search
* category
* status
* date range
* price range
* owner/user
* organization
* sorting

Use Spring Data Specifications where appropriate.

Example:

```text
GET /api/products
    ?keyword=laptop
    &category=electronics
    &minPrice=1000
    &maxPrice=50000
    &page=0
    &size=20
```

---

# 19. THYMELEAF UI

Every project must include a functional Thymeleaf UI.

The UI should provide practical screens for the major modules.

Example:

```text
/login
/register
/dashboard
/products
/products/{id}
/cart
/checkout
/orders
/orders/{id}
/profile
/admin
```

Thymeleaf should call the service layer.

Do not duplicate business rules between:

```text
REST Controller
```

and:

```text
Thymeleaf Controller
```

Both should ultimately use the same service layer.

---

# 20. BUSINESS LOGIC

Business logic must be realistic.

Do NOT create fake CRUD operations merely to increase the number of APIs.

Each important module should have:

* Validation
* State transitions
* Permission checks
* Business rules
* Error scenarios
* Transaction boundaries
* Audit requirements

Example order states:

```text
PENDING
CONFIRMED
PROCESSING
SHIPPED
DELIVERED
CANCELLED
REFUNDED
```

State transitions must be validated.

Do not allow arbitrary status changes.

---

# 21. DATABASE

Database design must happen before implementing complex modules.

For each project create:

```text
ER Diagram
Table definitions
Relationships
Indexes
Constraints
Sample data
```

Use foreign keys.

Use unique constraints where required.

Example:

```text
users.email UNIQUE
products.sku UNIQUE
```

---

# 22. TRANSACTIONS

Use transactions carefully.

Example:

```java
@Transactional
public OrderResponse createOrder(...) {
    ...
}
```

A transaction should ensure that related operations maintain consistency.

Do not add `@Transactional` everywhere without understanding the transaction boundary.

---

# 23. CONCURRENCY

Where inventory, wallet balance, task assignment or other shared resources are involved, consider concurrency.

Possible techniques:

* Optimistic locking
* Pessimistic locking
* Database constraints
* Atomic updates
* Idempotency

Use the appropriate technique based on the business requirement.

---

# 24. AUDIT LOGGING

Important actions should be auditable.

Example:

```text
User created
Product updated
Order cancelled
Payment initiated
Role changed
Wallet transfer created
```

Audit records should include appropriate information such as:

```text
actor
action
entity
entityId
timestamp
```

Do not log passwords, JWT tokens or sensitive secrets.

---

# 25. LOGGING

Use SLF4J/Logback.

Logs should help diagnose:

* authentication failures
* API errors
* business failures
* external API failures
* transaction failures

Never log:

* passwords
* access tokens
* refresh tokens
* payment secrets
* sensitive personal information

---

# 26. API DOCUMENTATION

Every REST API must be documented using OpenAPI/Swagger.

Document:

* endpoint
* HTTP method
* request
* response
* validation
* authorization requirement
* possible errors

Swagger should be available during development.

---

# 27. TESTING

Important business logic must have tests.

Minimum coverage should include:

### Unit tests

* Service methods
* Business rules
* Validation scenarios

### Controller tests

* Successful request
* Invalid request
* Unauthorized request
* Forbidden request
* Not found

### Integration tests

Where appropriate:

```text
Controller
    ↓
Service
    ↓
Repository
    ↓
Database
```

Do not write meaningless tests only to increase coverage percentage.

---

# 28. CODE QUALITY

Follow:

* meaningful class names
* meaningful method names
* single responsibility
* small methods
* proper exception handling
* reusable components
* no unnecessary duplication

Avoid:

```text
God classes
God methods
Huge controllers
Business logic in entities without reason
Business logic in controllers
Hard-coded credentials
Hard-coded secrets
Magic numbers
Duplicate code
```

---

# 29. CONFIGURATION

Use environment-based configuration.

Never hard-code:

```text
database password
JWT secret
API keys
payment secrets
AWS credentials
```

Use:

```text
application.yml
application-dev.yml
application-prod.yml
environment variables
```

Example:

```yaml
spring:
  datasource:
    url: ${DB_URL}
    username: ${DB_USERNAME}
    password: ${DB_PASSWORD}
```

---

# 30. API VERSIONING

Where appropriate, use:

```text
/api/v1/...
```

Example:

```text
/api/v1/auth/login
/api/v1/products
/api/v1/orders
```

Maintain backward compatibility when introducing new API versions.

---

# 31. DEVELOPMENT PROCESS

Do NOT build the entire project in one step.

Follow this sequence:

```text
1. Requirements
2. Domain modeling
3. Database design
4. Project setup
5. Entity design
6. Repository
7. DTO
8. Service
9. REST controller
10. Security
11. Exception handling
12. Thymeleaf UI
13. Testing
14. Swagger
15. Optimization
16. Documentation
```

Complete and test each module before moving to the next.

---

# 32. AI CODING RULES

When an AI assistant works on this repository:

1. Read this `ProjectGuide.md` before making changes.

2. Read the relevant project's `ProjectGuide.md`.

3. Understand the existing architecture before creating files.

4. Do not rewrite working code unnecessarily.

5. Do not introduce a new library without explaining why it is needed.

6. Do not change architecture without documenting the reason.

7. Do not remove existing functionality without explicit instruction.

8. Do not create duplicate classes.

9. Follow existing naming conventions.

10. Maintain backward compatibility when modifying APIs.

11. Update documentation when architecture or API behavior changes.

12. Add tests for important new business logic.

13. Never hard-code secrets.

14. Never store plaintext passwords.

15. Never expose passwords or sensitive security information.

16. Never put complex business logic inside controllers.

17. Never return JPA entities directly from public REST APIs.

18. Prefer DTOs.

19. Ask for clarification only when a requirement genuinely cannot be determined from the project documentation or existing code.

20. Before finishing a task, verify that the application still follows this guide.

---

# 33. DO NOT GENERATE FAKE SENIORITY

These projects are learning and interview-practice projects.

Do not invent:

* fake companies
* fake clients
* fake production incidents
* fake team sizes
* fake performance numbers
* fake users
* fake deployment statistics
* fake business results

When preparing interview explanations, distinguish between:

```text
Implemented personally
```

```text
Implemented as a practice project
```

```text
Concept understood
```

The goal is to understand the architecture deeply enough to explain it accurately.

---

# 34. INTERVIEW PREPARATION

For every major feature maintain documentation covering:

### What

What does the feature do?

### Why

Why was this approach selected?

### How

How does the implementation work?

### Alternatives

What alternatives were considered?

### Problems

What problems can occur?

### Solution

How are those problems handled?

### Interview questions

What questions can an interviewer ask about this feature?

Example:

```text
Feature:
Order creation

Questions:

1. Why did you use @Transactional?
2. What happens if payment fails?
3. How do you prevent duplicate orders?
4. How do you handle inventory concurrency?
5. What happens if the database transaction rolls back?
6. How do you handle an external payment timeout?
7. Why use DTOs?
8. How would you scale this API?
```

---

# 35. DEFINITION OF DONE

A feature is NOT complete merely because the code compiles.

A feature is complete when:

* Entity exists
* Database relationship works
* Repository works
* Service logic works
* REST API works
* Validation exists
* Exception handling exists
* Authorization is correct
* Thymeleaf UI works where applicable
* Tests exist
* Swagger documentation exists
* API has been tested
* Important edge cases are handled
* Documentation is updated

---

# 36. FINAL PRINCIPLE

Build these projects as if they were real enterprise systems.

Prefer:

```text
Correctness
Security
Maintainability
Business logic
Database consistency
Testability
Observability
Scalability
```

over:

```text
Writing the maximum amount of code
```

Every architectural decision should have a reason.

The objective is not to memorize code.

The objective is to understand:

```text
Requirement
    ↓
Architecture
    ↓
Database
    ↓
Business Logic
    ↓
REST API
    ↓
Security
    ↓
UI
    ↓
Testing
    ↓
Deployment
```

This repository should become a complete Spring Boot learning, development and interview-preparation environment.
