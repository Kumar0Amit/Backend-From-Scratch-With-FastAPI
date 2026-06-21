# DNS Caching 

## Introduction

When you type a website like:

```text
google.com
```

your computer does **not** immediately ask DNS servers on the Internet.

Instead, it first checks several local sources to see if it already knows the answer.

This makes DNS lookups much faster and reduces Internet traffic.

There are three main places that are checked:

1. Browser DNS Cache
2. Operating System (OS) DNS Cache
3. Hosts File

If none of these contain the answer, the request is sent to a **Recursive DNS Resolver**.

---

# DNS Lookup Order

A simplified DNS lookup order is:

```text
User Types Domain
        │
        ▼
Browser DNS Cache
        │
        ▼
Operating System DNS Cache
        │
        ▼
Hosts File
        │
        ▼
Recursive DNS Resolver
        │
        ▼
Root Name Server
        │
        ▼
TLD Name Server
        │
        ▼
Authoritative Name Server
        │
        ▼
IP Address Returned
```

> **Note:** On many operating systems, the exact order between the OS DNS cache and the Hosts file is managed by the operating system's name resolution mechanism. Conceptually, you can think of both as local checks before a network DNS query is made.

---

# 1. Browser DNS Cache

Modern browsers maintain their own **in-memory DNS cache**.

When you visit a website, the browser stores its IP address for a limited time.

Example:

```text
Browser DNS Cache

-----------------------------------------------
Domain              IP Address         TTL
-----------------------------------------------
google.com          142.250.183.78     220 sec
github.com          140.82.121.4       180 sec
youtube.com         142.251.40.206     90 sec
-----------------------------------------------
```

If you visit **google.com** again before the TTL expires, the browser immediately returns the cached IP address.

```text
Browser

↓

Browser DNS Cache

↓

Found

↓

Return IP
```

No network request is needed.

---

## Why Browsers Have Their Own Cache

Each browser keeps its own cache because it can respond instantly without asking the operating system.

Example:

```text
Chrome
   │
   ▼
Chrome DNS Cache
```

Firefox cannot access Chrome's DNS cache.

Each browser maintains its own separate cache.

---

## Viewing Browser DNS Cache

### Google Chrome

Open:

```text
chrome://net-internals/#dns
```

or (newer versions):

```text
chrome://net-export/
```

> **Note:** Google has removed the old `chrome://net-internals/#dns` page in many recent Chrome versions. If it isn't available, use the OS DNS cache tools below or browser developer/network tools.

---

### Microsoft Edge

```text
edge://net-internals/#dns
```

(Availability depends on the Edge version.)

---

### Firefox

Firefox does not provide a simple built-in page to view the DNS cache like older Chromium browsers.

You can inspect or clear DNS-related settings through:

```text
about:networking#dns
```

This page shows Firefox's DNS cache and allows you to clear it.

---

# 2. Operating System (OS) DNS Cache

The operating system also stores recently resolved DNS records.

Unlike the browser cache, the OS cache is **shared by all applications**.

Example:

```text
OS DNS Cache

-----------------------------------------------
Domain              IP Address         TTL
-----------------------------------------------
google.com          142.250.183.78     100 sec
reddit.com          151.101.65.140     250 sec
amazon.com          54.239.xxx.xxx     60 sec
-----------------------------------------------
```

If the browser cache misses:

```text
Browser

↓

OS DNS Cache

↓

Found

↓

Return IP
```

---

## Why Does the OS Have a Cache?

The operating system serves many applications.

Example:

```text
Chrome

↓

Windows DNS Cache

↑
Firefox

↑
VS Code

↑
Steam

↑
Discord
```

Instead of each application contacting DNS servers separately, they all benefit from the shared OS cache.

---

# Viewing the OS DNS Cache

## Windows

### View the DNS Cache

Open **Command Prompt** and run:

```cmd
ipconfig /displaydns
```

Example output:

```text
Record Name . . . . . : google.com
Record Type . . . . . : A
Time To Live  . . . . : 180
Data Length . . . . . : 4
Section . . . . . . . : Answer
A (Host) Record . . . : 142.250.183.78
```

### Clear the DNS Cache

```cmd
ipconfig /flushdns
```

---

## Linux

Depending on your Linux distribution:

### systemd-resolved

View cache statistics:

```bash
resolvectl statistics
```

or

```bash
systemd-resolve --statistics
```

Flush the cache:

```bash
sudo resolvectl flush-caches
```

or

```bash
sudo systemd-resolve --flush-caches
```

> **Note:** Most Linux systems do not maintain a DNS cache unless a caching service such as **systemd-resolved**, **dnsmasq**, or **nscd** is running.

---

## macOS

Display cached DNS information (limited):

```bash
sudo dscacheutil -cachedump -entries Host
```

Flush the DNS cache:

```bash
sudo dscacheutil -flushcache
sudo killall -HUP mDNSResponder
```

---

# 3. Hosts File

The **Hosts File** is **not a cache**.

It is a plain text file that allows you to manually map domain names to IP addresses.

---

## Windows Location

```text
C:\Windows\System32\drivers\etc\hosts
```

---

## Linux / macOS Location

```text
/etc/hosts
```

---

## Example Hosts File

```text
127.0.0.1       localhost

192.168.1.100   myserver.local

10.0.0.20       database.company

142.250.183.78  google.com
```

Each line contains:

```text
IP Address        Domain Name
```

---

## What Happens?

Suppose you add:

```text
1.2.3.4    google.com
```

Now your computer believes:

```text
google.com

↓

1.2.3.4
```

DNS servers are never contacted.

The Hosts file overrides DNS resolution for matching entries.

---

# Why Malware Targets the Hosts File

Because it has priority over normal DNS lookups.

Example:

