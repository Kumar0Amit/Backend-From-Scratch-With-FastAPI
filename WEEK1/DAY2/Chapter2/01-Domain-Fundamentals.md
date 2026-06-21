# DNS Fundamentals

# 2.1 What is DNS?

## Introduction

In the previous chapter, we learned that humans prefer using **domain names** like:

```text
google.com
youtube.com
github.com
```

However, computers do **not** understand these names.

They only communicate using **IP addresses**, such as:

```text
142.250.183.78
104.18.32.45
140.82.121.4
```

This creates a problem:

> **How does a computer know the IP address of `google.com`?**

The answer is **DNS**.

---

# What is DNS?

**DNS** stands for:

```text
Domain Name System
```

DNS is a **distributed hierarchical system** that translates **human-readable domain names** into **machine-readable IP addresses**.

In simple words:

> DNS converts website names into IP addresses so computers can communicate.

For example:

```text
google.com
      │
      ▼
DNS
      │
      ▼
142.250.183.78
```

Without DNS, every Internet user would have to remember the IP address of every website they wanted to visit.

---

# DNS Definition

A formal definition is:

> **The Domain Name System (DNS) is a distributed naming system that maps domain names to IP addresses, allowing humans to access Internet resources using easy-to-remember names instead of numerical addresses.**

Let's break this definition down:

### Distributed

DNS is **not one giant server**.

Instead, it consists of **millions of DNS servers** distributed around the world.

Each server is responsible for only a small part of the global DNS database.

This makes DNS:

* Fast
* Scalable
* Fault tolerant

---

### Naming System

DNS manages the names of Internet resources.

Examples:

```text
google.com
github.com
amazon.com
mail.google.com
docs.python.org
```

Each of these names can be translated into one or more IP addresses.

---

### Mapping

DNS performs a mapping:

```text
Domain Name
        │
        ▼
IP Address
```

Example:

```text
github.com
      │
      ▼
140.82.xxx.xxx
```

This process is called **Name Resolution**.

---

# Why DNS Exists

Imagine the Internet without DNS.

To visit Google, you would have to type:

```text
142.250.183.78
```

To visit GitHub:

```text
140.82.121.4
```

To visit Amazon:

```text
54.239.xxx.xxx
```

You would need to remember hundreds or even thousands of IP addresses.

This would make the Internet extremely difficult to use.

DNS exists to solve this problem by allowing humans to use meaningful names instead of numbers.

---

## Another Reason: IP Addresses Can Change

Suppose today Google's server has the IP:

```text
142.250.183.78
```

Tomorrow, Google upgrades its infrastructure and the IP changes to:

```text
34.117.xxx.xxx
```

If users had memorized the old IP address, every bookmark, application, and user would have to update it manually.

Instead, users continue typing:

```text
google.com
```

Only the DNS record changes.

```text
google.com
      │
      ▼
Old IP
142.250.xxx.xxx

        ↓

New IP
34.117.xxx.xxx
```

The user doesn't notice anything.

This flexibility is one of the biggest reasons DNS exists.

---

# DNS as the Internet's Phonebook

A phonebook stores information like this:

```text
John
   │
   ▼
+91 9876543210

Alice
   │
   ▼
+44 123456789

Bob
   │
   ▼
+1 5551234567
```

You search using a **name**, not a phone number.

The phonebook translates:

```text
Name
   │
   ▼
Phone Number
```

DNS works exactly the same way.

Instead of:

```text
Person Name
        │
        ▼
Phone Number
```

DNS performs:

```text
Domain Name
        │
        ▼
IP Address
```

Example:

```text
google.com
      │
      ▼
142.250.xxx.xxx
```

That's why DNS is often called:

> **The Internet's Phonebook**

---

# What is Name Resolution?

The process of converting a domain name into its IP address is called **Name Resolution**.

Example:

You type:

```text
github.com
```

The browser asks DNS:

```text
"What is the IP address of github.com?"
```

DNS replies:

```text
140.82.xxx.xxx
```

The browser then connects to that IP address.

This entire process is called **DNS Name Resolution**.

---

# Complete Name Resolution Flow

```text
You type

github.com
      │
      ▼

Browser

      │
      ▼

DNS Lookup

      │
      ▼

DNS returns

140.82.xxx.xxx

      │
      ▼

Browser creates TCP connection

      │
      ▼

Browser sends HTTP request

      │
      ▼

Server sends HTTP response

      │
      ▼

Browser renders the webpage
```

Notice that **DNS is involved only in finding the IP address**.

After the browser learns the IP address, DNS is no longer needed for that connection.

---

# Important Characteristics of DNS

* DNS translates **domain names** into **IP addresses**.
* DNS is a **distributed** system with servers located worldwide.
* DNS makes the Internet easy for humans to use.
* DNS allows IP addresses to change without affecting users.
* DNS performs **Name Resolution**, which is the process of converting a domain name into an IP address.
* DNS operates before the browser establishes a TCP connection to the destination server.

---

# Summary Table

| Term                 | Description                                                                        |
| -------------------- | ---------------------------------------------------------------------------------- |
| DNS                  | Domain Name System                                                                 |
| Purpose              | Converts domain names into IP addresses                                            |
| Domain Name          | Human-readable website name (e.g., `google.com`)                                   |
| IP Address           | Machine-readable network address                                                   |
| Name Resolution      | The process of translating a domain name into an IP address                        |
| Distributed System   | DNS servers are spread across the world rather than existing as one central server |
| Internet's Phonebook | A common analogy for DNS because it maps names to addresses                        |

---

# Key Takeaways

* Computers communicate using **IP addresses**, while humans prefer **domain names**.
* **DNS (Domain Name System)** bridges this gap by translating names into IP addresses.
* DNS exists because remembering numerical IP addresses is impractical and because IP addresses can change over time.
* DNS is often described as **the Internet's phonebook**, mapping names to addresses.
* The process of converting a domain name into an IP address is called **Name Resolution**.
* DNS is the first step that occurs before a browser can establish a network connection with a website.
