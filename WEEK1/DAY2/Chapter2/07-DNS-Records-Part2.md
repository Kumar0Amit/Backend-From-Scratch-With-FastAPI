# DNS Records Explained Simply But In Detail

## Introduction

When people first learn DNS, they usually think:

> "A Record = IP Address"

That's correct—but it doesn't answer the important questions:

* **Who uses this record?**
* **Why does it exist?**
* **When is it queried?**
* **How does it participate in a real network transaction?**
* **How can attackers abuse it?**

This chapter answers those questions using **real-world examples** (primarily `google.com` and `microsoft.com`) and shows how each DNS record participates in actual Internet communication.

---

# 1. A Record (Address Record)

## Purpose

Maps a hostname to an **IPv4 address**.

Example:

```text
google.com

↓

142.250.xxx.xxx
```

---

## Who Uses It?

* Web Browsers
* Mobile Apps
* API Clients
* Operating Systems
* Any software connecting via IPv4

---

## Why Is It Needed?

Computers communicate using IP addresses, not domain names.

The browser cannot create a TCP connection to:

```text
google.com
```

It must first know:

```text
142.250.xxx.xxx
```

The A Record provides that mapping.

---

## When Is It Requested?

Whenever an application wants to connect to a website over IPv4.

Examples:

* Opening a website
* Calling an API
* Downloading software
* Connecting to a backend server

---

## How Is It Used?

Suppose you type:

```text
https://google.com
```

Step-by-step:

```text
Browser

↓

DNS Query

Type = A

↓

Authoritative Server

↓

142.250.xxx.xxx

↓

Browser

↓

TCP Handshake

↓

HTTPS

↓

HTTP Request
```

The A Record is only used during DNS resolution.

After the browser learns the IP, DNS is no longer involved for that connection.

---

## Real Example

```text
google.com

Type: A

Value:

142.250.xxx.xxx
```

(The exact IP varies because Google uses load balancing.)

---

## Common Exploits (Brief)

* DNS Cache Poisoning
* Hosts File Manipulation
* DNS Spoofing
* Typosquatting (combined with fake A records)

---

# 2. AAAA Record (IPv6 Address Record)

## Purpose

Maps a hostname to an IPv6 address.

---

## Who Uses It?

Exactly the same clients that use A records,

but only if IPv6 connectivity exists.

---

## Why Needed?

IPv4 addresses are limited.

IPv6 provides a vastly larger address space.

Modern operating systems usually prefer IPv6 when available.

---

## When Requested?

Usually alongside the A Record.

Many browsers request both simultaneously.

Example:

```text
Query A

AND

Query AAAA
```

The operating system decides which address to use.

---

## How Used?

```text
Browser

↓

AAAA Query

↓

2607:f8b0:4004:814::200e

↓

TCP over IPv6
```

---

## Real Example

```text
google.com

AAAA

2607:f8b0:4004:814::200e
```

---

## Common Exploits (Brief)

* IPv6 misconfiguration
* Rogue IPv6 DNS environments
* IPv6-only attack paths

---

# 3. CNAME Record (Canonical Name)

## Purpose

Creates an alias to another hostname.

Example:

```text
www.google.com

↓

google.com
```

---

## Who Uses It?

DNS Resolvers.

Browsers never "follow" CNAMEs themselves.

The resolver does.

---

## Why Needed?

Imagine:

```text
shop.example.com

blog.example.com

api.example.com
```

All point to the same infrastructure.

Instead of updating multiple A records,

one A record can exist and others become aliases.

---

## When Requested?

Whenever the queried hostname is actually a CNAME.

---

## How Used?

```text
Browser

↓

DNS Query

↓

CNAME Returned

↓

Alias Found

↓

Resolver Queries Target

↓

A Record

↓

Browser Receives IP
```

---

## Real Example

Many Microsoft cloud services and CDN endpoints use CNAME chains that ultimately point to infrastructure hosted on Azure or CDN providers.

Example (simplified):

```text
www.microsoft.com

↓

CNAME

↓

microsoft.com

↓

A Record
```

---

## Common Exploits (Brief)

* Dangling CNAME takeover
* Subdomain hijacking
* CDN misconfiguration

---

# 4. MX Record (Mail Exchange)

## Purpose

Specifies which server receives email.

---

## Who Uses It?

Mail Servers

Examples:

* Gmail
* Outlook
* Exchange
* Postfix

Browsers never use MX records.

---

## Why Needed?

Suppose someone sends:

```text
john@gmail.com

↓

support@microsoft.com
```

How does Gmail know where Microsoft's mail server is?

MX records answer that question.

---

## When Requested?

Every time an email is delivered.

Not when it is read.

Only during delivery.

---

## How Used?

```text
Sender Mail Server

↓

DNS MX Query

↓

mail.protection.outlook.com

↓

A/AAAA Lookup

↓

Connect SMTP

↓

Deliver Email
```

---

## Real Example

Microsoft uses records similar to:

```text
microsoft.com

MX

↓

microsoft-com.mail.protection.outlook.com
```

---

## Common Exploits (Brief)

* Mail interception after DNS compromise
* Fake MX infrastructure
* Email routing attacks

---

# 5. TXT Record

## Purpose

Stores arbitrary text.

Today it is primarily used for verification and security.

---

## Who Uses It?

* Google Workspace
* Microsoft 365
* Email Servers
* Certificate Authorities
* Cloud Providers

Browsers almost never request TXT records.

---

## Why Needed?

Examples:

* Domain ownership verification
* SPF
* DKIM
* DMARC

---

## When Requested?

Depends on the service.

Examples:

