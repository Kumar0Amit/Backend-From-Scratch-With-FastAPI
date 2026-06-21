# Domain Registrars

## Introduction

You've learned that domain names make the Internet easier for humans to use.

But a natural question arises:

> **Who decides who owns `google.com`?**

What stops someone else from registering the same name?

The answer lies in the domain registration system, which involves several organizations working together:

* Domain Registration
* ICANN
* Registry
* Registrar
* WHOIS

Think of it like buying land.

You don't simply declare, "This land is mine."

Instead:

1. A government defines the rules.
2. A land office keeps ownership records.
3. An authorized agent processes your purchase.
4. Ownership is officially recorded.

The domain name system works in a very similar way.

---

# 1. Domain Registration

A **domain name** is not automatically yours.

You must **register** it.

Domain registration is the process of reserving a unique domain name for a specific period (typically 1–10 years).

Example:

Suppose you want:

```text
myawesomeapp.com
```

You first check whether it's available.

If nobody owns it, you can register it.

After registration:

* You become the registrant (owner).
* Nobody else can register the same domain while your registration is active.
* You can renew it before it expires.

Think of it like registering a company name.

Only one business can legally own a specific registered name.

---

# Why Registration Exists

Imagine if registration didn't exist.

Today:

You create

```text
myshop.com
```

Tomorrow:

Someone else also creates

```text
myshop.com
```

Now the Internet wouldn't know where users should go.

Registration guarantees that every domain name is globally unique.

---

# 2. ICANN (Overview)

## What is ICANN?

**ICANN** stands for:

```text
Internet Corporation for Assigned Names and Numbers
```

ICANN is a **non-profit organization** responsible for coordinating the global Domain Name System (DNS).

Think of ICANN as the **manager of the Internet's naming system**.

It does **not** sell domain names directly.

Instead, it:

* Creates rules for domain names.
* Approves registries.
* Accredits registrars.
* Ensures every domain name remains globally unique.
* Coordinates IP address allocation and DNS root management.

---

## Real-World Analogy

Imagine a country.

The government does not personally sell every house.

Instead it:

* Creates property laws.
* Authorizes land offices.
* Ensures ownership records remain valid.

Similarly:

```text
ICANN
   │
Creates Rules
   │
Authorizes
   │
Registries & Registrars
```

---

# 3. Registry

A **Registry** maintains the official database for a specific Top-Level Domain (TLD).

Each TLD has its own registry.

Examples:

| TLD    | Registry                                   |
| ------ | ------------------------------------------ |
| `.com` | Verisign                                   |
| `.net` | Verisign                                   |
| `.org` | Public Interest Registry                   |
| `.in`  | National Internet Exchange of India (NIXI) |

The registry maintains the master list of all registered domains under its TLD.

For example, the `.com` registry stores records like:

```text
google.com
amazon.com
github.com
openai.com
```

The registry does **not** usually sell domains directly to customers.

Instead, it works with registrars.

---

## Registry Analogy

Imagine the Transport Department.

It maintains the official database of vehicle ownership.

However, you usually don't go directly to the central office.

Instead, you visit an authorized service center.

The Transport Department is like the **Registry**.

---

# 4. Registrar

A **Registrar** is a company authorized to sell and manage domain names on behalf of registries.

This is the company that customers interact with.

Examples of registrars include:

* GoDaddy
* Namecheap
* Porkbun
* Google Domains (service migrated to Squarespace)
* Dynadot

When you purchase:

```text
mywebsite.com
```

You buy it through a registrar.

The registrar then communicates with the registry to officially register the domain.

---

## Registration Flow

```text
You
 │
 ▼
Registrar
 │
 ▼
Registry
 │
 ▼
Domain Registered
```

---

## Real-World Analogy

Suppose you buy a car.

You don't usually visit the national transport headquarters.

Instead:

```text
You
 │
 ▼
Authorized Dealer
 │
 ▼
Transport Department
 │
 ▼
Ownership Recorded
```

Similarly:

```text
You
 │
 ▼
Registrar
 │
 ▼
Registry
 │
 ▼
Domain Ownership Recorded
```

---

# 5. WHOIS

After a domain is registered, information about that registration is stored in a public registration database known as **WHOIS**.

WHOIS allows people to view basic information about a domain.

Depending on privacy settings, it may include:

* Registrar
* Registration date
* Expiration date
* Name servers
* Domain status
* Registrant information (often hidden today using privacy protection)

---

## Example

Suppose someone owns:

```text
example.com
```

A WHOIS lookup might show:

```text
Domain:
example.com

Registrar:
Namecheap

Registered:
2024-01-15

Expires:
2029-01-15

Status:
Active

Name Servers:
ns1.exampledns.com
ns2.exampledns.com
```

Many registrars now enable **WHOIS Privacy Protection**, which hides personal details like the owner's name, email address, and phone number from public view.

---

# Complete Registration Process

Suppose you want:

```text
coolstartup.com
```

The process looks like this:

```text
Step 1
You search for:
coolstartup.com

        │
        ▼

Step 2
Registrar checks availability

        │
        ▼

Step 3
Registry confirms:
Available

        │
        ▼

Step 4
You pay the registration fee

        │
        ▼

Step 5
Registrar registers the domain with the Registry

        │
        ▼

Step 6
Registry updates its official database

        │
        ▼

Step 7
You become the registered owner
```

---

# How Everything Fits Together

```text
                    ICANN
                      │
      Creates Rules & Accredits
                      │
          ┌───────────┴───────────┐
          │                       │
     Registries             Registrars
          │                       │
     Maintain Database      Sell Domains
          │                       │
          └───────────┬───────────┘
                      │
                     You
                      │
              Register Domain
                      │
                 WHOIS Updated
```

---

# Summary Table

| Term                | Role                                                                              |
| ------------------- | --------------------------------------------------------------------------------- |
| Domain Registration | Reserving a unique domain name for a period of time                               |
| ICANN               | Coordinates the global DNS and accredits registrars and registries                |
| Registry            | Maintains the official database for a specific TLD                                |
| Registrar           | Company that sells and manages domain registrations                               |
| WHOIS               | Public registration database containing domain ownership and registration details |

---

# Key Takeaways

* A domain name must be **registered** before it can be used.
* **ICANN** coordinates the global domain name system but does not sell domains.
* A **Registry** maintains the official records for a specific TLD (such as `.com` or `.org`).
* A **Registrar** is the company from which you purchase and manage your domain name.
* **WHOIS** stores publicly available registration information about domains, although personal details are often hidden through privacy protection.
* Together, ICANN, registries, registrars, and WHOIS ensure that every domain name on the Internet is unique and properly managed.
