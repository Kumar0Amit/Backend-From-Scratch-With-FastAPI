# 3.3 What Backend Does NOT Do

After learning the responsibilities of the backend, it's equally important to understand **what the backend is *not* responsible for**.

Many beginners assume that once a request leaves the browser, **the backend controls everything**.

That's not true.

Several important tasks happen **before the request reaches your backend** and **after the response leaves it**.

Understanding these boundaries will help you debug applications more effectively and understand where different technologies fit in the complete request lifecycle.

---

## The Complete Journey

When you visit:

```text id="f4r7qm"
https://example.com
```

the request follows a journey similar to this:

```text id="k7n3vp"
User

↓

Browser

↓

DNS

↓

TCP Connection

↓

TLS Handshake

↓

Internet Routing

↓

Web Server

↓

Application Server

↓

Backend

↓

Database

↓

Backend

↓

Browser

↓

User
```

Notice that the backend is only **one stage** in the complete journey.

---

# DNS Resolution

When you enter:

```text id="v8j2kt"
google.com
```

your computer does **not** automatically know where Google's servers are.

It first asks the **Domain Name System (DNS)**:

```text id="a6p9md"
google.com

↓

DNS

↓

142.xxx.xxx.xxx
```

Only after obtaining the IP address can the request be sent to Google's servers.

### Is This the Backend's Job?

**No.**

DNS resolution happens **before** the request reaches your backend.

Your FastAPI application never performs DNS lookups for incoming browser requests.

---

## Who Handles DNS?

Typically:

* Browser
* Operating System
* DNS Resolver
* DNS Servers

work together to translate a domain name into an IP address.

---

# TCP Connection

After finding the server's IP address,

a reliable connection must be established.

This is done using **TCP (Transmission Control Protocol).**

```text id="r5k8zn"
Browser

↓

TCP Connection

↓

Server
```

This connection ensures that data can be exchanged reliably.

### Is This the Backend's Job?

Again,

**No.**

Your backend application does not manually establish TCP connections.

The operating system and networking stack handle this automatically.

Your backend receives the request **after** the connection has already been created.

---

## What Actually Handles TCP?

Usually:

* Operating System
* Network Stack
* Web Server
* Application Server

work together to manage TCP connections.

As a backend developer, you normally don't write TCP connection code yourself.

---

# TLS (HTTPS Encryption)

If you're using HTTPS,

communication must be encrypted before any application data is exchanged.

This happens through the **TLS Handshake**.

```text id="n4v7px"
Browser

↓

TLS Handshake

↓

Secure Connection

↓

Backend
```

Once the secure channel is established,

HTTP requests and responses travel through the encrypted connection.

---

## Is Encryption Done by Your FastAPI Code?

Usually,

**No.**

In production environments,

TLS is commonly handled by:

* Nginx
* Apache
* Cloud Load Balancers
* Reverse Proxies

Your FastAPI application usually receives requests **after they have already been decrypted**.

---

# Browser Rendering

Suppose your backend returns:

```html id="x3q6tb"
<h1>Hello World</h1>
```

Who displays this?

The browser.

The backend only sends data.

The browser is responsible for:

* Parsing HTML
* Applying CSS
* Executing JavaScript
* Drawing pixels on the screen

Example:

```text id="u8m2df"
Backend

↓

HTML

↓

Browser

↓

Display Webpage
```

---

## Is Rendering a Backend Responsibility?

No.

Rendering belongs entirely to the browser (or another client).

The backend has no control over how the browser chooses to display the content.

---

# ISP Routing

After leaving your computer,

the request travels through multiple networks.

Example:

```text id="p2w5nc"
Browser

↓

Home Router

↓

ISP

↓

Regional Network

↓

Internet Backbone

↓

Destination Server
```

Routers determine the best path for every packet.

---

## Is Routing Controlled by the Backend?

No.

Routing decisions are made by:

* Routers
* Internet Service Providers
* Internet backbone networks

Your backend has no control over the path your packets take across the Internet.

---

# What Happens Before the Backend?

Many important things happen before your application receives a request.

```text id="m7k3pq"
User

↓

Browser

↓

DNS Lookup

↓

TCP Connection

↓

TLS Handshake

↓

Internet Routing

↓

Web Server

↓

Application Server

↓

Backend
```