During:

* Email validation
* Domain verification
* SSL certificate issuance

---

## How Used?

Email example:

```text
Receiving Mail Server

↓

TXT Lookup

↓

SPF Record

↓

Allowed?

↓

Accept Email
```

---

## Real Example

Google SPF:

```text
v=spf1 include:_spf.google.com ~all
```

Google verification:

```text
google-site-verification=

xxxxxxxx
```

---

## Common Exploits (Brief)

* Weak SPF policies
* Missing DMARC
* DKIM misconfiguration
* Information disclosure

---

# 6. NS Record (Name Server)

## Purpose

Specifies which DNS servers are authoritative.

---

## Who Uses It?

DNS Servers.

Not browsers.

---

## Why Needed?

Without NS records,

Root and TLD servers wouldn't know where a domain's official DNS records are stored.

---

## When Requested?

During DNS resolution.

Especially when moving from TLD servers to authoritative servers.

---

## How Used?

```text
Root

↓

.com

↓

NS Records

↓

ns1.google.com

↓

Ask There
```

---

## Real Example

Google uses authoritative name servers similar to:

```text
google.com

NS

↓

ns1.google.com

ns2.google.com

ns3.google.com

ns4.google.com
```

---

## Common Exploits (Brief)

* DNS hijacking
* Registrar compromise
* NS delegation attacks

---

# 7. PTR Record (Pointer Record)

## Purpose

Maps an IP address back to a hostname.

Reverse DNS.

---

## Who Uses It?

* Mail Servers
* Security Systems
* Logging Systems
* Network Administrators

---

## Why Needed?

Some mail servers reject emails from IPs without valid reverse DNS.

---

## When Requested?

Mostly:

* Email delivery
* Logging
* Security analysis

---

## How Used?

```text
Incoming Connection

↓

Reverse DNS Lookup

↓

PTR Record

↓

Hostname

↓

Continue Validation
```

---

## Real Example

```text
8.8.8.8

↓

dns.google
```

---

## Common Exploits (Brief)

* Fake reverse DNS
* Reputation bypass attempts

---

# 8. SOA Record (Start of Authority)

## Purpose

Stores administrative information for a DNS zone.

---

## Who Uses It?

* DNS Servers
* Secondary DNS Servers

Browsers never use it directly.

---

## Why Needed?

DNS servers must know:

* Which server is primary
* Serial number
* Refresh interval
* Retry interval
* Expiration

---

## When Requested?

Mainly during DNS zone synchronization.

---

## How Used?

```text
Secondary DNS

↓

SOA Query

↓

Serial Number

↓

Changed?

↓

Yes

↓

Zone Transfer
```

---

## Real Example

```text
google.com

SOA

↓

Primary NS

↓

Serial Number

↓

Refresh

↓

Retry
```

---

## Common Exploits (Brief)

* Information disclosure
* Poorly configured zone transfers (AXFR)

---

# 9. SRV Record (Service Record)

## Purpose

Specifies which server provides a service and on which port.

---

## Who Uses It?

Applications such as:

* Microsoft Active Directory
* SIP
* XMPP
* LDAP
* Kerberos

Browsers usually do not query SRV records.

---

## Why Needed?

Suppose a client needs:

```text
LDAP

↓

Which server?

↓

Which port?
```

SRV answers both.

---

## When Requested?

Before connecting to certain network services.

---

## How Used?

```text
Client

↓

SRV Query

↓

Server

↓

Port

↓

Connect
```

---

## Real Example

Microsoft Active Directory commonly uses records similar to:

```text
_ldap._tcp.dc._msdcs.example.com

↓

dc01.example.com

Port 389
```

---

## Common Exploits (Brief)

* Service enumeration
* Internal infrastructure discovery

---

# Which Record Is Used During Different Activities?

| Activity                                        | DNS Record Used |
| ----------------------------------------------- | --------------- |
| Open a website                                  | A / AAAA        |
| Visit [www.example.com](http://www.example.com) | CNAME → A/AAAA  |
| Send an email                                   | MX → A/AAAA     |
| Verify Google Workspace                         | TXT             |
| SPF/DKIM/DMARC                                  | TXT             |
| Find authoritative DNS servers                  | NS              |
| Reverse lookup an IP                            | PTR             |
| Synchronize DNS servers                         | SOA             |
| Discover LDAP/SIP services                      | SRV             |

---

# Visual Summary

```text
Open Website
      │
      ▼
A / AAAA

────────────────────────

Alias
      │
      ▼
CNAME

────────────────────────

Send Email
      │
      ▼
MX

────────────────────────

Email Security
      │
      ▼
TXT

────────────────────────

DNS Delegation
      │
      ▼
NS

────────────────────────

Reverse Lookup
      │
      ▼
PTR

────────────────────────

DNS Administration
      │
      ▼
SOA

────────────────────────

Service Discovery
      │
      ▼
SRV
```

---

# Final Mental Model

Think of DNS as a large office building:

* **A Record** → Street address of the building.
* **AAAA Record** → Same address using a newer navigation system (IPv6).
* **CNAME** → "This office has moved next door—go there instead."
* **MX Record** → The building's mail room.
* **TXT Record** → Notices and security instructions posted at reception.
* **NS Record** → The reception desk that tells visitors which office manages the building.
* **PTR Record** → Looking up the company's name from its street address.
* **SOA Record** → The building's administration office and maintenance schedule.
* **SRV Record** → A directory showing where specific services (HR, IT, Conference Room) are located.

Understanding **who**, **why**, **when**, and **how** each record is used makes DNS much easier to reason about than simply memorizing record names.
