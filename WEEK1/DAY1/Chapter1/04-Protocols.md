# 1.4 Protocols

In the previous section, we learned that computers communicate by exchanging messages.

But one important question remains:

> **How do completely different computers understand each other?**

A Windows laptop can communicate with a Linux server.

An Android phone can communicate with an iPhone.

A Python backend can communicate with a Java backend.

How is this possible?

The answer is **Protocols**.

---

## What is a Protocol?

A **protocol** is a set of rules that defines **how computers communicate with each other over a network**.

Think of a protocol as an agreed language and procedure.

It specifies things such as:

* How communication begins
* How data should be formatted
* How it is transmitted
* How errors are handled
* How communication ends

Without protocols, computers would exchange meaningless data that other devices could not understand.

### Definition

> A protocol is a standardized set of rules that allows different devices and software systems to communicate reliably over a network.

---

## Why Do Protocols Exist?

Imagine three companies manufacturing computers.

Company A decides to communicate like this:

```text
HELLO SERVER
```

Company B expects:

```text
CONNECT NOW
```

Company C expects:

```text
BEGIN DATA
```

Each company follows different rules.

As a result, none of their computers can communicate with one another.

Protocols solve this problem by providing **one common communication standard** that everyone follows.

---

## Problems Without Protocols

Without protocols:

* Devices could not understand each other.
* Websites would not load.
* Emails could not be delivered.
* Mobile apps could not communicate with backend servers.
* Online games would not synchronize players.

The modern Internet simply would not exist.

---

## Real-World Analogy

Imagine playing cricket.

Before the match begins, everyone already knows the rules.

* How many players participate
* How runs are scored
* What counts as an out
* When the match ends

Without agreed rules, everyone would play differently and the game would become impossible.

Protocols work in exactly the same way.

Every computer agrees to follow the same communication rules.

---

## Postal Service Analogy

Suppose you want to send a parcel.

You must include:

* Sender's address
* Receiver's address
* Correct packaging
* Delivery method

If you simply throw a box onto the road, nobody knows where it should go.

Similarly, computer messages require proper formatting and addressing before they can be delivered.

---

## What Do Protocols Define?

Protocols answer many important questions.

* How should communication begin?
* How should data be structured?
* How does the receiver identify the sender?
* How are errors detected?
* What happens if some data is lost?
* How should communication end?

Every network protocol defines answers to these questions.

---

## Protocol Stack (High-Level)

One protocol alone is not enough.

Different protocols solve different problems.

Think about sending a parcel.

You need:

* A letter
* An envelope
* An address
* A courier company
* Roads

Each part has a separate responsibility.

Networking works the same way.

Different protocols work together in layers.

```text
Application Layer
        │
        ▼
Transport Layer
        │
        ▼
Internet Layer
        │
        ▼
Network Access Layer
```

Each layer depends on the one below it.

---

## Application Layer

The Application Layer is responsible for communication between applications.

Examples include:

* Websites
* APIs
* Emails
* File Transfer
* Domain Name Lookups

Common protocols:

* HTTP
* HTTPS
* DNS
* FTP
* SMTP

---

## Transport Layer

The Transport Layer manages communication between two devices.

Its responsibilities include:

* Reliable delivery
* Packet ordering
* Error detection
* Data flow

Common protocols:

* TCP
* UDP

---

## Internet Layer

The Internet Layer is responsible for:

* Addressing devices
* Routing packets across networks

The most important protocol here is:

* IP (Internet Protocol)

---

## Network Access Layer

This layer handles the actual transmission of data through physical or wireless media.

Examples include:

* Ethernet
* Wi-Fi
* Fiber Optic Networks

---

## How the Protocol Stack Works

Suppose you request a webpage.

```text
Browser

↓

HTTP

↓

TCP

↓

IP

↓

Wi-Fi

↓

Internet

↓

Server
```

When the server receives the request, the process happens in reverse.

```text
Wi-Fi

↓

IP

↓

TCP

↓

HTTP

↓

Application
```

Every protocol performs one specific job.

Together they make Internet communication possible.

---

# Common Internet Protocols

Now let's look at some of the most important protocols you'll encounter as a backend developer.

---

## HTTP

**HTTP** stands for:

> **HyperText Transfer Protocol**

Purpose:

Transfers web pages and API requests between clients and servers.

Example:

```http
GET /users
```

Possible response:

```json
[
    {
        "id": 1,
        "name": "John"
    }
]
```

HTTP is the foundation of:

* Websites
* REST APIs
* Web applications

---

## HTTPS

HTTPS stands for:

> **HyperText Transfer Protocol Secure**

HTTPS is simply **HTTP with encryption**.

Instead of sending plain text over the Internet, all communication is encrypted.

Without HTTPS:

```text
Password

↓

Internet

↓

Anyone intercepting the traffic may read it.
```

With HTTPS:

```text
Encrypted Password

↓

Internet

↓

Unreadable without the encryption keys.
```

Today, almost every modern website uses HTTPS.

---

## TCP

TCP stands for:

> **Transmission Control Protocol**

Purpose:

Provides **reliable communication**.

TCP guarantees:

* Packets arrive.
* Packets arrive in order.
* Lost packets are retransmitted.
* Duplicate packets are handled correctly.

Example:

Downloading a PDF.

If page 5 is missing, the document becomes unusable.

TCP ensures the complete file arrives correctly.

Most web applications and APIs rely on TCP.

---

## UDP

UDP stands for:

> **User Datagram Protocol**

Purpose:

Provides **fast communication** without guaranteeing delivery.

Unlike TCP:

* No retransmissions
* No packet ordering
* Lower overhead
* Lower latency

