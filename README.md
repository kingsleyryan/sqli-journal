# SQLi Journal — TryHackMe Lab Notes

**Author:** Uzodinma Kingsley Chibugom (Hexaking)  
**Record date:** 2025-09-24

A concise, reproducible lab journal documenting SQL injection techniques practiced on TryHackMe. This repository contains step-by-step writeups for four SQLi lab types (Error-Based, Blind, Boolean Blind, Time-Based), the exact payloads used (where appropriate), recovered artifacts, and screenshots for each level. All testing was performed in a controlled, authorized lab environment.

---

## Table of contents
- [About](#about)  
- [Repository structure](#repository-structure)  
- [Quick flags summary](#quick-flags-summary)  
- [Per-level writeups](#per-level-writeups)  
- [Screenshots & file naming conventions](#screenshots--file-naming-conventions)  
- [How to update / push changes (PowerShell)](#how-to-update--push-changes-powershell)  
- [Safety & legal notice](#safety--legal-notice)  
- [Contributing & contact](#contributing--contact)

---

## About
This journal documents methodology and learning for personal study and portfolio use. It captures payloads used in controlled labs, the enumeration and exploitation process, recovered artifacts (flags, sample credentials where permitted), and lessons learned. Use this repository for study and demonstration purposes only — **do not** apply these techniques to unauthorized systems.

---

## Repository structure
sqli-journal/
├─ level1.md # Error-Based SQLi writeup
├─ level2.md # Blind SQLi writeup
├─ level3.md # Boolean Blind SQLi writeup
├─ level4.md # Time-Based Blind SQLi writeup
└─ sqli-screenshots/
├─ level1/
├─ level2/
├─ level3/
└─ level4/


---

## Quick flags summary
| Level | Type | Flag |
|-------|------|------|
| Level 1 | Error-Based SQLi | `THM{SQL_INJECTION_3840}` |
| Level 2 | Blind SQLi       | `THM{SQL_INJECTION_9581}` |
| Level 3 | Boolean Blind SQLi | `THM{SQL_INJECTION_1093}` |
| Level 4 | Time-Based Blind SQLi | `THM{SQL_INJECTION_MASTER}` |

> Full payloads, results and notes are recorded in each level’s markdown file.

---

## Per-level writeups
Open the markdown files for full details (payloads, step-by-step notes, screenshots, and lessons learned):

- `level1.md` — Error-Based SQLi (UNION + error leakage).  
- `level2.md` — Blind SQLi (authentication bypass with `' OR 1=1;--`).  
- `level3.md` — Boolean-Based Blind SQLi (information_schema enumeration).  
- `level4.md` — Time-Based Blind SQLi (character-by-character enumeration with `SLEEP()`).

---

## Screenshots & file naming conventions
Screenshots are referenced using relative links so GitHub preview renders them.

**Folder layout (relative to repo root)**
./sqli-screenshots/
level1/2025-09-24-Error-Based-SQLi.png
level2/2025-09-24-Blind-SQLi.png
level3/2025-09-24-Boolean-Blind-SQLi.png
level4/2025-09-24-Time-Based-Blind-SQLi.png