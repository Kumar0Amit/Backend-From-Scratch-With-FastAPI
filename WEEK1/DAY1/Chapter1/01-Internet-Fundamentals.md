# Module 1 – Internet Fundamentals

---

# 1.1 History of the Internet

## What is the Internet?

Before learning backend development, it's important to understand **what the Internet actually is** and **why it exists**.

Every API request your backend receives, every webpage you open, and every message you send travels through the Internet.

---

## Before the Internet

Imagine the 1950s.

Computers were:

* Huge
* Extremely expensive
* Standalone machines
* Unable to communicate with each other

Every computer was like an isolated island.

```text
Computer A

(no connection)

Computer B

(no connection)

Computer C
```

Sharing information meant physically transporting:

* Punch cards
* Magnetic tapes
* Printed documents

There were no:

* Websites
* Emails
* Cloud storage
* Online databases

Every computer worked independently.

---

## The Cold War Problem

During the 1960s, the United States and the Soviet Union were engaged in the Cold War.

One important concern was communication.

Traditional telephone systems relied on a dedicated communication path.

Imagine a network like this:

```text
A ---- B ---- C ---- D
```

If one important connection failed:

```text
A    X    C ---- D
```

Everything beyond that point became unreachable.

This was a major problem for military communication because a single failure could disconnect an entire region.

A more reliable communication system was needed.

---

## Birth of ARPANET

The solution came from the **Advanced Research Projects Agency (ARPA)**, a research organization funded by the U.S. Department of Defense.

ARPA funded a project called:

**ARPANET**

ARPANET became the world's first large-scale packet-switched computer network.

It officially started in **1969**.

Initially, it connected only four computers located at research institutions and universities.

```text
University A
      |
University B
      |
University C
      |
University D
```

Although it connected only four computers, it introduced ideas that later became the foundation of the modern Internet.

---

## The First Internet Message

The first message sent over ARPANET was supposed to be:

```text
LOGIN
```

However, the receiving computer crashed after receiving only:

```text
L
O
```

So the first Internet message in history was simply:

```text
LO
```

---

## Why Was ARPANET Created?

ARPANET was created to solve several important problems.

### 1. Resource Sharing

Computers were extremely expensive.

Instead of every university purchasing its own powerful computer, multiple universities could share computing resources.

```text
University A
      |
 Powerful Computer
      |
University B
      |
University C
```

---

### 2. Communication

Researchers wanted to exchange:

* Research papers
* Files
* Software
* Experimental results

without physically mailing magnetic tapes.

---

### 3. Reliability

The network needed to continue working even if part of it failed.

Instead of using a single communication path:

```text
A ---- B ---- C
```

A more connected network could be built.

```text
A ----- B
|       |
|       |
D ----- C
```

If one path failed, communication could continue through another route.

This concept later became one of the defining characteristics of the Internet.

---

## Evolution of the Internet

ARPANET gradually expanded.

```text
1969
4 Computers

↓

1970s
Dozens of Computers

↓

1980s
Hundreds of Computers

↓

1990s
Thousands of Networks

↓

Today
Billions of Connected Devices
```

As more organizations created their own networks, a way was needed to connect all of them.

This led to the adoption of common communication protocols, especially **TCP/IP**.

Once different networks adopted the same communication rules, they could communicate with each other.

This became the modern Internet.

---

## Why Was the Internet Created?

Many people believe the Internet was created only for military purposes.

While military reliability was one motivation, the Internet evolved because it solved many broader problems.

### Communication

People could exchange information instantly instead of sending physical documents.

Examples:

* Email
* Instant messaging
* Video calls

---

### Resource Sharing

Organizations could remotely access powerful computers and shared resources.

---

### Information Sharing

Knowledge became globally accessible through websites and online services.

---

### Global Connectivity

People from different countries could communicate almost instantly.

---

### Business

The Internet enabled entirely new industries such as:

* Online shopping
* Digital banking
* Cloud computing
* Video streaming
* Remote work
* Social media

---

## Circuit Switching

Before the Internet, telephone systems mainly used **Circuit Switching**.

When you made a phone call, a dedicated communication path was established.

```text
You

 |

A

 |

B

 |

C

 |

Friend
```

That path remained reserved until the call ended.

Even during moments of silence, the communication path remained occupied.

### Advantages

* Constant bandwidth
* Predictable communication
* Low delay after connection setup

### Disadvantages

* Wastes resources when idle
* A broken connection ends the communication
* Not suitable for computer networks where communication is bursty

---

## Packet Switching

The Internet uses **Packet Switching**.

Instead of sending one continuous stream of data, information is divided into many small pieces called **packets**.

Suppose you send:

```text
Hello World
```

It may be divided into:

```text
Packet 1

Packet 2

Packet 3
```

Each packet can travel independently.

```text
Packet 1
A → B → D

Packet 2
A → C → D

Packet 3
A → E → D
```

When all packets arrive at the destination, they are reassembled into the original message.

---

## Why Packet Switching Was Revolutionary

If one communication path becomes unavailable:

```text
A ---- B ---- D
```

the packets can simply take another route.

```text
A ---- C ---- D
```

This makes the network:

* More reliable
* More efficient
* Better at sharing communication resources
* Able to continue operating despite failures

These characteristics make packet switching ideal for the Internet.

---

## Packet Switching vs Circuit Switching

| Feature            | Circuit Switching                      | Packet Switching                    |
| ------------------ | -------------------------------------- | ----------------------------------- |
| Communication Path | Dedicated                              | Shared                              |
| Resource Usage     | Reserved throughout communication      | Shared among users                  |
| Failure Handling   | Communication stops if the path breaks | Packets can take alternative routes |
| Efficiency         | Lower                                  | Higher                              |
| Common Usage       | Traditional telephone systems          | Internet                            |

---

## Summary

The Internet did not appear overnight.

It evolved from ARPANET, a research project designed to create reliable communication between computers.

Over time, independent computer networks adopted common communication protocols, allowing them to interconnect and form today's global Internet.

One of the most important innovations was **packet switching**, which allows data to travel through multiple routes instead of relying on a single dedicated path.

---

## Key Takeaways

* Before the Internet, computers operated independently with no direct communication.
* ARPANET, launched in 1969, became the foundation of the modern Internet.
* The Internet was created to improve communication, resource sharing, reliability, and information exchange.
* Packet Switching divides data into packets that can travel independently across different routes.
* Circuit Switching reserves one dedicated communication path, while Packet Switching shares network resources efficiently.
* Modern Internet communication is built upon ideas first introduced by ARPANET.

---

