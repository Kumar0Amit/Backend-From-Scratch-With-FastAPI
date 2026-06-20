# Module 6 – Development Environment

---

# 6.1 Development Environment

Before deploying applications to the Internet, developers build, test, and debug them on **their own computers**.

This setup is called the **development environment**.

As a backend developer, you'll spend most of your time working in a local development environment before deploying your applications to production.

In this module, we'll understand what a development environment is, what **localhost** and **127.0.0.1** mean, what a **port** is, and why local development is an essential part of software development.

> **Note:** This is a high-level overview. We'll study networking, sockets, ports, and deployment in much greater detail later.

---

## What is a Development Environment?

**Definition**

> A development environment is the complete setup used by a developer to build, run, test, and debug software before it is deployed.

A typical development environment includes:

* Source code
* Programming language (Python)
* Framework (FastAPI)
* Database
* Code editor (VS Code)
* Terminal
* Browser
* Version control (Git)

Example:

```text id="r7m3kx"
Your Computer
│
├── VS Code
├── Python
├── FastAPI
├── PostgreSQL
├── Browser
└── Git
```

Everything runs on your own machine.

---

## Why Don't We Develop Directly on Production?

Imagine writing new code directly on a live shopping website.

Every mistake would immediately affect real users.

```text id="p4w8tn"
Developer

↓

Writes Bug

↓

Production Website

↓

Users Experience Errors
```

Instead, developers first test everything locally.

```text id="v9k5qc"
Write Code

↓

Run Locally

↓

Test

↓

Fix Bugs

↓

Deploy to Production
```

This approach is safer and allows developers to experiment freely.

---

## Local Development

**Local Development** means running your application on **your own computer** instead of a remote server.

Example:

```text id="m2q7zr"
Your Computer

↓

FastAPI Server

↓

Browser

↓

Test
```

For most backend development tasks, no Internet connection is required because the client and server are running on the same machine.

---

## Typical Development Workflow

A backend developer's workflow usually looks like this:

```text id="g5r9xp"
Write Code

↓

Run Server

↓

Open Browser

↓

Test API

↓

Fix Bugs

↓

Repeat
```

This cycle happens repeatedly throughout development.

---

# What is localhost?

One of the first addresses you'll encounter in backend development is:

```text id="n8v3kd"
http://localhost:8000
```

But what exactly is **localhost**?

---

## Definition

> **localhost** is a special hostname that always refers to **the computer you are currently using**.

It does **not** point to another machine on the Internet.

It always points back to your own computer.

---

## Simple Analogy

Imagine your home address.

Instead of writing the full address every time, you simply say:

> "My house."

Similarly,

instead of specifying your computer's network address, you use:

```text id="k3p7mz"
localhost
```

It always means:

> **This computer.**

---

## Example

Suppose you start a FastAPI application.

```bash id="b6t2wr"
uvicorn main:app --reload
```

Then you open:

```text id="c4m8qx"
http://localhost:8000
```

The communication looks like:

```text id="f7w3pd"
Browser

↓

localhost

↓

Your Computer

↓

FastAPI Server
```

The request never leaves your machine.

---

# What is 127.0.0.1?

You may also see addresses like:

```text id="j8q5vn"
http://127.0.0.1:8000
```

This behaves almost exactly like:

```text id="y5k9tr"
http://localhost:8000
```

Why?

Because:

> **127.0.0.1 is the IP address that refers to your own computer.**

It is called the **loopback address**.

---

## localhost vs 127.0.0.1

```text id="m4r8xp"
localhost

↓

127.0.0.1

↓

Your Computer
```

In most situations:

```text id="x6t3pk"
localhost

=

127.0.0.1
```

The main difference is:

| localhost                     | 127.0.0.1       |
| ----------------------------- | --------------- |
| Hostname                      | IP Address      |
| Human-friendly                | Numeric address |
| Usually resolves to 127.0.0.1 | Loopback IP     |

We'll study how this mapping works when we learn DNS and networking in detail.

---

# Loopback Concept

Normally, requests travel across networks.

```text id="h2v9md"
Laptop

↓

Internet

↓

Server
```

With localhost:

```text id="q7k4pw"
Laptop

↓

Laptop
```

The request "loops back" to the same machine.

That's why **127.0.0.1** is known as the **loopback address**.

---

# What is a Port?

Suppose your computer is a large apartment building.

The building has one address,

but many apartments inside it.

```text id="t5m8qx"
Building

├── Apartment 101
├── Apartment 102
├── Apartment 103
└── Apartment 104
```

