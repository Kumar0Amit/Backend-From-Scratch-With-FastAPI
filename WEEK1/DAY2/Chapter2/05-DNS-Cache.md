# 2.4 DNS Cache

## Introduction

Imagine if every time you visited:

```text id="yn6l8u"
google.com
```

your computer had to contact:

* Root Name Server
* TLD Name Server
* Authoritative Name Server

This would happen **for every single website visit**.

The Internet would become much slower, and DNS servers would receive billions of unnecessary requests.

To solve this problem, DNS uses **caching**.

A cache stores previously resolved DNS records for a limited amount of time so that future requests can be answered much faster.

---

# What is DNS Cache?

A **DNS Cache** is temporary storage that remembers previously resolved domain names and their corresponding IP addresses.

Example:

```text id="y5rzb2"
google.com

↓

142.250.183.78
```

Instead of asking DNS servers again, the cached result is returned immediately.

---

## Real-World Analogy

Suppose your friend asks:

> "What's Rahul's phone number?"

The first time, you search your contacts.

The second time, you already remember it.

Your memory acts as a **cache**.

DNS caching works exactly the same way.

---

# Why DNS Caching Exists

Without caching:

```text id="wm6fnd"
google.com

↓

Root

↓

TLD

↓

Authoritative

↓

IP
```

Every single visit.

With caching:

```text id="qef6qs"
google.com

↓

Cache

↓

IP
```

The lookup is almost instantaneous.

---

# Multiple Layers of DNS Cache

DNS doesn't have just one cache.

It has several caches working together.

```text id="s3s2qj"
Browser Cache

↓

Operating System Cache

↓

Router Cache

↓

ISP / Recursive Resolver Cache

↓

Root Server

↓

TLD Server

↓

Authoritative Server
```

Each layer reduces the amount of work required by the next layer.

---

# 1. Browser DNS Cache

Modern browsers maintain their own DNS cache.

Example:

```text id="c6mn4l"
Browser DNS Cache

------------------------------------------
Domain            IP Address       TTL
------------------------------------------
google.com        142.250.183.78   220 sec
github.com        140.82.121.4     180 sec
youtube.com       142.251.40.206    90 sec
------------------------------------------
```

When you revisit a website:

```text id="dhzaxd"
Browser

↓

Browser Cache

↓

Found

↓

Return IP
```

No request reaches the operating system.

---

## Advantages

* Fastest lookup.
* No OS interaction.
* No network traffic.

---

# View Browser DNS Cache

## Google Chrome

Older versions:

```text id="lfp6tw"
chrome://net-internals/#dns
```

Modern versions:

```text id="bnq3ec"
chrome://net-export/
```

> **Note:** Recent Chrome versions removed the old DNS cache page. Firefox still provides a DNS cache page, while Chrome relies more on OS networking tools.

---

## Firefox

```text id="z9h6j8"
about:networking#dns
```

---

# 2. Operating System DNS Cache

The operating system also stores DNS records.

Unlike the browser cache,

this cache is shared by all applications.

Example:

```text id="d8g1tx"
OS DNS Cache

------------------------------------------
Domain            IP Address      TTL
------------------------------------------
google.com        142.250.xxx.xxx
reddit.com        151.101.xxx.xxx
amazon.com        54.239.xxx.xxx
------------------------------------------
```

If Chrome misses,

Firefox,

VS Code,

Discord,

and every other application can still benefit from the OS cache.

---

## View Windows DNS Cache

```cmd id="dwp5qa"
ipconfig /displaydns
```

Clear cache:

```cmd id="22mjlwm"
ipconfig /flushdns
```

---

## Linux

Statistics:

```bash id="ukq06g"
resolvectl statistics
```

Flush:

```bash id="s6q2y0"
sudo resolvectl flush-caches
```

---

## macOS

Flush cache:

```bash id="ngc0os"
sudo dscacheutil -flushcache
sudo killall -HUP mDNSResponder
```

---

# 3. Router DNS Cache

Many home and office routers also maintain a DNS cache.

Example:

```text id="p8h17j"
Laptop

↓

Wi-Fi Router

↓

Router DNS Cache

↓

Found

↓

Return IP
```

Suppose:

* Your laptop visits `google.com`.
* Later your phone visits `google.com`.

The router may already know the answer.

This means the phone doesn't need to contact the ISP's DNS resolver.

---

## Example

```text id="z9tkrb"
Router Cache

-------------------------------------
google.com

↓

142.250.xxx.xxx

TTL: 180 sec
-------------------------------------
```

---

## Can You View Router Cache?

This depends on the router.

Business routers often expose DNS cache information.

Most consumer routers do **not**.

Some Linux-based routers allow:

```bash id="5qzuw0"
cat /var/cache/dnsmasq
```

or

```bash id="0fsrty"
journalctl -u dnsmasq
```

However, many home routers hide this information completely.

---

