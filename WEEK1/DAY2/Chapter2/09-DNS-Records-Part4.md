# How Does DNS Know Which Record (A, MX, TXT, etc.) to Return?

## Introduction

After learning about DNS records, a common question arises:

> **When I type `google.com` into my browser, who decides whether to request an A record, AAAA record, MX record, TXT record, or some other DNS record?**

Many beginners assume that the **Recursive Resolver** decides which DNS record to fetch.

**This is not correct.**

The **application that needs the information** decides the DNS record type.

The Recursive Resolver simply forwards that request and retrieves the requested record.

---

# DNS Query Contains Two Things

Every DNS query contains two important pieces of information:

```text
1. Domain Name

2. Record Type
```

Example:

```text
Name = google.com

Type = A
```

or

```text
Name = google.com

Type = AAAA
```

or

```text
Name = microsoft.com

Type = MX
```

The Recursive Resolver never changes the record type.

---

# Overall Flow

```text
Application

↓

Creates DNS Query

(Name + Record Type)

↓

OS Resolver

↓

Recursive Resolver

↓

Root Server

↓

TLD Server

↓

Authoritative Server

↓

Requested Record Returned
```

Notice that the **record type travels all the way to the Authoritative Name Server**.

---

# Who Chooses the Record Type?

The answer is simple:

**The application chooses it.**

Different applications need different kinds of information.

---

## Example 1 — Browser Opening a Website

Suppose you type:

```text
https://google.com
```

The browser thinks:

> "I need an IP address so I can create a TCP connection."

Therefore it creates:

```text
Name = google.com

Type = A
```

or

```text
Name = google.com

Type = AAAA
```

or sometimes both.

The Recursive Resolver simply forwards the query.

---

## Example 2 — Sending an Email

Suppose Gmail wants to send mail to:

```text
john@microsoft.com
```

Gmail does **not** need Microsoft's website.

It needs Microsoft's **mail server**.

Therefore Gmail sends:

```text
Name = microsoft.com

Type = MX
```

The Authoritative Server returns Microsoft's mail server information.

---

## Example 3 — Google Workspace Domain Verification

Suppose Google wants to verify ownership of:

```text
example.com
```

Google knows verification tokens are stored in TXT records.

Therefore it sends:

```text
Name = example.com

Type = TXT
```

The Authoritative Server returns the TXT record.

---

# Common Applications and Their DNS Queries

| Application         | DNS Record Requested |
| ------------------- | -------------------- |
| Browser             | A / AAAA             |
| Email Server        | MX                   |
| Google Workspace    | TXT                  |
| Microsoft 365       | TXT                  |
| DNS Server          | NS                   |
| Reverse Lookup Tool | PTR                  |
| Active Directory    | SRV                  |

---

# Role of the Recursive Resolver

Think of the Recursive Resolver as a courier.

Suppose this is the DNS query:

```text
To:

google.com

Request:

A Record
```

The resolver simply delivers this request to Google's Authoritative Name Server.

It never changes:

```text
A

↓

MX
```

or

```text
TXT

↓

AAAA
```

It only retrieves exactly what was requested.

---

# Mental Model

Imagine ordering food.

You tell the waiter:

```text
Pizza
```

The waiter goes to the kitchen.

The waiter does **not** decide:

```text
I'll bring Pasta instead.
```

Similarly,

the Recursive Resolver never decides the DNS record type.

It simply delivers the application's request.

---

# Key Takeaways

* Every DNS query contains both a **Domain Name** and a **Record Type**.
* The **application** determines which record type is required.
* The **Recursive Resolver** simply retrieves that specific record.
* Browsers typically request **A** and/or **AAAA** records.
* Mail servers request **MX** records.
* Verification services request **TXT** records.
* The Authoritative Name Server returns only the requested record type.
