# Module 1 – Footprinting with Multiple Tools

**Internship:** [Networkwalks-Cybersecurity]
**Intern:** [Awais Sajjad]
**Week:** 2

> Performed for educational purposes on an authorized/test domain.

## Objective
Gather reconnaissance information about a target domain using six different
footprinting tools, each revealing a different type of information
(registration data, web technology, DNS records, HTTP headers, and WAF
presence).

## Target
**Domain used:** [example.com]

## Tools & Tasks

| # | Task | Tool | Purpose |
|---|------|------|---------|
| 1 | Domain registration lookup | `whois` | Registrar, owner, creation/expiry dates, name servers |
| 2 | Web technology fingerprinting | `whatweb` | CMS, server, frameworks, plugins in use |
| 3 | DNS resolution | `nslookup` | Resolve domain to IP address |
| 4 | HTTP header inspection | `curl -I` | Server banner, status code, security headers |
| 5 | WAF detection | `wafw00f` | Identify if a Web Application Firewall is protecting the site |
| 6 | Full DNS enumeration | `dnsrecon` | A, MX, NS, TXT, SOA records and possible subdomains |

---

## Task 1: WHOIS Lookup
**Command:**
```bash
whois example.com
```
**Screenshot:**
![whois output](screenshots/01-whois.png)

**Raw output:** [`outputs/whois.txt`](outputs/whois.txt)

**Findings:**
- Registrar: [name]
- Creation date: [date]
- Expiry date: [date]
- Name servers: [list]

---

## Task 2: WhatWeb Fingerprinting
**Command:**
```bash
whatweb example.com
```
**Screenshot:**
![whatweb output](screenshots/02-whatweb.png)

**Raw output:** [`outputs/whatweb.txt`](outputs/whatweb.txt)

**Findings:**
- Web server: [e.g. nginx/Apache + version]
- Technologies detected: [e.g. WordPress, PHP, jQuery]
- Country/IP info (if shown): [details]

---

## Task 3: nslookup DNS Resolution
**Command:**
```bash
nslookup example.com
```
**Screenshot:**
![nslookup output](screenshots/03-nslookup.png)

**Raw output:** [`outputs/nslookup.txt`](outputs/nslookup.txt)

**Findings:**
- Resolved IP address: [IP]
- DNS server used: [resolver IP/name]

---

## Task 4: HTTP Response Headers
**Command:**
```bash
curl -I http://example.com
```
**Screenshot:**
![curl headers output](screenshots/04-curl-headers.png)

**Raw output:** [`outputs/curl-headers.txt`](outputs/curl-headers.txt)

**Findings:**
- HTTP status code: [e.g. 200 OK]
- Server header: [e.g. nginx]
- Security headers present: [e.g. X-Frame-Options, HSTS]
- Security headers missing: [list any, if relevant]

---

## Task 5: WAF Detection
**Command:**
```bash
wafw00f http://example.com
```
**Screenshot:**
![wafw00f output](screenshots/05-wafw00f.png)

**Raw output:** [`outputs/wafw00f.txt`](outputs/wafw00f.txt)

**Findings:**
- WAF detected: [Yes/No]
- WAF vendor (if any): [e.g. Cloudflare, Akamai]

---

## Task 6: DNS Enumeration
**Command:**
```bash
dnsrecon -d example.com
```
**Screenshot:**
![dnsrecon output](screenshots/06-dnsrecon.png)

**Raw output:** [`outputs/dnsrecon.txt`](outputs/dnsrecon.txt)


---


## Key Takeaway
Footprinting tools each expose a different slice of a target's public
footprint; combining them builds a far more complete picture than any
single tool alone, and highlights what information organizations
unintentionally expose (DNS records, server banners, missing security
headers) that defenders should review and harden.
