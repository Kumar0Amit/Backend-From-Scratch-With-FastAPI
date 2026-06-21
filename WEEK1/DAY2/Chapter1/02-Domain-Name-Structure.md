# Domain Name Structure

## Introduction

A domain name is not just a random string of words. It has a **hierarchical structure**, where each part has a specific purpose.

Consider the following domain:

```text
blog.shop.example.com
```

Each section of the domain represents a different level in the hierarchy.

```text
blog.shop.example.com.
 │     │      │       │
 │     │      │       └── Root Domain (.)
 │     │      └────────── Top-Level Domain (com)
 │     └───────────────── Second-Level Domain (example)
 └─────────────────────── Subdomains (shop, blog)
```

The Internet reads domain names **from right to left**, moving from the most general level to the most specific.

---

# 1. Root Domain

The **Root Domain** is the highest level in the Domain Name System (DNS) hierarchy.

It is represented by a single **dot (`.`)**.

```text
.
```

Every domain name technically ends with this dot.

For example:

```text
google.com.
```

Notice the dot at the end.

Most browsers hide this trailing dot because it is implied.

Therefore, when you type:

```text
google.com
```

the browser actually interprets it as:

```text
google.com.
```

The root domain is managed by the DNS root servers, which know where every Top-Level Domain (TLD) is located.

---

# 2. Top-Level Domain (TLD)

The **Top-Level Domain (TLD)** is the highest visible part of a domain name.

Examples:

```text
.com
.org
.net
.edu
.gov
.in
.uk
.ai
```

In:

```text
google.com
```

```text
google . com
         ▲
         │
       TLD
```

The TLD tells the DNS system which registry is responsible for that domain.

### Common TLD Categories

| TLD    | Purpose                                               |
| ------ | ----------------------------------------------------- |
| `.com` | Commercial businesses (now general purpose)           |
| `.org` | Organizations                                         |
| `.net` | Network-related services (originally)                 |
| `.edu` | Educational institutions                              |
| `.gov` | Government organizations                              |
| `.mil` | Military organizations                                |
| `.in`  | India (Country Code TLD)                              |
| `.uk`  | United Kingdom                                        |
| `.jp`  | Japan                                                 |
| `.ai`  | Originally Anguilla, now widely used for AI companies |

---

# 3. Second-Level Domain (SLD)

The **Second-Level Domain (SLD)** is the name chosen by the organization, company, or individual.

Example:

```text
google.com
```

```text
google . com
   ▲
   │
  SLD
```

Here:

* **google** is the Second-Level Domain.
* **com** is the Top-Level Domain.

More examples:

```text
amazon.com
github.com
microsoft.com
openai.com
```

The SLD is usually the brand or company name.

---

# 4. Subdomain

A **subdomain** is an additional prefix added before the Second-Level Domain.

Example:

```text
mail.google.com
```

```text
mail . google . com
 ▲        ▲       ▲
 │        │       │
Subdomain SLD     TLD
```

Here:

* **mail** → Subdomain
* **google** → Second-Level Domain
* **com** → Top-Level Domain

Another example:

```text
blog.shop.example.com
```

```text
blog . shop . example . com
 ▲      ▲        ▲       ▲
 │      │        │       │
Sub    Sub      SLD     TLD
```

There can be multiple levels of subdomains.

Examples:

```text
api.example.com
dev.example.com
mail.example.com
docs.python.org
support.microsoft.com
```

Subdomains are often used to separate different services within the same organization.

For example:

| Subdomain          | Purpose      |
| ------------------ | ------------ |
| `mail.google.com`  | Gmail        |
| `maps.google.com`  | Google Maps  |
| `drive.google.com` | Google Drive |
| `docs.google.com`  | Google Docs  |
| `api.example.com`  | Backend API  |
| `blog.example.com` | Blog         |

---

# 5. Fully Qualified Domain Name (FQDN)

A **Fully Qualified Domain Name (FQDN)** specifies the **complete and exact location** of a host within the DNS hierarchy.

It includes:

* Hostname (optional in casual usage but required for a specific host)
* All subdomains
* Second-Level Domain
* Top-Level Domain
* Root Domain (`.`)

Example:

```text
mail.google.com.
```

Breakdown:

```text
mail . google . com .
 │        │       │   │
 │        │       │   └── Root Domain
 │        │       └────── Top-Level Domain
 │        └────────────── Second-Level Domain
 └─────────────────────── Host/Subdomain
```

Another example:

```text
api.dev.example.com.
```

This represents one exact host in the global DNS namespace.

The trailing dot indicates that the name is absolute and should not be appended to any local search domain.

In everyday browsing, browsers usually omit the trailing dot.

---

# Reading a Domain from Right to Left

DNS processes domain names from **right to left**.

Consider:

```text
blog.shop.example.com
```

The lookup proceeds like this:

```text
.
│
▼
Root Domain

▼
com
(Top-Level Domain)

▼
example
(Second-Level Domain)

▼
shop
(Subdomain)

▼
blog
(Subdomain / Host)
```

Each DNS server only knows about the level directly beneath it and refers the request to the next appropriate server until the final destination is reached.

---

# Visual Hierarchy

```text
Root (.)
│
└── com
    │
    └── google
        │
        ├── mail
        ├── docs
        ├── maps
        ├── drive
        └── photos
```

Another example:

```text
Root (.)
│
└── org
    │
    └── python
        │
        ├── docs
        ├── wiki
        └── peps
```

---

# Summary Table

| Component                          | Example               | Description                               |
| ---------------------------------- | --------------------- | ----------------------------------------- |
| Root Domain                        | `.`                   | Highest level of the DNS hierarchy        |
| Top-Level Domain (TLD)             | `com`                 | Highest visible part of a domain          |
| Second-Level Domain (SLD)          | `google`              | Name chosen by the organization           |
| Subdomain                          | `mail`, `docs`, `api` | Divides services within a domain          |
| Fully Qualified Domain Name (FQDN) | `mail.google.com.`    | Complete domain name ending with the root |

---

# Key Takeaways

* Every domain name follows a hierarchical structure.
* The **Root Domain (`.`)** sits at the top of the DNS hierarchy.
* The **Top-Level Domain (TLD)** identifies the registry (e.g., `.com`, `.org`, `.in`).
* The **Second-Level Domain (SLD)** is the unique name registered by an organization.
* **Subdomains** organize different services under the same domain.
* An **FQDN** represents the complete domain name, including the root domain.
* DNS resolves domain names **from right to left**, starting at the root and moving toward the specific host.
