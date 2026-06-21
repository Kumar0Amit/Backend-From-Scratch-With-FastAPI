# 2.7 DNS Security

## DNS Spoofing & DNS Cache Poisoning

## Introduction

DNS is one of the most important systems on the Internet.

Every time you visit a website, your computer trusts DNS to return the **correct IP address**.

But what happens if someone tricks DNS into returning the **wrong IP address**?

Instead of going to:

```text
google.com

↓

142.250.xxx.xxx
```

you could be redirected to:

```text
google.com

↓

203.0.113.50

(Attacker's Server)
```

Your browser still shows:

```text
https://google.com
```

but you are actually communicating with an attacker's machine (or, in practice today, you'll often receive a certificate warning if HTTPS is properly implemented).

This class of attacks includes:

* DNS Spoofing
* DNS Cache Poisoning

Although they are related, they are **not exactly the same thing**.

---

# Normal DNS Resolution

Suppose you visit:

```text
google.com
```

A normal lookup looks like:

```text
Browser

↓

Browser Cache

↓

OS Cache

↓

Hosts File

↓

Recursive Resolver

↓

Root Server

↓

.com TLD

↓

Google Authoritative Server

↓

A Record

↓

142.250.xxx.xxx

↓

Browser connects
```

Everything works correctly.

---

# What is DNS Spoofing?

## Definition

DNS Spoofing is an attack where an attacker **provides a fake DNS response**, causing a victim to connect to the wrong IP address.

Instead of receiving the legitimate DNS response,

the victim receives a forged one.

---

# Goal

The attacker's goal is:

```text
Victim

↓

google.com

↓

Fake IP

↓

Attacker's Server
```

The victim believes they are visiting Google,

but they are actually communicating with the attacker.

---

# Example

Suppose the real DNS answer is:

```text
google.com

↓

142.250.xxx.xxx
```

The attacker sends:

```text
google.com

↓

203.0.113.50
```

The browser trusts the fake response.

---

# Where Can Spoofing Happen?

A spoofed response can be introduced at several points:

```text
Victim

↓

Wi-Fi Network

↓

Router

↓

Recursive Resolver

↓

Internet
```

Possible attack locations include:

* Malicious public Wi-Fi
* Compromised router
* Malware on the victim's computer
* Network attacker capable of injecting fake DNS replies

---

# DNS Spoofing Flow

```text
Browser

↓

DNS Query

↓

Attacker Sends Fake DNS Reply

↓

Browser Accepts Fake IP

↓

Attacker's Website
```

Instead of the legitimate DNS server responding first,

the attacker attempts to respond with forged data.

---

# Real-World Analogy

Imagine asking someone:

> "Where is the State Bank?"

A stranger replies:

> "It's down that street."

But they intentionally send you to a fake bank.

That's DNS Spoofing.

---

# What is DNS Cache Poisoning?

DNS Cache Poisoning is a **specific type of DNS Spoofing**.

Instead of only fooling one DNS lookup,

the attacker **poisons a DNS cache**.

Once the fake record is cached,

every user relying on that cache receives the fake answer until the cache expires or is cleared.

---

# Goal

Suppose the Recursive Resolver cache normally contains:

```text
google.com

↓

142.250.xxx.xxx
```

The attacker changes it to:

```text
google.com

↓

203.0.113.50
```

Now every user receives:

```text
google.com

↓

203.0.113.50
```

until the cache entry expires.

---

# Example

Normal cache:

```text
Recursive Resolver Cache

---------------------------------

google.com

↓

142.250.xxx.xxx
```

Poisoned cache:

```text
Recursive Resolver Cache

---------------------------------

google.com

↓

203.0.113.50
```

Every user querying that resolver is redirected.

---

# Cache Poisoning Flow

```text
User A

↓

Recursive Resolver

↓

Fake Record Stored

↓

Cache Updated

────────────────────

User B

↓

Recursive Resolver

↓

Returns Fake Record

────────────────────

User C

↓

Recursive Resolver

↓

Returns Fake Record
```

One poisoned cache can affect many users.

---

# DNS Spoofing vs DNS Cache Poisoning

