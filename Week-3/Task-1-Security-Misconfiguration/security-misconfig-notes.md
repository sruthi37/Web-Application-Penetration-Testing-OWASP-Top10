# Week 3 — Task 1: Security Misconfiguration Testing

- **Intern (Team Lead):** Sruthi Rajeshkumar
- **Team Members:** Abhinaya | MD Abdulla | Sudarshan Yadav
- **Organization:** Zaalimaa Development Pvt Ltd
- **Project:** Project 2 — Web Application Penetration Testing (OWASP Top 10 Focus)
- **Week:** Week 3
- **Date:** 11.06.2026
- **Status:** ✅ Completed

---

## 📌 Objective

Perform Security Misconfiguration testing on DVWA and OWASP Juice Shop
to identify improperly configured systems, exposed sensitive files,
default credentials, and publicly accessible admin panels.

- **OWASP Reference:** A02:2025 - Security Misconfiguration  
- **Platform:** DVWA (http://localhost:8080) + Juice Shop (http://localhost:3000)  
- **Security Level:** Low  

---

## 📸 Screenshots

- Screenshot 1: Docker containers running — `screenshots/01-docker-ps-week3.png`
- Screenshot 2: DVWA Dashboard — `screenshots/02-dvwa-dashboard-week3.png`
- Screenshot 3: PHP Info page exposed — `screenshots/03-phpinfo-exposed-config.png`
- Screenshot 4: Juice Shop homepage — `screenshots/04-juice-shop-homepage.png`
- Screenshot 5: Admin panel accessible — `screenshots/05-juice-shop-admin-page.png`
- Screenshot 6: FTP directory exposed — `screenshots/06-juice-shop-ftp-exposed.png`
- Screenshot 7: KeePass database downloaded — `screenshots/07-kdbx-file-downloaded.png`
- Screenshot 8: API unauthorized response — `screenshots/08-api-unauthorized.png`

---

## 🛠️ Environment Setup

| Field | Details |
|---|---|
| **OS** | Kali Linux (VMware Workstation) |
| **Platform 1** | DVWA v1.10 — http://localhost:8080 |
| **Platform 2** | OWASP Juice Shop — http://localhost:3000 |
| **Security Level** | Low |

---

## 🧪 Testing Process

### Test 1 — Default Credentials (DVWA)

- **URL:** http://localhost:8080
- **Username:** admin
- **Password:** password
- **Result:** Login successful with default credentials!
- **Observation:** Default credentials never changed — major misconfiguration

### Test 2 — PHP Info Page Exposed (DVWA)

- **URL:** http://localhost:8080/phpinfo.php
- **Result:** Full server configuration exposed publicly
- **Sensitive Data Found:**
   - PHP Version: 7.0.30-0+deb9u1
   - Apache Version: 2.4.25
   - Server Root: /etc/apache2
   - Document Root: /var/www/html
   - PHPSESSID Cookie exposed
   - Internal IP: 172.17.0.2

### Test 3 — Admin Panel Exposed (Juice Shop)

- **URL:** http://localhost:3000/#/administration
- **Result:** Admin panel accessible without proper authentication!
- **Sensitive Data Found:**
   - All registered users listed
   - admin@juice-sh.op
   - jim@juice-sh.op
   - bender@juice-sh.op
   - bjoern.kimminich@gmail.com
   - ciso@juice-sh.op
   - Customer feedback visible
   - Challenges solved: Login Admin + Admin Section

### Test 4 — FTP Directory Exposed (Juice Shop)

- **URL:** http://localhost:3000/ftp
- **Result:** Full FTP directory publicly accessible!
- **Files Exposed:**
   - acquisitions.md — Business data
   - announcement_encrypted.md
   - coupons_2013.md.bak — Backup file
   - eastere.gg
   - encrypt.pyc — Encryption script
   - incident-support.kdbx — KeePass password database!
   - legal.md — Legal documents
   - package-lock.json.bak
   - package.json.bak
   - suspicious_errors.yml
   - quarantine folder

### Test 5 — KeePass Database Download

- **File:** incident-support.kdbx
- **Size:** 3.2 KB
- **Result:** Downloaded successfully without any authentication!
- **Observation:** Critical password database freely accessible to anyone

### Test 6 — API Endpoint Test

- **URL:** http://localhost:3000/api/Users
- **Result:** 401 Unauthorized — Authorization header required
- **Observation:** API endpoint protected — good security practice

---

## 🔎 Findings & Results

| # | Finding | Location | Severity |
|---|---|---|---|
| 1 | Default credentials admin/password | DVWA | 🔴 High |
| 2 | PHP Info page publicly exposed | DVWA | 🔴 High |
| 3 | Admin panel accessible without auth | Juice Shop | 🔴 Critical |
| 4 | All user emails exposed in admin panel | Juice Shop | 🔴 Critical |
| 5 | FTP directory publicly accessible | Juice Shop | 🔴 Critical |
| 6 | KeePass database downloadable | Juice Shop | 🔴 Critical |
| 7 | Backup files publicly accessible | Juice Shop | 🔴 High |
| 8 | Encryption script exposed | Juice Shop | 🔴 High |

---

## ⚠️ Vulnerabilities Identified

### 1. Default Credentials — High 🔴
- **Location:** DVWA Login
- **Impact:** Anyone can login with default credentials
- **Evidence:** admin/password login successful

### 2. PHP Info Exposure — High 🔴
- **Location:** DVWA phpinfo.php
- **Impact:** Full server configuration exposed to attackers
- **Evidence:** PHP version, Apache version, server paths visible

### 3. Admin Panel Exposure — Critical 🔴
- **Location:** Juice Shop /#/administration
- **Impact:** All user data exposed without authentication
- **Evidence:** 5 user emails visible including admin

### 4. FTP Directory Exposure — Critical 🔴
- **Location:** Juice Shop /ftp
- **Impact:** Sensitive files downloadable without authentication
- **Evidence:** KeePass database downloaded successfully

---

## 🛡️ Remediation Recommendations

| # | Recommendation |
|---|---|
| 1 | Change all default credentials immediately |
| 2 | Remove phpinfo.php from production environment |
| 3 | Restrict admin panel access with proper authentication |
| 4 | Disable public FTP directory listing |
| 5 | Implement proper access controls on sensitive files |
| 6 | Remove backup files from public directories |
| 7 | Implement rate limiting and monitoring |
| 8 | Regular security configuration audits |
| 9 | Use security headers (X-Frame-Options, CSP, HSTS) |

---

## ✅ Task Completion Status

| Team Member | Role | Status |
|---|---|---|
| Sruthi Rajeshkumar | Team Lead | ✅ Completed |
| Abhinaya | Member | ❌ 0% Complete |
| MD Abdulla | Member | ❌ 0% Complete |
| Sudarshan Yadav | Member | ❌ 0% Complete |
