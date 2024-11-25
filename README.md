Online Store Project
Overview

The Online Store project is a user-friendly website enabling users to:

    View products
    Add items to their cart
    Place orders
    Manage their account

Team Members

    Artur Šuškevitš
    Denis Goryunov
    Oleksandr Bohatyrov

Table of Contents

    Idea and Requirements Analysis
    Technical Analysis and Evaluation
    Planning and Design
    Development
    Testing
    Code Review
    Core Functions
    Technology Stack
    Project Architecture
    Data Models
    Testing on Production Environment
    Release

Idea and Requirements Analysis

    Build an online store with robust functionality.
    Provide a convenient, user-friendly interface for purchasing a variety of products.
    Develop a scalable system capable of handling high traffic loads.

Technical Analysis and Evaluation
Backend

    ASP.NET Core Web API (C#)
    Entity Framework (Embedded database)

Frontend

    Blazor Web App
    RESTful API
    Version control with GitHub

Planning and Design

    Utilize Blazor for internal styling and create custom designs using Figma.

Task Management

    Manage tasks, roles, and Scrum meetings using JIRA.

Development

    Code hosted and managed on GitHub.
    Regular commits with meaningful messages.
    Maintain clean, readable code with clear comments.

Testing

Testing will ensure the application meets functional and non-functional requirements across different environments.
Code Review
General Feedback

    Repeated Logic:
        Duplicated logic exists across CartsController and PaymentController.
        Recommendation: Extract shared functionality (e.g., retrieving a cart with its items) into a common service or private method.

    Logging:
        Logging is missing for error handling.
        Recommendation: Use ILogger to track key events and issues.

    Security Issues:
        Passwords are stored without encryption. Use libraries like Identity or BCrypt.
        No validation for user permissions to access sensitive resources.

    Error Handling:
        Missing global exception handling middleware for unexpected issues.

Controller-Specific Feedback
CartsController

Positive Aspects:

    Proper use of Include and ThenInclude to handle nested entities.
    Good checks for empty cart and stock availability.

Recommendations:

    Use transactions for critical operations like stock updates during checkout.
    Extract repeated logic (e.g., retrieving carts) into private methods.
    Add validation annotations to DTOs like CartItemDto.

PaymentController

Positive Aspects:

    Validates stock availability during checkout.

Recommendations:

    Remove inappropriate placeholders (e.g., "denis loh suka").
    Consolidate overlapping logic with CartsController into a shared service.
    Replace string-based responses with structured objects for better readability.

ProductsController

Positive Aspects:

    Implements standard CRUD operations effectively.
    Validates product existence with ProductExists.

Recommendations:

    Add ModelState validation before saving data.
    Ensure consistent error handling across all methods.

UsersController

Positive Aspects:

    Implements basic user registration and login checks.
    Passwords are hashed before storage.

Recommendations:

    Replace outdated password hashing (e.g., SHA256 without a salt) with secure libraries like BCrypt.
    Avoid returning sensitive user data. Instead, return tokens or minimal information.
    Move password-related logic into a separate service for better maintainability.

Core Functions

    Add products to the cart.
    Update and delete products.
    User registration and login.
    Password hashing.

Technology Stack
Frontend

    Blazor Web App
    JSON (for API communication)

Backend

    RESTful API (client interaction)
    ASP.NET Core Web API (C#)
    Entity Framework (embedded database)

Tools

    Git (version control)

Project Architecture
Directory Structure

/Github
├─── /SolomikovPod # Frontend sources (Blazor Web App)
│   ├─── /pages # Pages
│   ├─── /services # API services
├─── /OnlineStoreApi # Backend sources (ASP.NET Core Web API)
    ├─── /controllers # Request handling logic
    ├─── /models # Database schemas

Data Models
Cart
Field	Type
Id	int
UserId	int
Items	List<CartItem>
CartItem
Field	Type
Id	int
ProductId	int
Quantity	int
CartId	int
Product
Field	Type
Id	int
Name	string
Description	string
Price	decimal
Stock	int
Currency	string
User
Field	Type
Id	int
Username	string
PasswordHash	string
Email	string
Testing on Production Environment

Pre-release testing will be performed in a production-like environment to ensure quality and performance.
Release

    Release Date: 25.11.2024
    Deliverables will include the complete project, ready for deployment.
