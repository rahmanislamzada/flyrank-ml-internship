# Phase: Build (Core) — Personal Infrastructure & DNS Walkthrough (PF-04)

---

## 1. Live Infrastructure & Hosting Setup

* **Primary Production URL:** [https://rahmanislamzada.github.io/flyrank-ml-internship/](https://rahmanislamzada.github.io/flyrank-ml-internship/)
* **Alternative Hosting Setup:** Netlify Deployment ([https://rahmanislamzada.netlify.app](https://rahmanislamzada.netlify.app))
* **Protocol & Security:** SSL/TLS Certificate Active (Enforced HTTPS with Padlock).
* **Integrations Included:** Working external anchor links to LinkedIn Profile, GitHub Repository, ML Data Engineering CV, and Direct Booking Link.

---

## 2. Plain-English DNS Walkthrough (How the Web Finds Your Site)

When a user opens a browser and types a web address like rahmanislamzada.flyrank.ai, a multi-step background discovery process occurs behind the scenes in milliseconds:

[User Browser]
      │  1. Requests "rahmanislamzada.flyrank.ai"
      ▼
[DNS Recursive Resolver] ──(Checks Cache)──► Found? Returns IP instantly
      │  2. Not in cache? Queries Root & TLD (.ai)
      ▼
[Authoritative Nameserver]
      │  3. Looks up CNAME Record for "rahmanislamzada"
      ▼
[Canonical Alias Response] ──► Points to: "rahmanislamzada.github.io"
      │  4. Resolves Final Target Server IP
      ▼
[GitHub Pages / Host Server] ──(Serves HTML over HTTPS)──► [User Screen]

---

## 3. Core Concepts Explained

### 1. What is a CNAME Record?
A **CNAME (Canonical Name) Record** is an alias in the DNS directory. Instead of mapping a domain name directly to a numeric IP address (which an **A Record** does), a CNAME maps one domain alias to another domain name. 

* *Analogy:* An A record is like listing someone's physical home address. A CNAME record is like saying "Rahman's office is located wherever FlyRank HQ is."

### 2. Capstone Subdomain Configuration Plan
When the `rahmanislamzada.flyrank.ai` subdomain is provisioned at capstone approval:

* **Record Type:** `CNAME`
* **Host / Subdomain Name:** `rahmanislamzada`
* **Target Value:** `rahmanislamzada.github.io` (or `rahmanislamzada.netlify.app`)

---

## 4. Four-Step Resolution Lifecycle

1. **The Request (Browser & Resolver):** The browser asks the ISP's **Recursive Resolver**: *"Where is `rahmanislamzada.flyrank.ai`?"*
2. **The Referral Chain (Root & TLD):** The Resolver asks the Top-Level Domain (`.ai`) nameservers to locate the authoritative server responsible for `flyrank.ai`.
3. **The Alias Lookup (Authoritative Server):** The `flyrank.ai` Authoritative Nameserver inspects its DNS zone file, finds the CNAME record for `rahmanislamzada`, and responds: *"That address is an alias pointing to `rahmanislamzada.github.io`."*
4. **The Final Response & Handshake:** The Resolver gets the destination IP from the host server, returns it to the browser, and the browser establishes a secure encrypted HTTPS connection to deliver the webpage.
