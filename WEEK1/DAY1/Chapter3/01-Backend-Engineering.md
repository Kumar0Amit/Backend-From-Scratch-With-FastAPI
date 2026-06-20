# Module 3 – Backend Engineering

---

# 3.1 Where Does Backend Fit?

By now, you understand:

* The Internet
* Clients and Servers
* Requests and Responses
* Network Protocols

Now let's answer one of the most important questions in backend development:

> **Where exactly does the backend fit in the overall architecture of a web application?**

When you use applications like Instagram, YouTube, Amazon, or ChatGPT, many components work together behind the scenes.

---

## A Modern Web Application

A typical web application consists of four major parts:

```text id="2qj7mf"
┌────────────┐
│ Frontend   │
└─────┬──────┘
      │
      ▼
┌────────────┐
│ Backend    │
└─────┬──────┘
      │
      ▼
┌────────────┐
│ Database   │
└─────┬──────┘
      │
      ▼
┌────────────────┐
│ Infrastructure │
└────────────────┘
```

Each component has a different responsibility.

---

## High-Level Flow

```text id="4b7xkp"
User

↓

Browser / Mobile App

↓

Frontend

↓

Backend

↓

Database

↓

Backend

↓

Frontend

↓

User
```

The backend sits **between the frontend and the database**, acting as the application's brain.

---

# Frontend

The **frontend** is everything the user sees and interacts with.

Examples include:

* Buttons
* Forms
* Images
* Menus
* Animations
* Colors
* Text

Common frontend technologies:

* HTML
* CSS
* JavaScript
* React
* Angular
* Vue

Example:

```text id="w8r3cm"
Instagram

❤️ Like Button

💬 Comment Button

📷 Photos

👤 Profile
```

Everything the user directly interacts with belongs to the frontend.

---

## Responsibilities of the Frontend

The frontend is responsible for:

* Displaying information
* Accepting user input
* Sending requests to the backend
* Receiving responses
* Updating the user interface

However, it usually does **not**:

* Access the database directly
* Process payments
* Store sensitive business logic
* Authenticate users independently

These tasks belong to the backend.

---

# Backend

The backend is the server-side application responsible for processing requests and performing the application's core logic.

**Definition**

> The backend is the part of an application responsible for processing client requests, executing business logic, interacting with databases and external services, and returning responses.

Think of the backend as the **brain** of the application.

It receives requests from clients, decides what should happen, performs the required work, and sends the result back.

---

## Responsibilities of the Backend

Typical backend responsibilities include:

* User authentication
* Authorization
* Business logic
* Database operations
* Payment processing
* Sending emails
* File uploads
* Calling external APIs
* Returning responses

Example:

User clicks:

```text id="t4j9pw"
Buy Now
```

Backend:

```text id="h7m2vd"
Check Inventory

↓

Calculate Total Price

↓

Apply Discounts

↓

Process Payment

↓

Create Order

↓

Update Database

↓

Return Success Response
```

The frontend simply displays the final result.

---

# Database

The **database** stores the application's persistent data.

Examples include:

* Users
* Products
* Orders
* Messages
* Posts
* Comments

Example:

```text id="z8v4nf"
Database

├── Users

├── Products

├── Orders

└── Payments
```

The database stores information.

It does **not** decide what should happen with that information.

Those decisions belong to the backend.

---

## Backend and Database

Clients should never communicate directly with the database.

Correct architecture:

```text id="u3r7kb"
Frontend

↓

Backend

↓

Database
```

Incorrect architecture:

```text id="w5n9gx"
Frontend

↓

Database
```

Allowing clients to access the database directly would expose sensitive information and bypass important business rules.

The backend acts as a secure gatekeeper.

---

## Example

User logs in.

Frontend sends:

```text id="m2k6zt"
Username

Password
```

↓

Backend:

```text id="j8r3mc"
Validate Input

↓

Check Database

↓

Verify Password

↓

Generate Token
```

↓

Database:

Returns user information.

↓

Backend:

Returns authentication response.

↓

Frontend:

Displays the dashboard.

---

# Infrastructure

Infrastructure is everything that allows your application to run.

It includes:

* Physical servers
* Cloud servers
* Operating systems
* Networking
* Storage
* Containers
* Load balancers
* Monitoring systems
* Security systems

Without infrastructure, your backend application would have nowhere to execute.

---

## Example Infrastructure

```text id="x5w8nd"
Cloud Provider

↓

Virtual Machine

↓

Linux

↓

Python

↓

FastAPI

↓

Application
```

Each layer supports the one above it.

---

# Browser

A browser is a **client**.

