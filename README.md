# 🔐 Project 2 — Web Application Penetration Testing (OWASP Top 10 Focus)

![Status](https://img.shields.io/badge/Status-In%20Progress-yellow)
![Week](https://img.shields.io/badge/Week%201-Completed-green)
![Organization](https://img.shields.io/badge/Organization-Zaalimaa%20Development%20Pvt%20Ltd-blue)

---

## 🏢 Internship Details

| Field | Details |
|---|---|
| **Organization** | Zaalimaa Development Pvt Ltd |
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

## 📋 Week 1 Tasks

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
| Task 3 — Burp Suite Recon | 5 screenshots | ✅ Uploaded |

---

## ⚠️ Disclaimer

> All penetration testing activities documented in this repository are performed
> exclusively on intentionally vulnerable applications (DVWA and OWASP Juice Shop)
> in a controlled local environment for educational purposes only.
> These activities are part of an authorized internship program at
> Zaalimaa Development Pvt Ltd.

---

*© 2026 Zaalimaa Development Pvt Ltd Internship — Week 1 Report*  
*Team Lead: Sruthi Rajeshkumar*
