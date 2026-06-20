# Module 4 – Journey of a Request

---

# 4.1 Journey of a Request (Bird's-Eye View)

So far, we've learned about:

* The Internet
* Protocols
* Clients
* Servers
* Backend
* Databases
* Web Servers
* Application Servers

Now it's time to connect all of these concepts together.

In this module, we'll follow the complete journey of a request—from the moment a user performs an action until the final response is displayed on the screen.

> **Important:** This is a high-level overview. We'll study technologies like DNS, TCP, TLS, HTTP, and ASGI in much greater detail in later modules.

---

## The Big Picture

Imagine you type the following URL into your browser:

```text id="j5k2qn"
https://example.com/products
```

and press **Enter**.

At first glance, it seems like a simple action.

```text id="n7w4pr"
Browser

↓

Server

↓

Webpage
```

In reality, many components work together before the webpage appears.

---

## Complete Journey

```text id="v9m6tx"
User
   │
   ▼
Browser
   │
   ▼
DNS Lookup
   │
   ▼
TCP Connection
   │
   ▼
TLS Handshake (HTTPS)
   │
   ▼
HTTP Request
   │
   ▼
Internet
(Routers / ISP)
   │
   ▼
Web Server
(Nginx)
   │
   ▼
Application Server
(Uvicorn)
   │
   ▼
FastAPI Backend
   │
   ▼
Business Logic
   │
   ▼
Database
(PostgreSQL)
   │
   ▼
Business Logic
   │
   ▼
HTTP Response
   │
   ▼
Internet
   │
   ▼
Browser
   │
   ▼
Render Page
   │
   ▼
User
```

This is the complete lifecycle of a typical web request.

Let's briefly understand each step.

---

# Step 1 — User Action

Every request begins with an action.

Examples:

* Opening a website
* Clicking a button
* Logging in
* Searching for something
* Refreshing a page
* Uploading a file

Example:

```text id="r3k8pb"
User

↓

Clicks Login
```

Without an action from a user (or another client), no request is created.

---

# Step 2 — Browser Creates the Request

The browser acts as the client.

Based on the user's action, it creates an HTTP request.

For example:

```text id="w2v9mh"
https://example.com/products
```

becomes something like:

```http id="m8q4jn"
GET /products
```

The browser prepares information such as:

* URL
* HTTP Method
* Headers
* Cookies
* Request Body (if needed)

This information is packaged into a request.

---

# Step 3 — DNS Lookup

As discussed in **Module 1**, computers communicate using **IP addresses**, not domain names.

The browser asks:

```text id="y5n2dt"
What is the IP address of example.com?
```

The DNS server replies:

```text id="d7k6pw"
example.com

↓

203.0.113.25
```

Now the browser knows where to send the request.

---

# Step 4 — TCP Connection

Before data can be exchanged,

the browser establishes a **TCP connection** with the destination server.

```text id="k9v4xb"
Browser

↓

TCP Connection

↓

Server
```

TCP provides reliable communication between the client and the server.

Once the connection is established,

both sides are ready to exchange data.

---

# Step 5 — TLS Handshake (HTTPS)

If the website uses **HTTPS**, communication must be secured before any sensitive information is exchanged.

The browser and server perform a **TLS Handshake**.

```text id="b4p8zn"
Browser

↓

TLS Handshake

↓

Secure Connection

↓

Server
```

After this step,

all communication between the client and server is encrypted.

---

# Step 6 — HTTP Request Travels

Now the browser sends the HTTP request.

Example:

```http id="g6t2rm"
GET /products
```

The request doesn't travel directly to the server.

It passes through several networking components.

```text id="q3m7kv"
Browser

↓

Wi-Fi

↓

Router

↓

ISP

↓

Internet

↓

Server
```

Routers determine the best path for the packets carrying the request.

---

# Step 7 — Web Server Receives the Request

The request first reaches a **Web Server** such as **Nginx**.

The web server is responsible for tasks like:

* Receiving HTTP requests
* Managing HTTPS
* Serving static files
* Forwarding dynamic requests to the application server

```text id="z8p5md"
Browser

↓

Nginx

↓

Application Server
```

In production environments, the backend application is usually not exposed directly to the Internet.

---

# Step 8 — Application Server

The request is forwarded to the **Application Server**.

For FastAPI applications, this is commonly:

```text id="m2r6qn"
Uvicorn
```

The application server:

* Runs your FastAPI application
* Passes incoming requests to your Python code
* Returns generated responses

