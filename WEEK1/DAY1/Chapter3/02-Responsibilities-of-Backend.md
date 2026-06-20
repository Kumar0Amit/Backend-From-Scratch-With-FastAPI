# 3.2 Responsibilities of the Backend

Now that we know **where the backend fits** in a web application, the next question is:

> **What exactly does the backend do?**

Many beginners think:

> "The backend just connects to the database."

In reality, database communication is only **one** of its responsibilities.

A modern backend is responsible for making decisions, enforcing business rules, protecting data, communicating with external services, and returning appropriate responses to clients.

Think of the backend as the **brain and control center** of an application.

---

## High-Level Responsibilities

```text id="9n4mxt"
                Backend
                    │
    ┌───────────────┼────────────────┐
    │               │                │
Business Logic   Authentication   Validation
    │               │                │
    ├───────────────┼────────────────┤
    │               │                │
Authorization   Database Access   API Responses
    │               │                │
    └───────────────┼────────────────┘
                    │
              Error Handling
```

Let's understand each responsibility.

---

# Business Logic

Business logic is the **decision-making process** of an application.

**Definition**

> Business logic is the set of rules that determines how an application should behave.

Every application has its own rules.

Examples:

### Banking

* Balance cannot become negative.
* Daily withdrawal limits.
* Interest calculation.

---

### E-Commerce

* Product must be in stock.
* Apply discount coupons.
* Calculate taxes.
* Calculate shipping charges.

---

### College Portal

* Student must complete the required credits.
* No active backlogs.
* Attendance must meet the minimum requirement.

---

### Food Delivery

* Restaurant must be open.
* Delivery address must be serviceable.
* Delivery partner must be available.

---

The backend checks these rules before taking any action.

Example:

```text id="v2q6cn"
User Clicks "Buy Now"

↓

Backend

↓

Product Available?

↓

Yes

↓

Calculate Price

↓

Create Order

↓

Return Success
```

The frontend only displays the outcome.

---

# Authentication

Authentication answers one simple question:

> **Who are you?**

The backend verifies the identity of the user.

Common authentication methods include:

* Username and Password
* OTP
* Email Verification
* Google Login (OAuth)
* JWT Tokens
* Biometric authentication (through client devices)

Example:

```text id="m8r3dz"
Client

↓

Username: john

Password: secret123

↓

Backend

↓

Check Database

↓

Valid?

↓

Yes

↓

Generate Token
```

If the credentials are incorrect:

```json id="g5t9wy"
{
    "error": "Invalid username or password"
}
```

---

# Authorization (Overview)

Authentication tells the backend **who the user is**.

Authorization determines:

> **What is this user allowed to do?**

Example:

Administrator:

```text id="j6k8tv"
Delete Users

Allowed
```

Regular User:

```text id="c4x2bn"
Delete Users

Not Allowed
```

Workflow:

```text id="y7w5qm"
User Authenticated

↓

Check Permissions

↓

Allowed?

↓

Yes

↓

Continue
```

We'll study Role-Based Access Control (RBAC), permissions, and authorization policies in detail later.

---

## Authentication vs Authorization

| Authentication    | Authorization                   |
| ----------------- | ------------------------------- |
| Who are you?      | What can you do?                |
| Verifies identity | Verifies permissions            |
| Happens first     | Happens after authentication    |
| Example: Login    | Example: Delete User Permission |

---

# Validation

Validation ensures that incoming data is correct before processing it.

Imagine a registration request like this:

```text id="z9m4rh"
Name:

(empty)

Email:

hello

Age:

-10
```

Without validation, invalid data would be stored in the database.

The backend validates things such as:

* Required fields
* Email format
* Password strength
* Number ranges
* Dates
* Data types

Example:

```text id="k8t3cx"
POST /register

↓

Backend

↓

Email Valid?

↓

Yes

↓

Password Strong?

↓

No

↓

Return Error
```

---

## Why Validation Matters

