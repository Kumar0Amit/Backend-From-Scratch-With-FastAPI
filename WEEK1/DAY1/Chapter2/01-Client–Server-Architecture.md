# Module 2 – Client–Server Architecture

---

# 2.1 What is a Client?

Every interaction on the Internet involves two main participants:

* Client
* Server

Understanding these two concepts is one of the foundations of backend development.

Whenever you use:

* Chrome
* Instagram
* WhatsApp
* Netflix
* A Python script
* Another backend service

something is acting as a **client**.

---

## What is a Client?

**Definition**

> A client is any device or software application that **initiates communication** by requesting a service or resource from another computer (called a server).

The important words here are:

* Initiates communication
* Requests data or services

The client asks.

The server responds.

---

## Basic Communication

```text id="2gkpwk"
Client
   │
   │ Request
   ▼
Server
   │
   │ Response
   ▼
Client
```

Example:

```text id="3fxlkm"
Chrome Browser

↓

Request Homepage

↓

Google Server

↓

HTML + CSS + JavaScript

↓

Browser Displays Webpage
```

The browser is the client.

Google's computer is the server.

---

## Real-World Analogy

Imagine visiting a restaurant.

```text id="hyn6e8"
Customer

↓

Orders Food

↓

Chef

↓

Prepares Food

↓

Customer Receives Food
```

* Customer → Client
* Chef → Server

The customer starts the conversation.

The chef waits until someone places an order.

Exactly the same happens on the Internet.

---

## Responsibilities of a Client

A client has several responsibilities.

---

### 1. Initiate Communication

The client starts the interaction.

Example:

```text id="1im8c0"
Open YouTube

↓

Browser Sends Request
```

Without the client,

nothing happens.

---

### 2. Send Requests

Clients tell servers what they want.

Example:

```http id="0tz4my"
GET /videos
```

or

```http id="bcbjca"
POST /login
```

These requests are created by the client.

---

### 3. Receive Responses

After processing,

the server replies.

Example:

```json id="kwfb18"
{
    "username": "John",
    "followers": 230
}
```

The client receives this information.

---

### 4. Display Information

Most clients present information to users.

Example:

Browser:

```text id="m4ixci"
Receives HTML

↓

Displays Webpage
```

Mobile App:

```text id="7dxmnf"
Receives JSON

↓

Displays User Profile
```

---

### 5. Accept User Input

Clients collect information from users.

Examples include:

* Username
* Password
* Search queries
* Button clicks
* Uploaded images

The client packages this information and sends it to the server.

---

### 6. Handle User Interaction

Clients manage everything the user directly interacts with.

Examples:

* Scrolling
* Clicking
* Typing
* Animations
* Menus
* Notifications

The server generally does not control these directly.

---

## What a Client Usually Does NOT Do

A client usually does **not**:

* Store the application's primary database
* Make business decisions
* Process payments
* Store sensitive business logic
* Decide user permissions
* Authenticate every request independently

These responsibilities typically belong to the backend server.

---

# Types of Clients

Many beginners think only web browsers are clients.

In reality,

anything that requests a service from another computer is a client.

Let's look at the most common examples.

---

## Browser

The browser is the most familiar client.

Examples:

* Google Chrome
* Microsoft Edge
* Mozilla Firefox
* Safari

Workflow:

```text id="6k4bck"
Browser

↓

GET https://google.com

↓

Google Server

↓

HTML

↓

Browser Renders Webpage
```

Browsers understand:

* HTML
* CSS
* JavaScript

and convert them into webpages users can interact with.

---

## Mobile App

Mobile applications are also clients.

Example:

Instagram.

```text id="j8hwx8"
Instagram App

↓

Request Feed

↓

Instagram Backend

↓

JSON Data

↓

Display Posts
```

Unlike browsers,

mobile apps usually receive **JSON** instead of HTML and build their own user interface.

---

## Desktop Application

Desktop software often communicates with remote servers.

Examples:

* Spotify
* Discord
* Slack
* VS Code Extensions

Workflow:

```text id="z5xmmg"
Desktop App

↓

API Request

↓

Backend Server

↓

JSON Response

↓

Update Interface
```

The desktop application acts as the client.

---

## Python Script

Even a simple Python program can be a client.

Example:

```python id="jlwm3q"
import requests

response = requests.get("https://api.example.com/users")
```

Your script sends a request.

The API returns a response.

In this situation, your Python script is the client.

This is common in:

* Automation
* Data analysis
* Machine learning pipelines
* Integration testing
* API testing

---

## Backend Service

Servers often communicate with other servers.

Suppose an Order Service needs to charge a customer's credit card.

```text id="2tpbpl"
Order Service

↓

Payment Service
```

At that moment:

* Order Service → Client
* Payment Service → Server

A backend application can act as both a client and a server depending on who it is communicating with.

---

### Microservices Example

```text id="jjlwm"
Frontend
    │
    ▼
User Service
    │
    ▼
Payment Service
    │
    ▼
Email Service
```

Each service calls another service.

Whenever one service sends a request to another, it acts as a client.

---

## IoT Device

An **Internet of Things (IoT)** device can also act as a client.

Examples:

* Smart watch
* Smart thermostat
* Smart bulb
* Smart camera
* Smart refrigerator

Example:

```text id="ukowv0"
Temperature Sensor

↓

Current Temperature

↓

Cloud Server

↓

Store Reading
```

The IoT device sends data to the cloud server, making it the client.

---

## Can One Device Be Both Client and Server?

Yes.

The role depends on the communication, not on the device.

Suppose your laptop is browsing Google.

```text id="2pcmv4"
Laptop

↓

Google Server
```

Your laptop is the client.

Now suppose your laptop is running a FastAPI application.

```text id="l3s2n4"
Phone

↓

Laptop (Running FastAPI)

↓

Response
```

Now your laptop is the server.

The same device can perform both roles at different times.

---

## Examples of Clients

| Client              | Server            |
| ------------------- | ----------------- |
| Chrome Browser      | Google Web Server |
| Instagram App       | Instagram Backend |
| Spotify Desktop App | Spotify Backend   |
| Python Script       | REST API          |
| Smart Watch         | Cloud Server      |
| Payment Service     | Banking API       |

---

## Client vs User

These two terms are often confused.

They are not the same.

### User

A human using an application.

### Client

The software or device that communicates with the server on behalf of the user.

Example:

```text id="t5j25u"
Human

↓

Chrome Browser (Client)

↓

Google Server
```

The user never communicates directly with the server.

The browser does it for them.

---

## Complete Communication Flow

```text id="r5pd22"
User
   │
   ▼
Client
(Browser / App / Script)
   │
   │ Request
   ▼
Internet
   │
   ▼
Server
   │
   │ Process Request
   ▼
Response
   │
   ▼
Client
   │
   ▼
User
```

The client acts as the bridge between the user (or another system) and the server.

---

## Summary

A client is any software application or device that starts communication by requesting a service from another computer.

Clients are responsible for collecting user input, sending requests, receiving responses, and presenting information to users.

While browsers are the most common example, mobile apps, desktop applications, backend services, Python scripts, and IoT devices can all act as clients.

The role of a client is determined by the interaction itself—a device can be a client in one situation and a server in another.

---

## Key Takeaways

* A client initiates communication by sending requests to a server.
* Clients collect user input, send requests, receive responses, and display results.
* Common clients include browsers, mobile apps, desktop applications, Python scripts, backend services, and IoT devices.
* A single application or device can act as both a client and a server depending on the communication.
* The client serves as the bridge between the user and the backend server.

---