# 4. ISP / Recursive Resolver Cache

Your Internet Service Provider usually operates a **Recursive Resolver**.

This resolver serves thousands or even millions of users.

Example:

```text id="zv7t6m"
You

↓

ISP Recursive Resolver

↓

DNS Cache
```

Suppose:

Person A visits:

```text id="evlfpz"
github.com
```

The resolver performs a full lookup.

Five seconds later,

Person B visits:

```text id="uh4q2q"
github.com
```

The resolver already knows:

```text id="s50sop"
github.com

↓

140.82.xxx.xxx
```

No Root Server,

No TLD Server,

No Authoritative Server.

The cached result is returned immediately.

---

## ISP Cache Example

```text id="7cljgn"
ISP Cache

---------------------------------------
google.com

↓

142.250.xxx.xxx

TTL: 180 sec

---------------------------------------

.com

↓

TLD Server Information

TTL: 24 Hours

---------------------------------------

google.com

↓

Authoritative Server

TTL: 24 Hours
```

Notice that recursive resolvers cache more than just IP addresses.

They also cache:

* TLD referrals
* Authoritative server referrals

This makes future DNS lookups significantly faster.

---

# Cache Hierarchy

```text id="5hieix"
Browser Cache
        │
        ▼
Operating System Cache
        │
        ▼
Router Cache
        │
        ▼
ISP Recursive Resolver Cache
        │
        ▼
Root Server
        │
        ▼
TLD Server
        │
        ▼
Authoritative Server
```

The goal is to answer the query as early as possible.

---

# TTL (Time To Live)

Caches should not keep DNS records forever.

Suppose Google's IP address changes.

If caches never expired,

computers would continue using the old IP address forever.

To solve this,

every DNS record has a **TTL**.

TTL stands for:

```text id="6aj3wn"
Time To Live
```

TTL tells a cache:

> **"You may keep this record for this amount of time."**

---

## Example

Suppose a DNS record is:

```text id="0gnlr9"
google.com

↓

142.250.xxx.xxx

TTL = 300 seconds
```

Timeline:

```text id="izybzs"
0 sec

↓

DNS Record Cached

↓

60 sec

↓

Still Valid

↓

120 sec

↓

Still Valid

↓

300 sec

↓

TTL Expires

↓

Delete Cache

↓

Next Request Performs New DNS Lookup
```

---

# Why TTL Matters

Imagine Google moves its website to a new IP.

Old:

```text id="jlwmc3"
142.250.183.78
```

New:

```text id="slaz2u"
34.117.xxx.xxx
```

Because of TTL,

all caches eventually expire and retrieve the updated IP address.

Without TTL,

many users would continue connecting to outdated servers.

---

# Short TTL vs Long TTL

## Short TTL

Example:

```text id="jlwmh7"
TTL = 60 seconds
```

Advantages:

* Changes propagate quickly.
* Useful during server migrations.

Disadvantages:

* More DNS lookups.
* Higher DNS server load.

---

## Long TTL

Example:

```text id="8f5bde"
TTL = 24 hours
```

Advantages:

* Fewer DNS queries.
* Faster browsing.
* Reduced DNS traffic.

Disadvantages:

* Changes take longer to propagate.

---

# Complete Example

Suppose you visit:

```text id="kslfgv"
github.com
```

The lookup proceeds like this:

```text id="mfxh72"
Browser Cache

↓

Miss

↓

OS Cache

↓

Miss

↓

Router Cache

↓

Miss

↓

ISP Cache

↓

Miss

↓

Root Server

↓

.com TLD

↓

GitHub Authoritative Server

↓

140.82.xxx.xxx

↓

Store in ISP Cache

↓

Store in Router Cache

↓

Store in OS Cache

↓

Store in Browser Cache

↓

Return IP
```

The **next request** is likely answered by the browser or OS without any network communication.

---

# Summary Table

| Cache Layer                    | Purpose                                                                       |
| ------------------------------ | ----------------------------------------------------------------------------- |
| Browser Cache                  | Stores DNS records for a single browser                                       |
| Operating System Cache         | Shared cache for all applications on the device                               |
| Router Cache                   | Shared cache for devices connected to the same router                         |
| ISP / Recursive Resolver Cache | Shared cache for many users of the same DNS resolver                          |
| TTL                            | Specifies how long a DNS record may remain cached before it must be refreshed |

---

# Key Takeaways

* DNS caching significantly reduces lookup time and Internet traffic.
* DNS records can be cached at multiple layers: **Browser**, **Operating System**, **Router**, and **ISP Recursive Resolver**.
* Each layer attempts to answer the query before contacting the next layer.
* Recursive resolvers cache not only IP addresses but also **TLD** and **Authoritative Server** referrals.
* **TTL (Time To Live)** determines how long a cached DNS record remains valid.
* After the TTL expires, the next DNS lookup retrieves fresh information from the DNS hierarchy.