| DNS Spoofing                               | DNS Cache Poisoning                                   |
| ------------------------------------------ | ----------------------------------------------------- |
| Fake DNS response is sent to a victim.     | Fake DNS response is stored inside a DNS cache.       |
| Usually affects a single lookup or victim. | Can affect many users sharing the poisoned cache.     |
| May not persist after the lookup.          | Persists until the cache entry expires or is removed. |
| Can occur without modifying a cache.       | Specifically targets cached DNS data.                 |

Think of it this way:

* **Spoofing** = Lying once.
* **Cache Poisoning** = Writing the lie into everyone's address book.

---

# What Can an Attacker Do?

If successful, attackers may attempt to:

* Redirect users to phishing websites.
* Steal usernames and passwords.
* Deliver malware.
* Monitor user traffic.
* Block access to legitimate websites.

---

# Example Attack

Suppose the attacker creates:

```text
google-login.example
```

which visually resembles Google's login page.

The victim types:

```text
google.com
```

The poisoned DNS response returns:

```text
203.0.113.50
```

The browser connects to:

```text
Attacker's Server
```

The victim enters:

* Email
* Password

The attacker captures the credentials.

> **Modern browsers help protect against this.** If the attacker cannot present a valid TLS certificate for `google.com`, the browser will usually display a prominent security warning, making successful attacks much harder.

---

# Why HTTPS Helps

DNS determines **where** you connect.

HTTPS verifies **who** you connected to.

Example:

```text
DNS

↓

203.0.113.50

↓

TLS Certificate

↓

Certificate Invalid

↓

Browser Warning
```

The browser warns the user that the website's identity cannot be verified.

HTTPS does **not** stop DNS spoofing itself,

but it greatly reduces the chance of silently impersonating legitimate websites.

---

# How Do We Protect Against DNS Attacks?

## 1. DNSSEC (Domain Name System Security Extensions)

DNSSEC digitally signs DNS records.

The resolver verifies the signature before trusting the response.

If someone changes the DNS record:

```text
google.com

↓

203.0.113.50
```

the signature no longer matches,

and the response is rejected.

DNSSEC protects the integrity and authenticity of DNS data.

---

## 2. Use Trusted Recursive Resolvers

Examples include:

* Google Public DNS
* Cloudflare DNS
* Quad9

These providers implement modern security protections and are less vulnerable to many historical attacks.

---

## 3. Keep Routers Updated

Home routers are common attack targets.

Updating router firmware helps protect against vulnerabilities.

---

## 4. Use HTTPS

HTTPS helps detect impersonation by verifying server identity using digital certificates.

---

## 5. Clear DNS Cache

If DNS cache poisoning is suspected:

### Windows

```cmd
ipconfig /flushdns
```

### Linux (systemd-resolved)

```bash
sudo resolvectl flush-caches
```

### macOS

```bash
sudo dscacheutil -flushcache
sudo killall -HUP mDNSResponder
```

---

# Complete Comparison

## Normal DNS

```text
Browser

↓

Recursive Resolver

↓

Authoritative Server

↓

Correct IP

↓

Real Website
```

---

## DNS Spoofing

```text
Browser

↓

Fake DNS Reply

↓

Fake IP

↓

Attacker's Website
```

---

## DNS Cache Poisoning

```text
Attacker

↓

Recursive Resolver Cache

↓

Fake Record Stored

↓

Every User Receives Fake IP
```

---

# Summary Table

| Topic               | Description                                                                                 |
| ------------------- | ------------------------------------------------------------------------------------------- |
| DNS Spoofing        | An attacker sends a forged DNS response, redirecting a victim to an incorrect IP address.   |
| DNS Cache Poisoning | A forged DNS response is stored in a DNS cache, affecting future users of that cache.       |
| Goal                | Redirect users to attacker-controlled infrastructure.                                       |
| Common Risks        | Phishing, credential theft, malware distribution, traffic interception.                     |
| Major Defenses      | DNSSEC, HTTPS, trusted recursive resolvers, updated routers, cache flushing when necessary. |

---

# Key Takeaways

* DNS is based on trust—clients assume DNS responses are correct.
* **DNS Spoofing** tricks a client into accepting a forged DNS response.
* **DNS Cache Poisoning** stores forged DNS information in a cache, affecting multiple users.
* Cache poisoning is a specialized form of DNS spoofing with a broader impact.
* Modern HTTPS significantly reduces the effectiveness of many spoofing attacks by validating the server's identity.
* **DNSSEC** adds cryptographic signatures to DNS records, allowing resolvers to detect tampering and reject forged responses.