Examples:

* Chrome
* Edge
* Firefox
* Safari

Its responsibilities include:

* Displaying webpages
* Executing JavaScript
* Sending HTTP requests
* Receiving responses
* Rendering HTML and CSS

Example:

```text id="r4n7vq"
Browser

↓

GET /products

↓

Backend

↓

HTML or JSON

↓

Display Page
```

---

## Browser Does NOT Talk Directly to the Database

Incorrect:

```text id="k6p2jt"
Browser

↓

Database
```

Correct:

```text id="b7m4zc"
Browser

↓

Backend

↓

Database
```

The backend protects the database and enforces business rules before any data is accessed.

---

# Web Server

A **Web Server** is software that receives incoming HTTP or HTTPS requests.

Common web servers include:

* Nginx
* Apache HTTP Server
* Caddy

Its responsibilities include:

* Accepting HTTP requests
* Serving static files
* Managing HTTPS
* Forwarding requests to application servers
* Load balancing (in many deployments)

Example:

```text id="g8t5mr"
Browser

↓

Web Server

↓

Application Server
```

Think of the web server as the **front desk** of a building.

It receives visitors and directs them to the correct department.

---

## Why Use a Web Server?

Instead of exposing your application directly to the Internet,

a web server can:

* Handle thousands of simultaneous connections
* Serve static files efficiently
* Manage HTTPS certificates
* Improve security
* Forward requests to multiple backend instances

---

# Application Server

The **Application Server** runs your backend code.

For Python applications, common examples include:

* Uvicorn
* Hypercorn
* Gunicorn (with Uvicorn workers)

Its responsibilities include:

* Running your FastAPI application
* Executing business logic
* Processing requests
* Communicating with databases
* Generating responses

Example:

```text id="y2v9nc"
Browser

↓

Nginx

↓

Uvicorn

↓

FastAPI

↓

PostgreSQL
```

---

# Web Server vs Application Server

Many beginners confuse these two.

| Web Server                 | Application Server          |
| -------------------------- | --------------------------- |
| Receives HTTP requests     | Executes backend code       |
| Serves static files        | Runs business logic         |
| Handles HTTPS              | Communicates with databases |
| Can reverse proxy requests | Generates responses         |
| Example: Nginx             | Example: Uvicorn            |

---

# Complete Architecture

```text id="m8j2kd"
                  User
                    │
                    ▼
         Browser / Mobile App
               (Frontend)
                    │
          HTTP / HTTPS Request
                    │
                    ▼
              Web Server
             (Nginx/Apache)
                    │
                    ▼
         Application Server
       (Uvicorn + FastAPI)
                    │
          Business Logic
                    │
         ┌──────────┴──────────┐
         ▼                     ▼
    Database            External APIs
 (PostgreSQL)      (Payments, Email, etc.)
         │                     │
         └──────────┬──────────┘
                    ▼
            Generate Response
                    │
                    ▼
              Browser / App
                    │
                    ▼
                  User
```

---

# Real-World Example

Suppose you order food online.

### Step 1

Frontend:

```text id="c7m5rv"
Click "Place Order"
```

↓

### Step 2

Browser sends the request.

↓

### Step 3

Web Server receives it.

↓

### Step 4

Application Server (FastAPI):

* Validates the order
* Checks inventory
* Calculates price
* Creates the order

↓

### Step 5

Database stores:

* Order
* Customer
* Payment Details

↓

### Step 6

Application Server returns:

```json id="p4v7xn"
{
    "message": "Order Confirmed"
}
```

↓

### Step 7

Frontend displays:

```text id="d8j2mq"
Your order has been placed successfully.
```

---

## Why This Architecture?

Separating responsibilities makes applications:

* Easier to maintain
* More secure
* Easier to scale
* Simpler to test
* More reliable

Each component focuses on its own responsibility instead of trying to do everything.

---

## Summary

A modern web application consists of multiple components working together.

The frontend handles user interaction.

The backend contains the application's business logic.

The database stores persistent information.

Infrastructure provides the environment in which the application runs.

The browser acts as the client, while web servers and application servers work together to receive requests, execute backend code, and return responses.

Understanding where the backend fits makes it much easier to understand everything you'll build in later modules.

---

## Key Takeaways

* The backend sits between the frontend and the database.
* The frontend handles the user interface, while the backend processes requests and business logic.
* Databases store information but do not make application decisions.
* Browsers communicate with the backend, not directly with databases.
* Web servers receive requests and forward them to application servers.
* Application servers execute backend code and generate responses.
* Separating responsibilities makes applications more secure, scalable, and maintainable.

---

