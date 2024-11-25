# Online Store Project

## Overview
The Online Store project is a user-friendly website enabling users to:
- View products
- Add items to their cart
- Place orders
- Manage their account

### Team Members
- Artur Šuškevitš
- Denis Goryunov
- Oleksandr Bohatyrov

---

## Table of Contents
1. [Idea and Requirements Analysis](#idea-and-requirements-analysis)
2. [Technical Analysis and Evaluation](#technical-analysis-and-evaluation)
3. [Planning and Design](#planning-and-design)
4. [Development](#development)
5. [Testing](#testing)
6. [Code Review](#code-review)
7. [Core Functions](#core-functions)
8. [Technology Stack](#technology-stack)
9. [Project Architecture](#project-architecture)
10. [Data Models](#data-models)
11. [Testing on Production Environment](#testing-on-production-environment)
12. [Release](#release)

---

## Idea and Requirements Analysis
- Build an online store with robust functionality.
- Provide a convenient, user-friendly interface for purchasing a variety of products.
- Develop a scalable system capable of handling high traffic loads.

---

## Technical Analysis and Evaluation

### Backend
- ASP.NET Core Web API (C#)
- Entity Framework (Embedded database)

### Frontend
- Blazor Web App
- RESTful API
- Version control with GitHub

---

## Planning and Design
- Utilize Blazor for internal styling and create custom designs using Figma.

### Task Management
- Manage tasks, roles, and Scrum meetings using JIRA.

---

## Development
- Code hosted and managed on GitHub.
- Regular commits with meaningful messages.
- Maintain clean, readable code with clear comments.

---

## Testing
Testing ensures that the application meets functional and non-functional requirements across different environments.

---

## Code Review

### General Feedback
1. **Repeated Logic**:
   - Duplicated logic exists across `CartsController` and `PaymentController`.
   - **Recommendation**: Extract shared functionality (e.g., retrieving a cart with its items) into a common service or private method.

2. **Logging**:
   - Logging is missing for error handling.
   - **Recommendation**: Use `ILogger` to track key events and issues.

3. **Security Issues**:
   - Passwords are stored without encryption. Use libraries like `Identity` or `BCrypt`.
   - No validation for user permissions to access sensitive resources.

4. **Error Handling**:
   - Missing global exception handling middleware for unexpected issues.

---

### Controller-Specific Feedback

#### CartsController
**Positive Aspects**:
- Proper use of `Include` and `ThenInclude` to handle nested entities.
- Good checks for empty cart and stock availability.

**Recommendations**:
1. Use transactions for critical operations like stock updates during checkout.
2. Extract repeated logic (e.g., retrieving carts) into private methods.
3. Add validation annotations to DTOs like `CartItemDto`.

#### PaymentController
**Positive Aspects**:
- Validates stock availability during checkout.

**Recommendations**:
1. Remove inappropriate placeholders (e.g., `"denis loh suka"`).
2. Consolidate overlapping logic with `CartsController` into a shared service.
3. Replace string-based responses with structured objects for better readability.

#### ProductsController
**Positive Aspects**:
- Implements standard CRUD operations effectively.
- Validates product existence with `ProductExists`.

**Recommendations**:
1. Add `ModelState` validation before saving data.
2. Ensure consistent error handling across all methods.

#### UsersController
**Positive Aspects**:
- Implements basic user registration and login checks.
- Passwords are hashed before storage.

**Recommendations**:
1. Replace outdated password hashing (e.g., SHA256 without a salt) with secure libraries like `BCrypt`.
2. Avoid returning sensitive user data. Instead, return tokens or minimal information.
3. Move password-related logic into a separate service for better maintainability.

---

## Core Functions
- Add products to the cart.
- Update and delete products.
- User registration and login.
- Password hashing.

---

## Technology Stack

### Frontend
- Blazor Web App
- JSON (for API communication)

### Backend
- RESTful API (client interaction)
- ASP.NET Core Web API (C#)
- Entity Framework (embedded database)

### Tools
- Git (version control)

---

## Project Architecture

### Directory Structure

/Github
- SolomikovPod
    - pages
    - services
- OnlineStoreApi
   - controllers
   - models
   
---

## Data Models

### Cart
| Field     | Type   |
|-----------|--------|
| Id        | int    |
| UserId    | int    |
| Items     | List<CartItem> |

### CartItem
| Field      | Type |
|------------|------|
| Id         | int  |
| ProductId  | int  |
| Quantity   | int  |
| CartId     | int  |

### Product
| Field       | Type    |
|-------------|---------|
| Id          | int     |
| Name        | string  |
| Description | string  |
| Price       | decimal |
| Stock       | int     |
| Currency    | string  |

### User
| Field         | Type    |
|---------------|---------|
| Id            | int     |
| Username      | string  |
| PasswordHash  | string  |
| Email         | string  |

---

## Testing on Production Environment
Pre-release testing will be performed in a production-like environment to ensure quality and performance.

---

## Release
- **Release Date**: 25.11.2024
- Deliverables will include the complete project, ready for deployment.