Example:

Voice calls.

If one audio packet is lost, it's usually better to continue the conversation than to pause and resend the missing data.

Common uses include:

* Online gaming
* Video conferencing
* Live streaming
* Voice over IP (VoIP)

---

## TCP vs UDP

| Feature           | TCP                            | UDP                            |
| ----------------- | ------------------------------ | ------------------------------ |
| Reliable Delivery | Yes                            | No                             |
| Packet Ordering   | Yes                            | No                             |
| Error Recovery    | Yes                            | No                             |
| Speed             | Slightly Slower                | Faster                         |
| Common Usage      | Websites, APIs, File Downloads | Gaming, Streaming, Voice Calls |

---

## DNS

DNS stands for:

> **Domain Name System**

Humans prefer names like:

```text
google.com
```

Computers communicate using IP addresses.

DNS translates domain names into IP addresses.

```text
google.com

↓

DNS

↓

142.xxx.xxx.xxx

↓

Browser connects
```

Without DNS, users would need to remember numerical IP addresses for every website.

---

## FTP

FTP stands for:

> **File Transfer Protocol**

Purpose:

Transfers files between computers.

Example:

```text
Developer

↓

Upload Website Files

↓

Server
```

Traditionally, FTP was widely used to deploy websites.

Today, **SFTP (Secure File Transfer Protocol)** is more common because it encrypts transferred data.

---

## SMTP

SMTP stands for:

> **Simple Mail Transfer Protocol**

Purpose:

Sends emails between mail servers.

Example:

```text
You

↓

SMTP Server

↓

Recipient's Mail Server

↓

Recipient
```

Whenever your backend sends:

* Account verification emails
* Password reset links
* Welcome emails
* OTPs

SMTP is typically involved.

---

## How Multiple Protocols Work Together

Suppose you visit:

```text
https://www.example.com
```

Several protocols cooperate.

```text
Browser

↓

DNS
(Find Server Address)

↓

TCP
(Create Reliable Connection)

↓

HTTPS
(Encrypt Communication)

↓

HTTP
(Send Request)

↓

Server

↓

HTTP Response

↓

Browser
```

Each protocol has one specific responsibility.

Together they provide secure and reliable communication.

---

---

# Module Summary

In this module, we explored the foundations of the Internet and how modern computer networks communicate.

We began by understanding the **history of the Internet**, starting with **ARPANET**, the first large-scale packet-switched computer network. We learned why it was created, how it evolved into today's Internet, and why **packet switching** became the preferred communication method over **circuit switching**.

Next, we studied **what the Internet actually is**. Rather than being one enormous network, it is a **network of networks** where millions of independent networks communicate using common protocols. We also learned about distributed communication, the physical infrastructure that supports the Internet, and the difference between the **Internet**, a **Local Area Network (LAN)**, and the **World Wide Web (WWW)**.

We then looked at **how computers communicate**. Just like humans exchange messages using language, computers exchange structured data across networks. We learned about messages, data transmission, packet-based communication, the need for communication rules, and why standardization allows billions of different devices to work together.

Finally, we studied **protocols**, the standardized rules that govern communication between computers. We introduced the idea of a **protocol stack** and learned the purpose of several important Internet protocols including:

* HTTP
* HTTPS
* TCP
* UDP
* DNS
* FTP
* SMTP

Although we only covered these protocols at a high level, they form the foundation for almost everything that follows in backend development.

---

# Key Takeaways

* The Internet evolved from **ARPANET**, a research network designed to improve communication and reliability.
* **Packet Switching** divides data into packets that can travel independently through different routes, making the Internet efficient and fault tolerant.
* The Internet is a **global network of interconnected networks**, not one giant centralized network.
* Communication across the Internet is **distributed**, meaning there is no single computer controlling everything.
* The Internet is supported by physical infrastructure such as:

  * Fiber optic cables
  * Undersea cables
  * Routers
  * Data centers
  * Internet Service Providers (ISPs)
* A **Local Area Network (LAN)** connects devices within a limited area, while the Internet connects countless LANs around the world.
* The **Internet** and the **World Wide Web** are different. The Web is one service that operates on top of the Internet.
* Computers communicate by exchanging **structured messages** across networks.
* The movement of data between devices is called **data transmission**, and data is typically divided into **packets** before being sent.
* Computers rely on **protocols**, which are standardized rules that define how communication should occur.
* Standardization enables devices running different operating systems, hardware, and programming languages to communicate successfully.
* Internet communication relies on multiple protocols working together, each with a specific responsibility.
* Some of the most important protocols introduced in this module are:

  * **HTTP** – Transfers web pages and API requests.
  * **HTTPS** – Secure version of HTTP using encryption.
  * **TCP** – Reliable, ordered communication.
  * **UDP** – Fast communication with minimal overhead.
  * **DNS** – Converts domain names into IP addresses.
  * **FTP** – Transfers files between computers.
  * **SMTP** – Sends emails between mail servers.

---

# Module Flow Recap

```text
History of the Internet
        │
        ▼
What is the Internet?
        │
        ▼
How Computers Communicate
        │
        ▼
Need for Protocols
        │
        ▼
Internet Protocols
        │
        ▼
Foundation for Client–Server Communication
```

Everything covered in this module builds the foundation for the next stage of your backend journey.

In the next module, we'll move from understanding **the Internet itself** to understanding **how applications communicate over it**.

We'll answer questions such as:

* What is a client?
* What is a server?
* How do they communicate?
* What is a request?
* What is a response?
* What does stateless communication mean?

These concepts form the basis of every web application and every backend framework you'll use, including FastAPI.

---


