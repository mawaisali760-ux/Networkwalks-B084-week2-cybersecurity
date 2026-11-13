# Module 3 – Footprinting with Maltego

**Internship:** [Networkwalks]
**Intern:** [Awais Sajjad]
**Week:** 2

> Performed for educational purposes only, on the target domain
> networkwalks.com, with permission as specified in the task.

## Objective
Install Maltego and use it to discover email addresses associated with
the target organization domain **networkwalks.com**.

## Task 1: Install Maltego

**Note on environment:** The task specified installing Maltego on a
Windows computer. Since Maltego comes **pre-installed on Kali Linux**, I
performed this task on Kali instead of a separate Windows install, using
the pre-installed version (Maltego Graph Desktop v4.13.0).

**Launch command (Kali):**
```bash
maltego
```

**Screenshot — Maltego launched, before starting the task:**
![Maltego before task](screenshots/01-maltego-before.png)

The interface opened successfully with an empty **Run View**, confirming
the installation was working and ready to run transforms.

---

## Task 2: Find Email Addresses for networkwalks.com

**Steps performed:**
1. Created a new graph.
2. Added a **Domain** entity and set its value to `networkwalks.com`.
3. Right-clicked the entity → **Run Transform → To Email Addresses [Search Engine]**.
4. Reviewed the resulting graph for discovered email entities.

**Screenshot — after running the transform:**
![Maltego after task](screenshots/02-maltego-after.png)

**Transform log (from Output panel):**
INFO Running transform [Utilities] To Email Addresses [Search Engine] on 1 entities
INFO --- [ Unified Credits ] --- : You have consumed 10 credits. You have 190 credits remaining.
INFO Transform [Utilities] To Email Addresses [Search Engine] completed in 15s 274ms


**Findings:**

| # | Email Found | Source Transform |
|---|-------------|-------------------|
| 1 | info@networkwalks.com | To Email Addresses [Search Engine] |

Only one public email address (`info@networkwalks.com`) was returned by
this transform. Additional transforms (e.g. `To Email Addresses [PGP]`,
`To Email Addresses [whois]`, or running multiple search-engine-based
transforms in sequence) could be chained to try to surface more results,
but a single general-contact email is a common outcome for smaller
organizations that don't expose individual staff emails publicly.

## Summary
Maltego's graph-based approach made it quick to go from a single domain
entity to a confirmed, linked email address in one transform. It's
especially useful when you want to visually map relationships between
multiple pieces of information (domains, emails, people, infrastructure)
rather than just getting a flat list, which is where it differs from
command-line tools like theHarvester.

## Key Takeaway
Even organizations with a minimal public footprint will usually expose at
least one general contact email, which becomes the starting point an
attacker could use for phishing or social engineering — reinforcing why
businesses should be deliberate about what contact information they
publish and where.