```text
google.com

↓

1.2.3.4
```

Instead of reaching Google's real servers, your computer would attempt to connect to `1.2.3.4`.

For this reason, malware has historically modified the Hosts file to redirect users to malicious websites.

---

# Browser Cache vs OS Cache

| Feature                     | Browser Cache | OS Cache |
| --------------------------- | ------------- | -------- |
| Shared by all applications? | ❌ No          | ✅ Yes    |
| Visible to other browsers?  | ❌ No          | ✅ Yes    |
| Exists in memory?           | ✅ Yes         | ✅ Yes    |
| Used only by one browser?   | ✅ Yes         | ❌ No     |

---

---

## Does the Recursive Resolver have its own TLD?

No.

It doesn't own a TLD.

Instead, it caches information it has learned from previous queries.

This is an important distinction.

Suppose the recursive resolver receives:
```text
google.com

The first lookup goes like this:

Recursive Resolver

↓

Root

↓

.com TLD

↓

Google Authoritative

↓

IP returned
```

Now it stores several things in its cache.

It might cache:
```text
google.com

↓

142.250.183.78
```
It may also cache:
```text
.com

↓

IP addresses of .com TLD servers
```
It can also cache referrals like:
```text
google.com

↓

Google Authoritative Name Server
```
---------------------------------------

So after one lookup, its cache could look like:

```text
-----------------------------------------
Recursive Resolver Cache
-----------------------------------------
google.com

↓

142.250.183.78

TTL: 250 sec

-----------------------------------------

.com

↓

a.gtld-servers.net
b.gtld-servers.net
...

TTL: 24 hours

-----------------------------------------

google.com

↓

ns1.google.com
ns2.google.com

TTL: 24 hours
Now another user asks for:
github.com

The resolver thinks:

Do I know where the .com TLD servers are?

↓

Yes.

↓

Skip the Root Server.

↓

Go directly to the .com TLD server.
```
So the lookup becomes:
```text
Recursive Resolver

↓

.com TLD

↓

GitHub Authoritative

↓

IP

```

Notice that the Root Server wasn't contacted.

Even Better

Suppose another user asks for: google.com

If this entry is still cached:

```text
google.com

↓

142.250.183.78
```
Then the resolver immediately returns:

```text
Cache

↓

Found

↓

Return IP
```

No Root Server.

No TLD Server.

No Authoritative Server.

Nothing else is contacted.

---

So does the recursive resolver "store recently given TLD IPs"?

Yes.

That's exactly what happens.

It caches:

The IP addresses (or names and resolved addresses) of TLD name servers.
Referrals to authoritative name servers.
Final DNS records (such as A or AAAA records).

As long as the cached information hasn't expired (its TTL hasn't run out), the recursive resolver can skip parts of the lookup process, making DNS much faster.

---
Complete Optimized Flow
First-ever lookup
```text
Client
   │
   ▼
Recursive Resolver
   │
   ▼
Root Server
   │
   ▼
.com TLD Server
   │
   ▼
Authoritative Server
   │
   ▼
IP Address
Later lookup for another .com domain
Client
   │
   ▼
Recursive Resolver
   │
   ▼
(Cache knows .com TLD servers)
   │
   ▼
.com TLD Server
   │
   ▼
Authoritative Server
   │
   ▼
IP Address
Later lookup for the same domain
Client
   │
   ▼
Recursive Resolver
   │
   ▼
(Cache contains google.com)
   │
   ▼
Return IP Immediately

```

---
# Recursive Resolver Cache

A Recursive Resolver also maintains its own DNS cache.

Example:

```text
Recursive Resolver Cache

------------------------------------------
google.com

↓

142.250.183.78

TTL: 250 sec

------------------------------------------

.com

↓

a.gtld-servers.net
b.gtld-servers.net

TTL: 24 hours

------------------------------------------

google.com

↓

ns1.google.com
ns2.google.com

TTL: 24 hours
```

It caches:

* Final IP addresses
* TLD server information
* Authoritative Name Server information

This allows future DNS lookups to skip unnecessary steps.

---

# Example Lookup

## First Lookup

```text
Client
   │
   ▼
Recursive Resolver
   │
   ▼
Root Server
   │
   ▼
.com TLD Server
   │
   ▼
Authoritative Server
   │
   ▼
IP Address
```

---

## Later Lookup for Another `.com` Domain

```text
Client
   │
   ▼
Recursive Resolver
   │
(Cache already knows .com TLD servers)
   │
   ▼
.com TLD Server
   │
   ▼
Authoritative Server
   │
   ▼
IP Address
```

The Root Server is skipped.

---

## Later Lookup for the Same Domain

```text
Client
   │
   ▼
Recursive Resolver
   │
(Cache contains google.com)
   │
   ▼
Return Cached IP
```

No Root, TLD, or Authoritative servers are contacted.

---

# Summary Table

| Component                | Purpose                                                                                   |
| ------------------------ | ----------------------------------------------------------------------------------------- |
| Browser DNS Cache        | Stores recently resolved domains for a single browser                                     |
| OS DNS Cache             | Shared DNS cache used by all applications                                                 |
| Hosts File               | Manual domain-to-IP mappings that override DNS                                            |
| Recursive Resolver Cache | Stores DNS records, TLD referrals, and authoritative referrals to speed up future lookups |

---

# Key Takeaways

* DNS lookups first check local sources before querying Internet DNS servers.
* Browsers maintain their own DNS caches for faster lookups.
* The operating system provides a shared DNS cache for all applications.
* The Hosts file is a manual mapping file, **not** a cache.
* Recursive DNS resolvers cache DNS information, including TLD and authoritative server referrals, to reduce lookup time.
* Caching at multiple layers makes DNS fast, efficient, and scalable.