# Module 2 – Footprinting with GHDB (Google Hacking Database)

**Internship:** [Networkwalks]
**Intern:** [Awais Sajjad]
**Week:** 2

> Performed for educational purposes only. Live camera links found during
> this exercise are not published here to protect the privacy of their
> owners — only the dorks used are shared. Full results were submitted
> privately to my supervisor.

## Objective
Use Google dorks (GHDB and manual dorking) to discover two categories of
publicly exposed resources:
1. Live, internet-accessible security cameras
2. Downloadable mathematics eBooks in PDF format

## Tools / Resources
- Google Hacking Database — exploit-db.com/google-hacking-database
- Manual Google dork construction (search term: `cam`)

---

## Task 1: Exposed Security Cameras

**Search term used on GHDB:** `cam`

Found 10 live, internet-exposed camera interfaces using a mix of GHDB
entries and manually constructed dorks. Links and credentials are withheld
from this public README; only the dork pattern is listed below.

| No. | Relevant Dork | Notes |
|-----|----------------|-------|
| 1 | `intitle:"Webcam" inurl:WebCam.htm` | Camera panel accessible, no login required |
| 2 | `intext:"Real-time IP Camera Monitoring System"` | Default credentials (admin/admin) worked |
| 3 | `intext:"Real-time IP Camera Monitoring System"` | Default credentials (admin/admin) worked |
| 4 | `intitle:"webcamXP" inurl:8080` | Camera panel accessible, no login required |
| 5 | `intitle:"webcamXP" inurl:8080` | Multi-camera view accessible |
| 6 | `intitle:"webcamXP 5" inurl:admin.html` | Mobile-view panel accessible |
| 7 | `inurl:/multi.html intitle:webcam` | Multi-camera view accessible |
| 8 | `intitle:"webcamxp 5" intext:"live stream"` | Live stream accessible |
| 9 | `inurl:/ViewerFrame? intitle:"Network Camera NetworkCamera"` | Panasonic-style network camera viewer |
| 10 | `Display Cameras intitle:"Express6 Live Image"` | Live camera image feed accessible |

**Findings:**
Several of these cameras (#2, #3) were still using the vendor **default
credentials (admin/admin)**, meaning anyone could not just view but
potentially control the camera (pan/tilt/zoom, settings). The rest required
no authentication at all to view the live feed.

**Mitigation Notes:**
- Never leave default manufacturer credentials in place.
- Don't expose camera admin/viewer interfaces directly to the internet —
  place them behind a VPN or firewall.
- Disable features (like `ViewerFrame`, `CgiStart`) that allow anonymous
  remote viewing.

---

## Task 2: Mathematics eBooks (PDF)

**Dork used (primary):** `intitle:index.of "parent directory" mathematics pdf`
Variants used to reach 10 results: adding `free`, `free download`, and
`book` to the dork when the primary query returned duplicates.

| No. | Link | Dork Used |
|-----|------|-----------|
| 1 | [education.giakonda.org.uk/Maths/math7.pdf](https://education.giakonda.org.uk/Maths/math7.pdf) | `intitle:index.of "parent directory" mathematics pdf` |
| 2 | [erewhon.superkuh.com – A Mathematician's Apology](http://erewhon.superkuh.com/library/Math/A%20Mathematicians%20Apology_%20Godfrey%20H%20Hardy.pdf) | `intitle:index.of "parent directory" mathematics pdf` |
| 3 | [unm.edu/~megrad/Math/Mathematics-2017.pdf](https://www.unm.edu/~megrad/Math/Mathematics-2017.pdf) | `intitle:index.of "parent directory" mathematics pdf` |
| 4 | [ochicken.net – Matrix Mathematics](https://ochicken.net/library/Mathematics/Linear_Algebra/Matrix%20Mathematics%3A%20Theory%2C%20Facts%2C%20and%20Formulas%20with%20Application%20to%20Linear%20Systems%20Theory.pdf) | `intitle:index.of "parent directory" mathematics pdf` |
| 5 | [amsi.org.au – Addition and Subtraction](https://amsi.org.au/teacher_modules/pdfs/Addition_and_subtraction.pdf) | `intitle:index.of "parent directory" mathematics pdf free download` |
| 6 | [zaco.au – Cambridge Maths Ext 1 Yr 12](https://zaco.au/lib/math/hs/dokumen.pub_cambridgemaths-stage-6-mathematics-extension-1-year-12-9781108766302.pdf) | `intitle:index.of "parent directory" mathematics pdf free` |
| 7 | [zaco.au – Cambridge Maths Ext 1 Yr 11](https://zaco.au/lib/math/hs/dokumen.pub_cambridgemaths-stage-6-mathematics-extension-1-year-11-9781108469074.pdf) | `intitle:index.of "parent directory" mathematics pdf free` |
| 8 | [education.giakonda.org.uk – Additional Mathematics](https://education.giakonda.org.uk/Maths/Additional_Mathematics__Pure_and_Applied.pdf) | `intitle:index.of "parent directory" mathematics book pdf maths` |
| 9 | [math.fsu.edu – Yuma 42 Yearbook](https://www.math.fsu.edu/~bellenot/past/yuma42yearbook.pdf) | `intitle:index.of "parent directory" mathematics pdf free` |
| 10 | [jsoftware.com – aioj.pdf](https://www.jsoftware.com/books/pdf/aioj.pdf) | `intitle:index.of "parent directory" mathematics book pdf maths` |

**Findings:**
These results came from web servers with **directory listing (indexing)
enabled**, which exposes the full folder structure instead of just a
single intended page — letting anyone browse and download every file in
that directory, not just the PDF that was linked publicly.

**Mitigation Notes:**
- Disable directory listing (`Options -Indexes` in Apache, or equivalent in nginx/IIS).
- Keep course/library material behind authentication if it isn't meant to be public.

---

## Summary
This module showed how a single search engine query, with no hacking or
exploitation involved, can expose live camera feeds with default
credentials and entire directories of files that were never meant to be
publicly browsable. Both issues stem from basic misconfigurations
(default credentials, directory indexing left on) rather than software
vulnerabilities — meaning they're easy to find and just as easy to fix.

## Key Takeaway
GHDB-style dorking is entirely passive (no packets sent to the target
beyond what a normal browser visit would send) yet reveals serious
exposure. Organizations should regularly dork their own domains to catch
these misconfigurations before attackers do.
