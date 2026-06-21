# 2.2 DNS Architecture

## Introduction

In the previous chapter, we learned that DNS translates a domain name like:

```text
google.com
```

into an IP address like:

```text
142.250.xxx.xxx
```

But an important question remains:

> **Who actually performs this translation?**

Is there one giant DNS server for the whole Internet?

**No.**

DNS is a **distributed hierarchical system** made up of different types of servers, each responsible for a specific part of the lookup process.

When you visit a website, several components work together to find the correct IP address.

The main components are:

* Client
* Resolver
* Recursive Resolver
* Root Name Server
* TLD Name Server
* Authoritative Name Server

Let's understand each one.

---

# High-Level DNS Architecture

```text
              You
               │
               ▼
           Web Browser
               │
               ▼
      OS DNS Resolver
               │
               ▼
     Recursive Resolver
               │
        ┌──────┴──────┐
        ▼             ▼
 Root Name Server  (Finds TLD)
        │
        ▼
  TLD Name Server
        │
        ▼
Authoritative Name Server
        │
        ▼
   IP Address Returned
        │
        ▼
Browser connects to server
```

Notice that **each server has a different responsibility**.

---

# 1. Client

The **Client** is the device or application requesting the IP address.

Examples include:

* Web Browser
* Mobile App
* Laptop
* Smartphone
* API Client

Suppose you type:

```text
google.com
```

into Chrome.

The browser becomes the **DNS client** because it needs the IP address before it can connect.

The client does **not** know the IP address.

It only knows the domain name.

---

## Client Responsibilities

The client:

* Knows the domain name.
* Needs the IP address.
* Starts the DNS lookup process.
* Waits for the final answer.

Think of the client as the person asking:

> "Where is Google?"

---

# 2. Resolver

The **Resolver** is usually part of your operating system.

It acts as the **first DNS component** that receives the browser's request.

For example:

```text
Chrome

↓

Windows DNS Resolver
```

or

```text
Firefox

↓

Linux Resolver
```

The resolver first checks:

* Browser cache
* Operating system DNS cache
* Local hosts file

If the answer is found, the lookup stops immediately.

Otherwise, it forwards the request to a **Recursive Resolver**.

---

## Resolver Responsibilities

* Accept requests from applications.
* Check local caches.
* Check the hosts file.
* Forward unresolved queries.

Think of it as the receptionist in an office.

Before asking anyone else, the receptionist checks whether the answer is already available locally.

---

# 3. Recursive Resolver

The **Recursive Resolver** performs the actual search for the IP address.

It is often operated by:

* Your Internet Service Provider (ISP)
* Google Public DNS
* Cloudflare DNS
* Quad9

Unlike the local resolver, the recursive resolver communicates with DNS servers across the Internet.

Its goal is simple:

> "Don't return until you have the final IP address."

That's why it's called **recursive**.

---

## Responsibilities

The recursive resolver:

* Receives queries from clients.
* Checks its own DNS cache.
* Contacts Root Name Servers.
* Contacts TLD Name Servers.
* Contacts Authoritative Name Servers.
* Returns the final IP address.

The recursive resolver does all the hard work.

The browser simply waits for the answer.

---

## Real-World Analogy

Imagine asking a librarian:

> "Can you find this book?"

The librarian doesn't simply point somewhere.

Instead, they:

* Check nearby shelves.
* Ask another librarian.
* Visit storage.
* Return with the book.

The recursive resolver behaves the same way.

---

# 4. Root Name Server

The **Root Name Server** sits at the top of the DNS hierarchy.

It does **not** know the IP address of every website.

Instead, it knows:

> **Which TLD Name Server should handle the request?**

Suppose someone asks for:

```text
google.com
```

The recursive resolver asks:

```text
Where can I find .com domains?
```

The Root Server replies:

```text
Ask the .com TLD server.
```

That's all.

It simply points to the next step.

---

## Root Server Responsibilities

