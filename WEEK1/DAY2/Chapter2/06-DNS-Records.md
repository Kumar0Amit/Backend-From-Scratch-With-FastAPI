# 2.5 DNS Records

## Introduction

So far we've learned:

* DNS translates domain names into IP addresses.
* DNS uses Root, TLD, and Authoritative Name Servers.
* DNS caches responses for better performance.

But here's an important question:

> **Where is the actual information about a domain stored?**

The answer is:

**DNS Records.**

A DNS record is simply a piece of information stored on an **Authoritative Name Server**.

Think of a domain as a folder and DNS records as files inside that folder.

Example:

```text id="q0e6ax"
google.com

├── A Record
├── AAAA Record
├── MX Record
├── TXT Record
├── NS Record
├── SOA Record
├── CNAME Record
└── ...
```

Each record serves a different purpose.

---

# What is a DNS Record?

A **DNS Record** is an entry stored in a DNS zone that provides information about a domain.

Some records answer:

> "What is this website's IP address?"

Others answer:

> "Which server receives email?"

Others answer:

> "Which servers are authoritative?"

Each record has:

* Name
* Record Type
* Value
* TTL

Example:

```text id="uzm20k"
Name: example.com

Type: A

Value: 93.184.216.34

TTL: 3600
```

---

# 1. A Record (Address Record)

## Purpose

Maps a domain name to an **IPv4 address**.

Example:

```text id="wrvrrp"
google.com

↓

142.250.183.78
```

DNS Record:

```text id="szm4z8"
Name: google.com

Type: A

Value: 142.250.183.78
```

When your browser requests:

```text id="4vcgk5"
google.com
```

the Authoritative Server returns the A Record.

---

## Example

```text id="p8ltdb"
example.com

↓

93.184.216.34
```

---

## When Used

* Hosting websites
* Backend servers
* APIs
* Load balancers

---

# 2. AAAA Record (Quad-A Record)

## Purpose

Maps a domain to an **IPv6 address**.

Example:

```text id="08fgiv"
google.com

↓

2607:f8b0:4004:814::200e
```

DNS Record:

```text id="o6hbmm"
Type: AAAA

Value:
2607:f8b0:4004:814::200e
```

---

## Difference

| Record | IP Version |
| ------ | ---------- |
| A      | IPv4       |
| AAAA   | IPv6       |

---

# 3. CNAME Record (Canonical Name)

## Purpose

Creates an **alias** for another domain.

Instead of pointing directly to an IP,

it points to another hostname.

Example:

```text id="hy26m3"
www.example.com

↓

example.com
```

DNS Record:

```text id="ngt7fd"
Type: CNAME

www.example.com

↓

example.com
```

Now DNS resolves:

```text id="5h8jfr"
www.example.com

↓

example.com

↓

93.184.216.34
```

---

## Why Use CNAME?

Suppose both of these should point to the same server:

```text id="hbrquu"
example.com

www.example.com
```

Instead of maintaining two A Records,

you create:

```text id="b40pcq"
example.com

↓

A Record

↓

93.184.216.34
```

and

```text id="4cbxft"
www.example.com

↓

CNAME

↓

example.com
```

Now changing one A Record updates both.

---

# 4. MX Record (Mail Exchange)

## Purpose

Specifies which server receives email for a domain.

Example:

```text id="6jv76r"
user@example.com
```

Which mail server should receive it?

DNS answers using the MX Record.

Example:

```text id="u4bsld"
example.com

↓

mail.example.com
```

DNS Record:

```text id="5b0nif"
Type: MX

Priority: 10

Server:

mail.example.com
```

---

## Priority

Multiple mail servers may exist.

Example:

```text id="vn3q1v"
Priority 10

mail1.example.com

Priority 20

mail2.example.com
```

Lower number = higher priority.

---

# 5. TXT Record (Text Record)

## Purpose

Stores arbitrary text associated with a domain.

Originally created for human-readable notes,

today it is mainly used for verification and security.

Examples:

* Domain ownership verification
* Email authentication
* SPF
* DKIM
* DMARC

Example:

```text id="0r52s2"
Type: TXT

"v=spf1 include:_spf.google.com ~all"
```

Another example:

```text id="wj65h8"
google-site-verification=

abc123xyz
```

---

## Common Uses

* Verify ownership
* Prevent email spoofing
* Configure security policies

---

# 6. NS Record (Name Server)