The building's address gets you to the correct building.

The apartment number tells you **which resident** you want.

A **port** works in a very similar way.

---

## Definition

> A port is a logical communication endpoint that identifies a specific application or service running on a computer.

Your computer can run many applications simultaneously.

Examples:

* FastAPI
* PostgreSQL
* Redis
* React Development Server

Each listens on a different port.

---

## Example

```text id="r3n7kv"
Computer

├── Port 8000 → FastAPI
├── Port 5432 → PostgreSQL
├── Port 6379 → Redis
└── Port 3000 → React
```

When you visit:

```text id="v8q2tn"
http://localhost:8000
```

you're saying:

> "Connect to the application listening on **port 8000** of my computer."

---

## Address + Port

A network location usually consists of:

```text id="k5m4pr"
Address

+

Port
```

Example:

```text id="b2t8xq"
localhost:8000
```

* **localhost** → Which computer?
* **8000** → Which application on that computer?

---

## Example Flow

You open:

```text id="y7p3md"
http://localhost:8000/users
```

The browser interprets it as:

```text id="c6r9tw"
Computer

↓

localhost

↓

Application

↓

Port 8000

↓

Endpoint

↓

/users
```

---

# Why We Use localhost

Local development offers several important advantages.

---

## Safe Testing

You can freely experiment without affecting real users.

```text id="n4w7pk"
Developer

↓

localhost

↓

Experiment Safely
```

---

## Faster Development

Since the client and server are running on the same computer,

communication is extremely fast.

No Internet routing is required.

---

## No Hosting Required

You don't need to purchase a cloud server just to learn backend development.

Everything runs locally.

---

## Easier Debugging

When something goes wrong, you can easily inspect:

* Logs
* Error messages
* Database
* Source code

Everything is available on your own computer.

---

## Offline Development

Many backend development tasks can be performed without an Internet connection because all communication stays on your machine.

---

# Typical Local Development Flow

```text id="j5k8vn"
Write Python Code

↓

Run FastAPI

↓

http://localhost:8000

↓

Browser Sends Request

↓

FastAPI Processes Request

↓

Browser Displays Response

↓

Modify Code

↓

Repeat
```

This rapid feedback loop is one of the biggest advantages of local development.

---

# Example with FastAPI

Suppose you write:

```python id="q8m2rt"
@app.get("/")
def home():
    return {"message": "Hello World"}
```

You start the server:

```bash id="g4p9wx"
uvicorn main:app --reload
```

The terminal displays:

```text id="x2v6kp"
Running on:

http://127.0.0.1:8000
```

or

```text id="w6t3mq"
http://localhost:8000
```

You open the address in your browser.

The browser sends the request to **your own computer**, and FastAPI returns:

```json id="t9r5pv"
{
    "message": "Hello World"
}
```

No external server is involved.

---

# Development vs Production

| Development                 | Production                             |
| --------------------------- | -------------------------------------- |
| Runs on your computer       | Runs on public servers                 |
| Uses localhost or 127.0.0.1 | Uses a public domain or IP address     |
| Safe for experimentation    | Used by real users                     |
| Frequent code changes       | Stable, tested code                    |
| Focused on debugging        | Focused on reliability and scalability |

---

# Putting It All Together

When you visit:

```text id="m3q7kn"
http://localhost:8000/users
```

the browser interprets it as:

```text id="d8v4px"
Protocol

↓

HTTP

↓

Host

↓

localhost

↓

IP

↓

127.0.0.1

↓

Port

↓

8000

↓

Endpoint

↓

/users
```

This tells the browser:

* Which computer to contact.
* Which application should receive the request.
* Which resource is being requested.

---

## Summary

A development environment allows developers to safely build, test, and debug applications on their own computers before deployment.

Using **localhost** and **127.0.0.1**, developers can run both the client and server on the same machine.

Ports allow multiple applications to run simultaneously without interfering with one another.

Understanding local development is essential because almost every backend application begins its life running on localhost before eventually being deployed to production.

---

## Key Takeaways

* A development environment is the local setup used to build and test applications.
* Local development allows developers to experiment safely before deployment.
* **localhost** is a hostname that always refers to the current computer.
* **127.0.0.1** is the loopback IP address and usually represents localhost.
* A port identifies a specific application or service running on a computer.
* Localhost and ports allow browsers to communicate with locally running backend applications.
* Most backend development begins locally before applications are deployed to production.

---
