# 🔍 Week 2 — Task 3: XSS & Sensitive Data Exposure Testing

**Intern (Team Lead):** Sruthi Rajeshkumar  
**Team Members:** MD Abdulla | Sudarshan Yadav  
**Organization:** Zaalimaa Development Pvt Ltd  
**Project:** Project 2 — Web Application Penetration Testing (OWASP Top 10 Focus)  
**Week:** Week 2  
**Date:** 06.06.2026  
**Status:** ✅ Completed

---

## 📌 Objective
Perform Cross-Site Scripting (XSS) testing on DVWA to understand how
XSS vulnerabilities work, execute malicious scripts in the browser,
and document sensitive data exposure through PHP Info page.

**OWASP Reference:** A05:2025 - Injection (XSS) | A04:2025 - Cryptographic Failures  
**Platform:** DVWA (http://localhost:8080)  
**Security Level:** Low  
**Modules:** XSS Reflected | XSS Stored | PHP Info

---

## 📸 Screenshots

- Screenshot 1: Docker containers running:

<img width="1600" height="838" alt="WhatsApp Image 2026-06-05 at 11 51 06 PM" src="https://github.com/user-attachments/assets/9d724a61-5a90-43b6-a878-d98f3140ba37" />



- Screenshot 2: DVWA Dashboard:

<img width="1600" height="844" alt="WhatsApp Image 2026-06-05 at 11 54 14 PM" src="https://github.com/user-attachments/assets/6334198c-3f29-434a-b4cd-e1130453ac26" />



- Screenshot 3: XSS Reflected module: 

<img width="1600" height="842" alt="WhatsApp Image 2026-06-05 at 11 55 38 PM" src="https://github.com/user-attachments/assets/eb6fa846-6cc6-4097-b412-8ae35487de41" />



- Screenshot 4: Normal input result:

<img width="1600" height="839" alt="WhatsApp Image 2026-06-05 at 11 58 20 PM" src="https://github.com/user-attachments/assets/0d9717bc-3e16-4cf9-a0a9-d2a0a4bcd6bd" />



- Screenshot 5: XSS Reflected alert popup:

<img width="1600" height="843" alt="WhatsApp Image 2026-06-05 at 11 59 50 PM" src="https://github.com/user-attachments/assets/f652af0a-b809-46ca-bdcf-2c85befed7a1" />



- Screenshot 6: XSS Stored module:

<img width="1600" height="828" alt="WhatsApp Image 2026-06-06 at 12 02 48 AM" src="https://github.com/user-attachments/assets/e5444930-6d9c-4a50-a0b9-342a6e1bd468" />



- Screenshot 7: XSS Stored input:

<img width="1600" height="835" alt="WhatsApp Image 2026-06-06 at 12 05 06 AM" src="https://github.com/user-attachments/assets/291f7f6c-9013-49ae-9472-a9cb50f59e36" />



- Screenshot 8: XSS Stored alert popup:

<img width="1600" height="843" alt="WhatsApp Image 2026-06-06 at 12 06 01 AM" src="https://github.com/user-attachments/assets/ba70fedd-b1d6-4261-b2e1-cccafc3c0c0c" />



- Screenshot 9: XSS Stored persistent alert:

<img width="1600" height="839" alt="WhatsApp Image 2026-06-08 at 1 02 17 PM" src="https://github.com/user-attachments/assets/40100c9d-e04d-4b83-a54d-a1a5eae089be" />



- Screenshot 10: PHP Info page:

<img width="1600" height="763" alt="WhatsApp Image 2026-06-08 at 1 07 47 PM" src="https://github.com/user-attachments/assets/71a44230-0b27-4d61-aa37-40b0e3167d5c" />



- Screenshot 11: Apache environment exposed:

<img width="1600" height="842" alt="WhatsApp Image 2026-06-08 at 1 07 47 PM (1)" src="https://github.com/user-attachments/assets/9ab4c876-1ab0-4e8d-8f69-607451104487" />



- Screenshot 12: Sensitive data exposed:

<img width="1600" height="840" alt="WhatsApp Image 2026-06-08 at 1 07 47 PM (2)" src="https://github.com/user-attachments/assets/50057d7b-6e58-4478-969c-2e7c512113ce" />



---

## 🛠️ Environment Setup

| Field | Details |
|---|---|
| **OS** | Kali Linux (VMware Workstation) |
| **Platform** | DVWA v1.10 |
| **URL** | http://localhost:8080 |
| **Security Level** | Low |
| **Modules Tested** | XSS Reflected, XSS Stored, PHP Info |

---

## 🧪 Testing Process

### Part 1 — XSS Reflected Testing

#### Step 1 — Normal Input (Baseline)
Input: John
Result: Hello John
Observation: Input is directly reflected in the page output
             Input also visible in URL — ?name=John
             No input sanitization

#### Step 2 — XSS Reflected Payload
Input: <script>alert('XSS')</script>
Result: Alert popup fired showing "XSS"
Observation: Script executed successfully in browser
             Malicious input reflected without sanitization
             URL contains the injected script

---

### Part 2 — XSS Stored Testing

#### Step 1 — Inject Stored XSS Payload
Name Field: Test
Message Field: <script>alert('Stored XSS')</script>
Clicked: Sign Guestbook
Result: Alert popup fired showing "Stored XSS"

#### Step 2 — Verify Persistence
- Action: Refreshed the page
- Result: Alert fired AGAIN automatically!
- Observation: Script permanently stored in database
               Fires for every user who visits the page
               More dangerous than Reflected XSS

---

### Part 3 — Sensitive Data Exposure (PHP Info)

#### Module: PHP Info
- URL: http://localhost:8080/phpinfo.php
- Result: Full server configuration exposed!

Sensitive Data Found:
- PHP Version: 7.0.30-0+deb9u1
- Apache Version: 2.4.25 (Debian)
- Server Root: /etc/apache2
- Document Root: /var/www/html
- Server Admin: webmaster@localhost
- PHPSESSID Cookie: Fully exposed
- Security Level: visible in cookie
- All loaded modules listed
- Internal IP: 172.17.0.2
- Server Port: 8080

---

## 🔎 Findings & Results

| # | Test | Payload | Result | Severity |
|---|---|---|---|---|
| 1 | XSS Reflected | <script>alert('XSS')</script> | Alert fired | 🔴 High |
| 2 | XSS Stored | <script>alert('Stored XSS')</script> | Persistent alert | 🔴 Critical |
| 3 | Sensitive Data | PHP Info page | Full server info exposed | 🔴 High |

---

## ⚠️ Vulnerabilities Identified

### 1. Reflected XSS — High 🔴
- **Location:** XSS Reflected module — Name input field
- **Payload:** <script>alert('XSS')</script>
- **Impact:** Script executes in victim's browser
- **Evidence:** Alert popup fired successfully

### 2. Stored XSS — Critical 🔴
- **Location:** XSS Stored module — Message input field
- **Payload:** <script>alert('Stored XSS')</script>
- **Impact:** Persistent script affects ALL visitors
- **Evidence:** Alert fires automatically on every page load

### 3. Sensitive Data Exposure — High 🔴
- **Location:** PHP Info page (phpinfo.php)
- **Impact:** Full server configuration exposed to attackers
- **Evidence:** PHP version, Apache version, server paths, cookies all visible

---

## 🗄️ Sensitive Data Extracted

| Data | Value | Risk |
|---|---|---|
| PHP Version | 7.0.30-0+deb9u1 | Known vulnerabilities |
| Apache Version | 2.4.25 (Debian) | Known vulnerabilities |
| Server Root | /etc/apache2 | Path disclosure |
| Document Root | /var/www/html | Path disclosure |
| Internal IP | 172.17.0.2 | Network info |
| PHPSESSID | Fully exposed | Session hijacking |
| Security Level | Visible in cookie | Security bypass |

---

## 🛡️ Remediation Recommendations

| # | Recommendation |
|---|---|
| 1 | Sanitize and encode ALL user inputs |
| 2 | Implement Content Security Policy (CSP) |
| 3 | Use HTTPOnly and Secure flags on cookies |
| 4 | Never expose phpinfo.php in production |
| 5 | Remove or restrict access to debug pages |
| 6 | Use output encoding to prevent script injection |
| 7 | Implement input validation on both client and server side |
| 8 | Keep PHP and Apache versions updated |
| 9 | Hide server version information from headers |

---

## ✅ Task Completion Status

| Team Member | Role | Status |
|---|---|---|
| Sruthi Rajeshkumar | Team Lead | ✅ Completed |
| MD Abdulla | Member | ✅ Completed |
| Sudarshan Yadav | Member | ✅ Completed |