## Purpose

Specifies which Name Servers are authoritative for a domain.

Example:

```text id="1k5x9e"
example.com

↓

ns1.exampledns.com

↓

ns2.exampledns.com
```

DNS Record:

```text id="qbh5z2"
Type: NS

ns1.exampledns.com

ns2.exampledns.com
```

Without NS records,

DNS wouldn't know which server contains the official records.

---

# 7. PTR Record (Pointer Record)

## Purpose

Maps an **IP address back to a domain name**.

This is called **Reverse DNS**.

Normal DNS:

```text id="c1jsk8"
google.com

↓

142.250.xxx.xxx
```

PTR Record:

```text id="w2rdz7"
142.250.xxx.xxx

↓

google.com
```

---

## Common Uses

* Email spam filtering
* Logging
* Network troubleshooting
* Security audits

---

# 8. SOA Record (Start of Authority)

## Purpose

Contains administrative information about a DNS zone.

Every DNS zone has exactly one SOA Record.

Example:

```text id="pdjlwm"
Type: SOA

Primary Name Server:

ns1.example.com

Responsible Email:

admin@example.com

Serial Number:

2026062101

Refresh:

3600

Retry:

600

Expire:

1209600

Minimum TTL:

86400
```

---

## Why Important?

DNS servers use the SOA record to determine:

* Which server is primary.
* Whether records have changed.
* When to synchronize secondary servers.

---

# 9. SRV Record (Service Record) — Overview

## Purpose

Specifies which server provides a particular service.

Unlike A Records,

SRV records include:

* Hostname
* Port Number
* Priority
* Weight

Example:

```text id="1z4r6m"
_sip._tcp.example.com

↓

sipserver.example.com

↓

Port 5060
```

---

## Used By

* Microsoft Active Directory
* SIP (VoIP)
* XMPP
* LDAP
* Kerberos

Most web developers rarely configure SRV records directly, but system administrators frequently use them.

---

# Example DNS Zone

```text id="4w1omg"
example.com

├── A
│     └── 93.184.216.34
│
├── AAAA
│     └── 2606:2800:220...
│
├── CNAME
│     └── www → example.com
│
├── MX
│     └── mail.example.com
│
├── TXT
│     └── SPF / DKIM
│
├── NS
│     └── ns1.exampledns.com
│
├── PTR
│     └── Reverse Lookup
│
├── SOA
│     └── Zone Information
│
└── SRV
      └── Service Discovery
```

---

# How DNS Uses These Records

Suppose a browser asks:

```text id="2c5r54"
example.com
```

DNS might return:

```text id="l8emql"
A Record

↓

93.184.216.34
```

An email server asks:

```text id="fjlwm5"
Who handles mail?
```

DNS returns:

```text id="9k4cxn"
MX Record

↓

mail.example.com
```

An administrator asks:

```text id="kyspl2"
Who owns this DNS zone?
```

DNS returns:

```text id="h0y8kk"
SOA Record
```

Each application requests only the record type it needs.

---

# Summary Table

| Record Type | Purpose                                                            |
| ----------- | ------------------------------------------------------------------ |
| **A**       | Maps a domain to an IPv4 address                                   |
| **AAAA**    | Maps a domain to an IPv6 address                                   |
| **CNAME**   | Creates an alias pointing to another hostname                      |
| **MX**      | Specifies mail servers for receiving email                         |
| **TXT**     | Stores text for verification and security (SPF, DKIM, DMARC, etc.) |
| **NS**      | Specifies the authoritative name servers for a domain              |
| **PTR**     | Maps an IP address back to a domain (Reverse DNS)                  |
| **SOA**     | Stores administrative information about a DNS zone                 |
| **SRV**     | Specifies the server, port, and priority for a particular service  |

---

# Key Takeaways

* **DNS Records** are pieces of information stored on an **Authoritative Name Server**.
* Different record types serve different purposes—web browsing, email delivery, verification, service discovery, and DNS administration.
* **A** and **AAAA** records map domains to IPv4 and IPv6 addresses.
* **CNAME** creates aliases between hostnames.
* **MX** records tell email systems where to deliver mail.
* **TXT** records are widely used for ownership verification and email security.
* **NS** records identify the authoritative name servers for a domain.
* **PTR** records enable reverse DNS lookups.
* **SOA** records define administrative information for a DNS zone.
* **SRV** records help clients discover services running on specific hosts and ports.