Your FastAPI code begins working only after all of these steps have already completed successfully.

---

# What Happens After the Backend?

After your backend generates a response,

more work still remains.

```text id="d9t6xr"
Backend

↓

Application Server

↓

Web Server

↓

Internet

↓

Browser

↓

Render HTML

↓

Display to User
```

Again,

the backend is only one part of the overall journey.

---

# Backend vs Other Components

| Responsibility               | Backend?   |
| ---------------------------- | ---------- |
| Business Logic               | Yes        |
| Authentication               | Yes        |
| Authorization                | Yes        |
| Validation                   | Yes        |
| Database Communication       | Yes        |
| API Responses                | Yes        |
| Error Handling               | Yes        |
| DNS Resolution               | No         |
| TCP Connection Establishment | No         |
| TLS Handshake                | Usually No |
| Browser Rendering            | No         |
| Internet Routing             | No         |

---

# Why This Separation Matters

Imagine a website doesn't open.

Should you immediately assume your FastAPI code is broken?

Not necessarily.

The problem could be:

* DNS failure
* Internet outage
* Router issue
* Expired TLS certificate
* Reverse proxy misconfiguration
* Firewall rules
* Web server configuration

The backend might never even receive the request.

Understanding where each responsibility belongs helps you troubleshoot problems much more efficiently.

---

# Common Examples

### Problem

```text id="v6n3qb"
"This website can't be reached."
```

Possible cause:

* DNS failure
* Internet connection problem

Usually **not** the backend.

---

### Problem

```text id="t8k5yr"
"SSL Certificate Expired"
```

Possible cause:

* TLS configuration
* Web server
* Reverse proxy

Usually **not** the backend.

---

### Problem

```text id="g3m9vx"
"500 Internal Server Error"
```

Possible cause:

* Bug in backend code
* Database issue
* Unhandled exception

This **is** generally a backend problem.

---

### Problem

```text id="x2w7pf"
"Website looks broken."
```

Possible cause:

* HTML
* CSS
* JavaScript
* Browser rendering

Usually a frontend issue.

---

# Complete Request Journey

Putting everything together:

```text id="q5r8zn"
User
   │
   ▼
Browser
   │
DNS Lookup
   │
TCP Connection
   │
TLS Handshake
   │
Internet Routing
   │
Web Server
   │
Application Server
   │
Backend
   │
Business Logic
   │
Database
   │
Response
   │
Browser Rendering
   │
User
```

This diagram clearly shows where the backend fits and where its responsibilities begin and end.

---

## Summary

The backend plays a critical role in modern web applications, but it is **not responsible for everything** that happens during a request.

DNS resolution, TCP connection establishment, TLS encryption, browser rendering, and Internet routing are handled by other components of the networking stack.

Understanding these boundaries makes it easier to learn networking concepts, deploy applications, and diagnose problems when something goes wrong.

---

## Key Takeaways

* The backend is only one part of the complete request lifecycle.
* DNS resolution happens before the request reaches the backend.
* TCP connections are established by the networking stack, not backend code.
* TLS encryption is usually handled by web servers or reverse proxies.
* Browsers are responsible for rendering HTML, CSS, and JavaScript.
* Routers and ISPs determine how packets travel across the Internet.
* Knowing where backend responsibilities begin and end makes debugging much easier.

---

# Module Summary

In this module, we explored the role of the backend within a modern web application.

We began by understanding where the backend fits in relation to the frontend, database, infrastructure, browsers, web servers, and application servers.

Next, we studied the backend's primary responsibilities, including business logic, authentication, authorization, validation, database communication, API responses, and error handling.

Finally, we clarified what the backend does **not** do. Many networking tasks—such as DNS resolution, TCP connection establishment, TLS encryption, browser rendering, and Internet routing—are handled by other components outside the backend application.

Understanding these responsibilities and boundaries provides a clear picture of the backend's role before moving on to the complete request journey in the next module.

---

# Key Takeaways

* The backend acts as the application's decision-making layer.
* It sits between clients and databases, enforcing business rules.
* Backend responsibilities include authentication, authorization, validation, business logic, database communication, API responses, and error handling.
* The backend does not perform DNS lookups, establish TCP connections, render webpages, or control Internet routing.
* Modern web applications rely on many components working together, with each component focusing on a specific responsibility.

---