* Knows all Top-Level Domains.
* Directs queries to the correct TLD server.
* Does not store website IP addresses.

Think of it as the information desk in a shopping mall.

It doesn't know where every product is.

It only knows which floor or department to visit.

---

# 5. TLD Name Server

The **Top-Level Domain (TLD) Name Server** manages domains under a specific extension.

Examples:

```text
.com
.org
.net
.in
.edu
```

Suppose the query is:

```text
google.com
```

The recursive resolver reaches the `.com` TLD server and asks:

> "Where is google.com?"

The TLD server replies:

> "Ask Google's Authoritative Name Server."

Again, it doesn't return the IP address.

It only tells the resolver where to ask next.

---

## Responsibilities

* Manages one specific TLD.
* Knows which Authoritative Server is responsible for each domain.
* Does not usually store website IP addresses.

Think of it as a city's directory office.

It knows which building contains the information you need.

---

# 6. Authoritative Name Server

The **Authoritative Name Server** is the final source of truth.

It stores the actual DNS records for a domain.

For example:

```text
google.com
```

Its DNS records might contain:

```text
A Record

google.com

↓

142.250.xxx.xxx
```

When asked,

it returns the final IP address.

---

## Responsibilities

* Stores DNS records.
* Stores A, AAAA, MX, TXT, CNAME records.
* Returns the official IP address.
* Provides the final answer.

This is the only server that knows the actual IP address.

---

## Real-World Analogy

Suppose you're looking for a student's marks.

You ask:

School Reception

↓

Department Office

↓

Teacher

↓

Teacher opens the official gradebook.

The gradebook is the **authoritative source**.

Similarly,

the Authoritative Name Server is the official source for a domain's DNS records.

---

# Complete DNS Lookup Flow

Suppose you visit:

```text
github.com
```

The complete architecture works like this:

```text
Step 1

Browser

↓

OS Resolver

↓

Checks Local Cache

↓

Not Found

↓

Recursive Resolver

↓

Checks Its Cache

↓

Not Found

↓

Root Name Server

↓

"Ask .com"

↓

.com TLD Server

↓

"Ask GitHub's Authoritative Server"

↓

Authoritative Server

↓

140.82.xxx.xxx

↓

Recursive Resolver

↓

OS Resolver

↓

Browser

↓

TCP Connection Starts
```

---

# Real-World Analogy

Imagine searching for someone's address.

```text
You

↓

Receptionist
(Local Resolver)

↓

City Information Office
(Recursive Resolver)

↓

Country Directory
(Root Server)

↓

State Directory
(TLD Server)

↓

Local Municipality
(Authoritative Server)

↓

Exact House Address
```

Each office knows only the next place to ask until the exact address is found.

---

# Summary Table

| Component                 | Responsibility                                                   |
| ------------------------- | ---------------------------------------------------------------- |
| Client                    | Starts the DNS request by asking for a domain's IP address       |
| Resolver                  | Checks local cache and forwards unresolved queries               |
| Recursive Resolver        | Performs the complete DNS lookup on behalf of the client         |
| Root Name Server          | Directs queries to the appropriate Top-Level Domain (TLD) server |
| TLD Name Server           | Directs queries to the correct Authoritative Name Server         |
| Authoritative Name Server | Stores the official DNS records and returns the final IP address |

---

# Key Takeaways

* DNS is a **hierarchical distributed system**, not a single server.
* The **Client** initiates the request by asking for a domain's IP address.
* The **Resolver** first checks local caches before forwarding the query.
* The **Recursive Resolver** performs the complete lookup process and returns the final answer.
* The **Root Name Server** knows where each Top-Level Domain is managed.
* The **TLD Name Server** knows which Authoritative Name Server manages a specific domain.
* The **Authoritative Name Server** is the final and official source of a domain's DNS records.
* Once the IP address is returned, the browser can begin establishing a TCP connection to the destination server.
