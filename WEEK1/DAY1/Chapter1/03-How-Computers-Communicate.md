# 1.3 How Computers Communicate

Now that we understand what the Internet is, the next question is:

> **How do computers actually communicate with each other?**

Every backend application you build depends on this communication. Whether it's loading a webpage, sending an email, calling an API, or querying a database, it all comes down to computers exchanging information.

---

## Communication Between Computers

Humans communicate by exchanging information through spoken or written language.

Example:

```text
Person A: Hello!

↓

Person B: Hi!
```

Computers communicate in a very similar way.

Instead of speaking English or another human language, they exchange **data**.

Example:

```text
Your Laptop

↓

"Give me Google's homepage."

↓

Google Server

↓

"Here is the homepage."
```

Communication simply means:

> **One computer sends information, and another computer receives it.**

---

## Real-World Example

Suppose you open YouTube.

You type:

```text
https://youtube.com
```

or click the YouTube icon.

What actually happens?

Your browser creates a request.

```text
Laptop

↓

Request

↓

YouTube Server
```

The server processes the request and replies.

```text
YouTube Server

↓

Response

↓

Laptop
```

Finally, your browser displays the webpage.

Every website follows this same communication pattern.

---

## Messages

Communication happens through **messages**.

A message is simply:

> **A piece of information sent from one computer to another.**

Humans send messages like:

```text
How are you?
```

Computers send structured messages.

Example:

```http
GET /index.html
```

or

```json
{
    "username": "john",
    "password": "123"
}
```

Although the format is different, both are simply messages carrying information.

---

## Everyday Examples of Messages

Whenever you use the Internet, thousands of messages are exchanged.

### Logging In

```text
Username
Password

↓

Server

↓

Login Successful
```

---

### Watching a Video

```text
Browser

↓

Send me Video XYZ

↓

Server

↓

Video Data
```

---

### Searching on Google

```text
Browser

↓

Search = FastAPI

↓

Google

↓

Search Results
```

Every user action eventually becomes one or more messages exchanged between computers.

---

## Data Transmission

Once a message is created, it needs to travel to another computer.

The movement of data from one device to another is called:

> **Data Transmission**

Think of sending a parcel.

```text
You

↓

Courier

↓

Road

↓

Friend
```

Similarly, computer data travels through:

* Wi-Fi
* Ethernet cables
* Fiber optic cables
* Routers
* ISPs
* Undersea cables
* Mobile networks

Example:

```text
Laptop

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

This entire journey is known as data transmission.

---

## Data is Sent in Packets

Earlier, we learned about packet switching.

Suppose you want to send:

```text
Hello World
```

Instead of sending it as one large block, it is divided into smaller pieces.

```text
Packet 1

Packet 2

Packet 3
```

Each packet may travel through different routes before reaching the destination.

Once all packets arrive, they are reassembled into the original message.

---

## Sender and Receiver

Every communication has two sides.

```text
Sender

↓

Network

↓

Receiver
```

For example:

When you open Instagram:

```text
Your Phone

↓

Instagram Server
```

Your phone is the sender.

The Instagram server is the receiver.

When Instagram sends the feed back:

```text
Instagram Server

↓

Your Phone
```

Now the server becomes the sender, and your phone becomes the receiver.

Communication is usually **two-way**.

---

## But How Do Computers Understand Each Other?

Imagine this conversation.

```text
Person A speaks English.

Person B speaks Japanese.
```

Without a common language, communication becomes difficult.

Computers face the same challenge.

Different companies build:

* Windows computers
* Linux servers
* Android phones
* iPhones
* IoT devices

How can they all communicate?

The answer is:

**Protocols**

---

## Protocol Concept

A **protocol** is simply:

> **A set of rules that defines how computers communicate with each other.**

Think about a game of cricket.

Everyone knows:

* How many players participate.
* How runs are scored.
* What counts as an out.
* How many overs are played.

Without agreed rules, there is no game.

Similarly,

without communication rules, there is no Internet.

---

## Human Communication Analogy

Imagine making a phone call.

Both people naturally follow certain rules:

* Say hello.
* Speak one at a time.
* Listen while the other person talks.
* End the conversation politely.

These are communication rules.

Computers also need communication rules.

Those rules are called **protocols**.

---

## Why Protocols Exist

Imagine if every company invented its own communication language.

Google sends:

```text
HELLO123
```

Microsoft expects:

```text
WELCOME456
```

Apple expects:

```text
APPLE789
```

Nothing would work together.

Instead,

everyone follows common communication standards.

Because of this:

* A Windows computer can access a Linux server.
* An Android phone can communicate with an iPhone.
* A Python backend can serve data to a React frontend.
* Different devices and operating systems can work together.

---

## What Do Protocols Define?

Protocols answer important questions such as:

* How does communication begin?
* How should data be formatted?
* Who sent the message?
* Who should receive it?
* How are errors handled?
* What happens if some data is lost?
* When should communication end?

Without protocols, computers would not know how to interpret incoming data.

---

## Example Without a Protocol

Suppose a computer receives:

```text
123456789ABCDE
```

Questions immediately arise:

* Where does the message start?
* Where does it end?
* Who sent it?
* Is the message complete?
* Is any data missing?

Without communication rules, these questions cannot be answered.

---

## Example With a Protocol

Now imagine the message contains additional information.

```text
Sender : Laptop

Receiver : Google

Length : 256 Bytes

Data :

GET /index.html
```

Now the receiving computer knows exactly how to process the message.

Protocols define this structure.

---

## Standardization

One of the greatest achievements of the Internet is **standardization**.

Standardization means:

> **Everyone agrees to follow the same communication standards.**

Because of standardization:

* Windows communicates with Linux.
* Android communicates with iOS.
* Chrome opens websites hosted on different operating systems.
* Python, Java, C++, and JavaScript applications can all communicate over the Internet.

Even though the hardware and software are different, the communication rules remain the same.

---

## Real-World Analogy

Imagine if every city had different meanings for traffic lights.

City A:

```text
Green = Stop
```

City B:

```text
Green = Go
```

Driving would become dangerous.

Instead,

traffic rules are standardized.

Network protocols work in exactly the same way.

---

## Communication Flow

Putting everything together:

```text
User

↓

Client

↓

Create Message

↓

Network

↓

Server

↓

Process Message

↓

Create Response

↓

Network

↓

Client

↓

User
```

Every modern web application follows this communication model.

---

## Summary

Computers communicate by exchanging structured messages across networks.

These messages travel through various networking technologies until they reach the destination.

For communication to work correctly, every device must follow a common set of rules known as **protocols**.

Because these protocols are standardized, billions of devices from different manufacturers can communicate reliably over the Internet.

---

## Key Takeaways

* Computer communication is the exchange of data between devices connected through a network.
* Information is exchanged using structured messages.
* The movement of these messages across a network is called data transmission.
* Data is usually divided into packets before being transmitted.
* Protocols define the rules that computers follow while communicating.
* Standardization ensures devices from different manufacturers can communicate successfully.

---


