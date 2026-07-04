# Project 2 — Web Application Penetration Testing (OWASP Top 10 Focus)

![Status](https://img.shields.io/badge/Status-All%20Completed-green)
![Week](https://img.shields.io/badge/Week:1,2,3,4%20-Completed-green)
![Organization](https://img.shields.io/badge/Organization-Zaalima%20Development%20Pvt%20Ltd-blue)

---

## 🏢 Internship Details

| Field | Details |
|---|---|
| **Organization** | Zaalima Development Pvt Ltd |
| **Internship Mode** | Online |
| **Duration** | 3 Months |
| **Project** | Project 2 — Web Application Penetration Testing (OWASP Top 10 Focus) |
| **Week** | Week 1 |
| **Date** | 20.05.2026 |

---

## 👥 Team

| Name | Role | GitHub |
|---|---|---|
| Sruthi Rajeshkumar | Team Lead | @sruthi37 |
| Abhinaya | Member | @Abhinaya-329 |
| MD Abdulla | Member | @Abdulla-08 |
| Sudarshan Yadav | Member | @bsudarshan868-netizen |

---

## 🎯 Week 1 Objective

Study the OWASP Top 10:2025 vulnerabilities, set up the penetration testing environment (DVWA & OWASP Juice Shop), and perform basic reconnaissance using Burp Suite Community Edition.

---

## 🛠️ Tools & Technologies Used

| Tool | Version | Purpose |
|---|---|---|
| Kali Linux | Latest | Primary penetration testing OS |
| Docker | 28.5.2 | Container platform |
| DVWA | 1.10 | Vulnerable web app — localhost:8080 |
| OWASP Juice Shop | Latest | Vulnerable web app — localhost:3000 |
| Burp Suite | Community v2023.5.4 | Proxy & reconnaissance |
| Firefox | 102.0 | Browser with proxy configuration |

---

# 📋 Week 1 Tasks

### ✅ Task 1 — OWASP Top 10:2025 Study
| Field | Details |
|---|---|
| **Reference** | https://owasp.org/Top10/2025/ |
| **Status** | ✅ Completed |
| **Documentation** | [View Notes](Week-1/Task-1-OWASP-Top10-Notes/notes.md) |

**Vulnerabilities Studied:**
| ID | Vulnerability |
|---|---|
| A01 | Broken Access Control |
| A02 | Security Misconfiguration |
| A03 | Software Supply Chain Failures |
| A04 | Cryptographic Failures |
| A05 | Injection |
| A06 | Insecure Design |
| A07 | Authentication Failures |
| A08 | Software or Data Integrity Failures |
| A09 | Security Logging and Alerting Failures |
| A10 | Mishandling of Exceptional Conditions |

---

### ✅ Task 2 — Test Environment Setup
| Field | Details |
|---|---|
| **Status** | ✅ Completed |
| **Documentation** | [View Setup Notes](Week-1/Task-2-Environment-Setup/setup-notes.md) |

**Environment Summary:**
| Application | URL | Status |
|---|---|---|
| DVWA | http://localhost:8080 | ✅ Running |
| OWASP Juice Shop | http://localhost:3000 | ✅ Running |

---

### ✅ Task 3 — Burp Suite Reconnaissance & Spidering
| Field | Details |
|---|---|
| **Status** | ✅ Completed |
| **Target** | OWASP Juice Shop (http://localhost:3000) |
| **Documentation** | [View Recon Notes](Week-1/Task-3-Burp-Suite-Recon/recon-notes.md) |

**Key Endpoints Discovered:**
| Endpoint | Method | Type |
|---|---|---|
| /rest/products/search | GET | JSON API |
| /rest/admin/application-configuration | GET | JSON API |
| /api/Challenges/ | GET | JSON API |
| /socket.io/ | GET | WebSocket |
| /main.js | GET | Script |

---

## 📁 Repository Structure

```
📁 Web-Application-Penetration-Testing-OWASP-Top10/
│
└── 📁 Week-1/
    │
    ├── 📁 Task-1-OWASP-Top10-Notes/
    │   ├── 📄 notes.md
    │   └── 📁 screenshots/
    │       ├── 🖼️ owasp-homepage.png
    │       ├── 🖼️ a01-broken-access-control.png
    │       ├── 🖼️ a05-injection.png
    │       ├── 🖼️ a07-authentication-failures.png
    │
    ├── 📁 Task-2-Environment-Setup/
    │   ├── 📄 setup-notes.md
    │   └── 📁 screenshots/
    │       ├── 🖼️ docker-ps.png
    │       ├── 🖼️ dvwa-setup-page.png
    │       ├── 🖼️ dvwa-database-reset.png
    │       ├── 🖼️ dvwa-dashboard.png
    │       └── 🖼️ juice-shop-running.png
    │
    └── 📁 Task-3-Burp-Suite-Recon/
        ├── 📄 recon-notes.md
        └── 📁 screenshots/
            ├── 🖼️ burp-suite-dashboard.png
            ├── 🖼️ proxy-settings.png
            ├── 🖼️ firefox-proxy-config.png
            ├── 🖼️ intercept-live-request.png
            └── 🖼️ site-map-endpoints.png
            └── 🖼️ site Map localhost discovered
            └── 🖼️ site Map endpoints expanded

```

---

## ✅ Week 1 Completion Status

| Task | Description | Team Status |
|---|---|---|
| Task 1 | OWASP Top 10:2025 Study Notes | ✅ All Members Completed |
| Task 2 | DVWA & Juice Shop Environment Setup | ✅ All Members Completed |
| Task 3 | Burp Suite Reconnaissance & Spidering | ✅ All Members Completed |

---

## 📸 Screenshots Summary

| Task | Screenshots | Status |
|---|---|---|
| Task 1 — OWASP Study | 4 screenshots | ✅ Uploaded |
| Task 2 — Environment Setup | 5 screenshots | ✅ Uploaded |
| Task 3 — Burp Suite Recon | 7 screenshots | ✅ Uploaded |

---

---

# ✅ Week 2 — Completed
| Task | Description | Platform | Status |
|---|---|---|---|
| Task 1 | SQL Injection Testing | DVWA | ✅ Done |
| Task 2 | Broken Authentication Testing | DVWA + Juice Shop | ✅ Done |
| Task 3 | XSS + Sensitive Data Exposure | DVWA | ✅ Done |

---

## 🔍 Vulnerabilities Found — Week 2

| # | Vulnerability | Platform | Severity | Status |
|---|---|---|---|---|
| 1 | SQL Injection — Error Based | DVWA | 🔴 Critical | ✅ Confirmed |
| 2 | SQL Injection — Boolean Based | DVWA | 🔴 Critical | ✅ Confirmed |
| 3 | SQL Injection — UNION Based | DVWA | 🔴 Critical | ✅ Confirmed |
| 4 | No Account Lockout | DVWA | 🔴 High | ✅ Confirmed |
| 5 | Weak Password Policy | DVWA | 🔴 High | ✅ Confirmed |
| 6 | Credentials in Plain Text URL | DVWA | 🔴 High | ✅ Confirmed |
| 7 | SQLi Authentication Bypass | Juice Shop | 🔴 Critical | ✅ Confirmed |
| 8 | XSS Reflected | DVWA | 🔴 High | ✅ Confirmed |
| 9 | XSS Stored | DVWA | 🔴 Critical | ✅ Confirmed |
| 10 | Sensitive Data Exposure | DVWA | 🔴 High | ✅ Confirmed |

---

## 📊 Progress Tracker

- Week 1  ████████████████████  100% ✅
- Week 2  ████████████████████  100% ✅
- Week 3  ░░░░░░░░░░░░░░░░░░░░    0% 🔄
- Week 4  ░░░░░░░░░░░░░░░░░░░░    0% 🔄

---


## 👥 Week 2 — Team Contribution Tracker

| Task | Sruthi Rajeshkumar (Team Lead) | MD Abdulla | Sudarshan Yadav | Abhinaya |
|---|---|---|---|---|
| Task 1 — SQL Injection | ✅ Fully Completed | ✅ Fully Completed | 🔄 Half Completed | ❌ Not Completed |
| Task 2 — Broken Authentication | ✅ Fully Completed | ❌ Not Completed | ❌ Not Completed | ❌ Not Completed |
| Task 3 — XSS + Sensitive Data | ✅ Fully Completed | ❌ Not Completed | ❌ Not Completed | ❌ Not Completed |

---

## 📊 Week 2 — Individual Progress

| Team Member | Role | Tasks Completed | Status |
|---|---|---|---|
| Sruthi Rajeshkumar | Team Lead | Task 1 + Task 2 + Task 3 | ✅ 100% Complete |
| MD Abdulla | Member | Task 1 only | 🔄 33% Complete |
| Sudarshan Yadav | Member | Task 1 only | 🔄 33% Complete |
| Abhinaya | Member | None | ❌ 0% Complete |

---

## ⚠️ Week 2 Contribution Note

- **Sruthi Rajeshkumar (Team Lead)** has completed all Week 2 tasks fully with proper documentation and proof.
- **MD Abdulla (Mem)** completed Task 1 — SQL Injection fully.
- **Sudarshan Yadav (Mem)** completed Task 1 — SQL Injection fully.
- **Abhinaya (Mem)** has not responded or submitted any work for Week 2.

**Note:** All pending members have been notified to complete their tasks at the earliest.

---

---

### ✅ Week 3 — Completed
| Task | Description | Platform | Status |
|---|---|---|---|
| Task 1 | Security Misconfiguration Testing | DVWA + Juice Shop | ✅ Done |
| Task 2 | Broken Access Control Testing | DVWA + Juice Shop | ✅ Done |
| Task 3 | Proof of Concept (PoC) Reports | Documentation | ✅ Done |

---

### ✅ Week 4 — Completed
| Task | Description | Status |
|---|---|---|
| Task 1 | Final Penetration Testing Report | ✅ Done |
| Task 2 | Demo Session / Video Walkthrough | ⬜ Optional |

---

## 🔍 Vulnerabilities Found — Week 3

| # | Vulnerability | Platform | Severity | Status |
|---|---|---|---|---|
| 11 | Default Credentials | DVWA | 🔴 High | ✅ Confirmed |
| 12 | PHP Info Page Exposed | DVWA | 🔴 High | ✅ Confirmed |
| 13 | Admin Panel Exposed | Juice Shop | 🔴 Critical | ✅ Confirmed |
| 14 | FTP Directory Exposed | Juice Shop | 🔴 Critical | ✅ Confirmed |
| 15 | KeePass Database Downloadable | Juice Shop | 🔴 Critical | ✅ Confirmed |
| 16 | Weak Sequential Session IDs | DVWA | 🔴 High | ✅ Confirmed |
| 17 | Broken Access Control | Juice Shop | 🔴 Critical | ✅ Confirmed |
| 18 | JWT Token Exposed in localStorage | Juice Shop | 🔴 High | ✅ Confirmed |

---

## 📊 Final Progress Tracker

- Week 1  ████████████████████  100% ✅
- Week 2  ████████████████████  100% ✅
- Week 3  ████████████████████  100% ✅
- Week 4  ████████████████████  100% ✅

---

## 📊 Complete Vulnerability Summary

| # | Vulnerability | Platform | Severity | Week |
|---|---|---|---|---|
| 1 | SQL Injection — Error Based | DVWA | 🔴 Critical | Week 2 |
| 2 | SQL Injection — Boolean Based | DVWA | 🔴 Critical | Week 2 |
| 3 | SQL Injection — UNION Based | DVWA | 🔴 Critical | Week 2 |
| 4 | No Account Lockout | DVWA | 🔴 High | Week 2 |
| 5 | Weak Password Policy | DVWA | 🔴 High | Week 2 |
| 6 | SQLi Authentication Bypass | Juice Shop | 🔴 Critical | Week 2 |
| 7 | XSS Reflected | DVWA | 🔴 High | Week 2 |
| 8 | XSS Stored | DVWA | 🔴 Critical | Week 2 |
| 9 | Sensitive Data Exposure | DVWA | 🔴 High | Week 2 |
| 10 | Credentials in Plain Text URL | DVWA | 🔴 High | Week 2 |
| 11 | Default Credentials | DVWA | 🔴 High | Week 3 |
| 12 | PHP Info Page Exposed | DVWA | 🔴 High | Week 3 |
| 13 | Admin Panel Exposed | Juice Shop | 🔴 Critical | Week 3 |
| 14 | FTP Directory Exposed | Juice Shop | 🔴 Critical | Week 3 |
| 15 | KeePass Database Downloadable | Juice Shop | 🔴 Critical | Week 3 |
| 16 | Weak Sequential Session IDs | DVWA | 🔴 High | Week 3 |
| 17 | Broken Access Control | Juice Shop | 🔴 Critical | Week 3 |
| 18 | JWT Token Exposed | Juice Shop | 🔴 High | Week 3 |

---

## 🏆 Project Summary

| Metric | Value |
|---|---|
| Total Weeks | 4 |
| Total Tasks Completed | 10 |
| Total Vulnerabilities Found | 18 |
| Critical Vulnerabilities | 8 |
| High Vulnerabilities | 10 |
| Platforms Tested | 2 (DVWA + Juice Shop) |
| OWASP Categories Covered | 5 |
| Tools Used | Burp Suite, Docker, Kali Linux |
| GitHub Commits | 116+ |

---

## 👥 Final Team Contribution

| Task | Sruthi (Team Lead) | Abdulla | Sudarshan | Abhinaya |
|---|---|---|---|---|
| Week 1 — All Tasks | ✅ | ✅ | ✅ | ✅ |
| Week 2 — Task 1 SQLi | ✅ | ✅ | 🔄 Partial | ❌ |
| Week 2 — Task 2 Auth | ✅ | ❌ | ❌ | ❌ |
| Week 2 — Task 3 XSS | ✅ | ❌ | ❌ | ❌ |
| Week 3 — All Tasks | ✅ | ❌ | ❌ | ❌ |
| Week 4 — Final Report | ✅ | ❌ | ❌ | ❌ |

## ⚠️ Disclaimer

> All penetration testing activities documented in this repository are performed exclusively on intentionally vulnerable applications (DVWA and OWASP Juice Shop) in a controlled local environment for educational purposes only.
> These activities are part of an authorized internship program at Zaalimaa Development Pvt Ltd.

---

*© 2026 Zaalima Development Pvt Ltd Internship — Week 1 Report & Week 2 Report & Week 3 & Week 4 Report*  
*Team Lead: Sruthi Rajeshkumar*