Without validation:

* Invalid data enters the database.
* Security vulnerabilities increase.
* Unexpected errors occur.
* User experience suffers.

Validation is one of the backend's most important responsibilities.

---

# Database Communication

The backend acts as the bridge between clients and the database.

Clients should **never** communicate directly with the database.

Correct flow:

```text id="f7m2qn"
Browser

↓

Backend

↓

Database

↓

Backend

↓

Browser
```

The backend performs operations such as:

* Create
* Read
* Update
* Delete

These are commonly called **CRUD operations**.

Example:

```text id="d4v8pk"
GET /products

↓

Backend

↓

Database Query

↓

Return Products
```

---

# API Responses

After processing a request,

the backend sends a response to the client.

Responses may contain:

* JSON
* HTML
* Images
* Files
* PDFs
* Error messages

Example:

```json id="a5j7tr"
{
    "id": 1,
    "name": "John"
}
```

Another example:

```json id="m6k9qw"
{
    "message": "Order Created Successfully"
}
```

The frontend uses these responses to update the user interface.

---

## Good API Responses

A good API response should be:

* Correct
* Consistent
* Easy to understand
* Fast

Example:

```json id="t2x8pm"
{
    "success": true,
    "message": "User Created Successfully",
    "data": {
        "id": 101,
        "name": "John"
    }
}
```

---

# Error Handling (Overview)

Not every request succeeds.

Many things can go wrong.

Examples:

* Invalid input
* User not found
* Database unavailable
* Payment failed
* File too large
* Unexpected server error

Instead of crashing,

the backend should return meaningful error responses.

Example:

```json id="w4n6zk"
{
    "error": "Product not found"
}
```

Instead of:

```text id="g8p3mv"
Application Crashed
```

Good error handling:

* Prevents crashes
* Helps users understand the problem
* Helps developers debug issues
* Improves reliability

Later we'll study:

* Exceptions
* Logging
* Custom exception handlers
* HTTP status codes

---

# Complete Backend Workflow

Almost every request follows this general flow.

```text id="c6q8jw"
Client

↓

Request

↓

Authentication

↓

Authorization

↓

Validation

↓

Business Logic

↓

Database

↓

Generate Response

↓

Return Response
```

Some steps may be skipped depending on the endpoint, but this is the general lifecycle of a backend request.

---

## Real-World Example

Suppose a user places an order.

```text id="j9v2kc"
Click "Place Order"

↓

Backend

↓

Authentication

↓

Authorization

↓

Validate Order

↓

Check Inventory

↓

Calculate Total

↓

Save Order

↓

Generate Response

↓

Return Success
```

The user only sees:

```text id="v3m7qx"
Order Placed Successfully
```

Everything else happens inside the backend.

---

## Why These Responsibilities Belong to the Backend

Imagine allowing every client to make business decisions.

One client might calculate taxes differently.

Another might ignore stock availability.

Another might skip payment verification.

The application would become inconsistent and insecure.

By centralizing these responsibilities in the backend:

* Every client follows the same rules.
* Sensitive logic remains protected.
* Data stays consistent.
* Security improves.

Whether the client is:

* A browser
* A mobile app
* A desktop application
* Another backend service

everyone receives the same behavior because the backend enforces the rules.

---

## Summary

The backend is responsible for much more than simply communicating with a database.

It authenticates users, authorizes actions, validates incoming data, executes business logic, interacts with databases and external services, generates API responses, and handles errors.

Together, these responsibilities make the backend the central decision-making component of a modern application.

---

## Key Takeaways

* Business logic defines how the application behaves.
* Authentication verifies **who** the user is.
* Authorization determines **what** the user is allowed to do.
* Validation protects the application from invalid or malicious input.
* The backend communicates with databases on behalf of clients.
* API responses return the results of backend processing.
* Proper error handling makes applications more reliable and easier to maintain.
* The backend ensures every client follows the same business rules.

---

