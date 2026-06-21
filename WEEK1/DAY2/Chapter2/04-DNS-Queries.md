# 2.3 Recursive Query, Iterative Query & DNS Resolution Steps

## Introduction

In the previous chapter, we learned about the different components of DNS:

* Client
* Resolver
* Recursive Resolver
* Root Name Server
* TLD Name Server
* Authoritative Name Server

Now let's understand **how these components communicate**.

There are two types of DNS queries:

1. **Recursive Query**
2. **Iterative Query**

Understanding these two query types is one of the most important concepts in DNS because they explain **who is responsible for finding the final IP address**.

---

# High-Level Overview

Suppose you type:

```text
google.com
```

The complete DNS lookup looks like this:

```text
Browser
    │
    ▼
OS Resolver
    │
    ▼
Recursive Resolver
    │
    ├───────────────┐
    ▼               ▼
Root Server     (Referral)
    │
    ▼
TLD Server
    │
    ▼
Authoritative Server
    │
    ▼
IP Address
```

Notice something important:

The **browser only talks to the Recursive Resolver**.

The Recursive Resolver talks to all the other DNS servers.

---

# 1. Recursive Query

## Definition

A **Recursive Query** is a DNS query where the client expects the server to return the **final answer**.

The client says:

> "I don't care how you find it. Just give me the IP address."

If the server cannot answer immediately, it must search other DNS servers until it finds the answer.

---

## Example

You type:

```text
google.com
```

The browser asks:

```text
Recursive Resolver

"What is the IP address of google.com?"
```

The browser expects only one of two responses:

```text
IP Address
```

or

```text
Domain Not Found
```

The browser does **not** want referrals.

---

## Characteristics

* Client expects the final answer.
* Recursive Resolver performs all the work.
* Simplifies the client's job.
* Most user devices perform recursive queries.

---

## Real-World Analogy

Imagine asking your assistant:

> "Find the CEO of Microsoft."

You don't want directions like:

> "Ask HR."

or

> "Go to Building A."

You simply expect:

```text
Satya Nadella
```

The assistant does all the searching.

That's a **Recursive Query**.

---

# Recursive Query Flow

```text
Browser
    │
    ▼
Recursive Resolver

"I need google.com's IP"

    │
    ▼
(Returns final IP)

142.250.xxx.xxx
```

The browser never communicates with Root, TLD, or Authoritative servers directly.

---

# 2. Iterative Query

## Definition

An **Iterative Query** is a DNS query where the server returns the **best information it currently has**, instead of the final answer.

In other words:

> "I don't know the answer, but I know who might."

Instead of performing the search itself, the server returns a **referral**.

---

## Example

The Recursive Resolver asks the Root Server:

```text
"What is the IP address of google.com?"
```

The Root Server replies:

```text
I don't know.

Ask the .com TLD Server.
```

The Recursive Resolver then asks the `.com` TLD Server.

The `.com` TLD Server replies:

```text
I don't know.

Ask Google's Authoritative Name Server.
```

Finally, the Recursive Resolver asks Google's Authoritative Server.

That server replies:

```text
142.250.xxx.xxx
```

---

## Characteristics

* Server returns the best information available.
* Usually returns referrals.
* The querying server continues searching.
* Used between DNS servers.

---

## Real-World Analogy

Suppose you're looking for a person in a large company.

You ask the receptionist.

The receptionist says:

```text
Go to the HR Department.
```

HR says:

```text
Go to the Engineering Department.
```

Engineering says:

```text
Room 302.
```

Finally:

```text
Room 302

↓

Person Found
```

Each person only tells you **where to go next**.

That is an **Iterative Query**.

---

# Recursive vs Iterative Query

| Feature                          | Recursive Query | Iterative Query |
| -------------------------------- | --------------- | --------------- |
| Client expects final answer?     | ✅ Yes           | ❌ No            |
| Server performs complete lookup? | ✅ Yes           | ❌ No            |
| Returns referrals?               | ❌ Usually No    | ✅ Yes           |
| Used by browsers?                | ✅ Yes           | ❌ No            |
| Used between DNS servers?        | ❌ No            | ✅ Yes           |

---

# Complete DNS Resolution Steps

Let's see the complete lookup for:

```text
github.com
```

---

## Step 1

The user types:

```text
github.com
```

into the browser.

---

## Step 2

The browser checks:

```text
Browser DNS Cache
```

Found?

```text
Yes

↓

Return IP

Stop.
```

Otherwise continue.

---

## Step 3

The browser asks the Operating System.

The OS checks:

```text
OS DNS Cache

↓

Hosts File
```

Found?

```text
Yes

↓

Return IP

Stop.
```

Otherwise continue.

---

## Step 4

The OS sends a **Recursive Query** to the Recursive Resolver.

```text
"What is github.com's IP address?"
```

---

## Step 5

The Recursive Resolver checks its own cache.

If found:

```text
Return IP

Stop.
```

Otherwise continue.

---

## Step 6

The Recursive Resolver asks the **Root Name Server**.

```text
github.com ?
```

Root replies:

```text
Ask the .com TLD Server.
```

This is an **Iterative Query**.

---

## Step 7

The Recursive Resolver asks the **.com TLD Server**.

```text
github.com ?
```

The `.com` server replies:

```text
Ask GitHub's Authoritative Server.
```

Again, this is an **Iterative Query**.

---

## Step 8

The Recursive Resolver asks GitHub's **Authoritative Name Server**.

```text
github.com ?
```

The Authoritative Server replies:

```text
140.82.xxx.xxx
```

---

## Step 9

The Recursive Resolver caches the result.

It may cache:

* Final IP address
* TLD referral
* Authoritative server referral

---

## Step 10

The Recursive Resolver sends the IP back to the Operating System.

The OS may also cache it.

---

## Step 11

The Operating System returns the IP to the browser.

The browser may cache it as well.

---

## Step 12

The browser creates a TCP connection using:

```text
140.82.xxx.xxx
```

and sends the HTTP request.

---

# Complete Flow Diagram

```text
User
 │
 ▼
Browser
 │
 ▼
Browser DNS Cache
 │
 ▼
OS Resolver
 │
 ▼
OS DNS Cache
 │
 ▼
Hosts File
 │
 ▼
Recursive Resolver
 │
 ▼
Recursive Resolver Cache
 │
 ▼
Root Name Server
 │
 ▼
.com TLD Server
 │
 ▼
Authoritative Name Server
 │
 ▼
140.82.xxx.xxx
 │
 ▼
Recursive Resolver
 │
 ▼
OS Resolver
 │
 ▼
Browser
 │
 ▼
TCP Connection
 │
 ▼
HTTP Request
```

---

# Which Queries Are Recursive and Which Are Iterative?

```text
Browser
   │
   │  Recursive Query
   ▼
Recursive Resolver
   │
   │  Iterative Query
   ▼
Root Server
   │
   │  Iterative Query
   ▼
TLD Server
   │
   │  Iterative Query
   ▼
Authoritative Server
```

Remember this simple rule:

* **Client → Recursive Resolver = Recursive Query**
* **Recursive Resolver → Root/TLD/Authoritative = Iterative Queries**

---

# Summary Table

| Query Type                | Description                                                                               |
| ------------------------- | ----------------------------------------------------------------------------------------- |
| Recursive Query           | Client asks a DNS server to return the final answer.                                      |
| Iterative Query           | DNS server returns the best information it has, usually a referral to another DNS server. |
| Recursive Resolver        | Performs the complete lookup on behalf of the client.                                     |
| Root Name Server          | Refers the resolver to the correct TLD server.                                            |
| TLD Name Server           | Refers the resolver to the correct Authoritative Name Server.                             |
| Authoritative Name Server | Returns the final DNS record (such as the IP address).                                    |

---

# Key Takeaways

* A **Recursive Query** means **"Find the final answer for me."**
* An **Iterative Query** means **"I don't know the final answer, but here's where to ask next."**
* Browsers and operating systems send **recursive queries** to recursive resolvers.
* Recursive resolvers send **iterative queries** to Root, TLD, and Authoritative Name Servers.
* Root and TLD servers usually return **referrals**, while Authoritative Name Servers return the **actual DNS record**.
* After receiving the IP address, the recursive resolver caches the result and returns it to the client, allowing the browser to establish a TCP connection.