---

# Step 9 — Backend Processing

Now your backend code begins executing.

Typical tasks include:

* Authentication
* Authorization
* Validation
* Business Logic
* Database Communication
* Calling External APIs

Example:

```text id="t4x8pj"
Receive Request

↓

Validate Input

↓

Authenticate User

↓

Execute Business Logic

↓

Query Database
```

This is where most backend development happens.

---

# Step 10 — Database

If the backend needs stored information,

it communicates with the database.

Example:

```text id="v5q3kr"
Backend

↓

SELECT * FROM products
```

The database returns the requested data.

The backend processes it before creating a response.

---

# Step 11 — Backend Creates the Response

After completing its work,

the backend creates an HTTP response.

Example:

```json id="j8w2mn"
{
    "id": 1,
    "name": "Laptop",
    "price": 50000
}
```

The response may contain:

* JSON
* HTML
* Images
* Files
* Error messages

---

# Step 12 — Response Travels Back

The response follows the reverse path.

```text id="x6m4pt"
Backend

↓

Application Server

↓

Web Server

↓

Internet

↓

Browser
```

The browser receives the response.

---

# Step 13 — Browser Renders the Result

If the response contains a webpage,

the browser:

* Parses HTML
* Applies CSS
* Executes JavaScript
* Draws the interface on the screen

If the response contains JSON,

the frontend code processes it and updates the interface.

---

# Step 14 — User Sees the Result

Finally,

the user sees the result.

Examples:

* Homepage
* Product list
* Login successful
* Search results
* Error message

The request lifecycle is now complete.

---

# Complete Example

Suppose you visit an online store.

You enter:

```text id="w3n7zb"
https://shop.com/products
```

The journey looks like this:

```text id="a8k5qx"
User
   │
   ▼
Browser
   │
   ▼
DNS
   │
   ▼
TCP
   │
   ▼
TLS
   │
   ▼
HTTP Request
   │
   ▼
Internet
   │
   ▼
Nginx
   │
   ▼
Uvicorn
   │
   ▼
FastAPI
   │
   ▼
Business Logic
   │
   ▼
PostgreSQL
   │
   ▼
Business Logic
   │
   ▼
JSON Response
   │
   ▼
Browser
   │
   ▼
Render Page
   │
   ▼
User
```

Although this appears to involve many steps, modern systems usually complete this entire process in just a few milliseconds.

---

# Why We Aren't Studying Each Step Deeply Yet

At this stage, your goal is to understand **the complete picture**.

In the upcoming modules, we'll explore each stage individually, including:

* DNS
* IP Addressing
* TCP
* TLS
* HTTP
* Web Servers
* ASGI
* Uvicorn
* FastAPI Internals
* Databases
* ORMs
* Deployment

By the end of the roadmap, every box in the diagram above will make complete sense.

---

## Request Journey at a Glance

| Step | What Happens                                      |
| ---- | ------------------------------------------------- |
| 1    | User performs an action                           |
| 2    | Browser creates an HTTP request                   |
| 3    | DNS resolves the domain name                      |
| 4    | TCP establishes a reliable connection             |
| 5    | TLS secures the communication (HTTPS)             |
| 6    | The HTTP request travels through the Internet     |
| 7    | The Web Server receives the request               |
| 8    | The Application Server forwards it to the backend |
| 9    | The Backend executes business logic               |
| 10   | The Backend communicates with the database        |
| 11   | The Backend creates an HTTP response              |
| 12   | The Response travels back to the client           |
| 13   | The Browser renders the result                    |
| 14   | The User sees the final output                    |

---

## Summary

A web request travels through many layers before the user sees the final result.

The browser creates the request, DNS resolves the destination, TCP establishes a connection, TLS secures communication, and the request travels through the Internet to the web server and application server.

The backend processes the request, interacts with the database if necessary, creates a response, and sends it back to the browser, which finally renders the result for the user.

Although we've only looked at these steps from a bird's-eye view, this complete journey forms the foundation for everything you'll learn in the remaining modules.

---

## Key Takeaways

* A single user action triggers a complete request lifecycle.
* The backend is only one stage in a much larger communication process.
* DNS, TCP, TLS, HTTP, Web Servers, Application Servers, and Databases all work together to process a request.
* The browser is responsible for creating requests and rendering responses.
* The backend is responsible for business logic and generating responses.
* Understanding the complete request journey provides the context needed for learning each networking technology in depth.

---


