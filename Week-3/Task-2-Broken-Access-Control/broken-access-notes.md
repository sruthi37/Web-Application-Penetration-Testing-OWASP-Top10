# 🔓 Week 3 — Task 2: Broken Access Control Testing

**Intern (Team Lead):** Sruthi Rajeshkumar  
**Team Members:** Abhinaya | MD Abdulla | Sudarshan Yadav  
**Organization:** Zaalimaa Development Pvt Ltd  
**Project:** Project 2 — Web Application Penetration Testing (OWASP Top 10 Focus)  
**Week:** Week 3  
**Date:** 10.06.2026  
**Status:** ✅ Completed

---

## 📌 Objective
Perform Broken Access Control testing on DVWA and OWASP Juice Shop
to identify unauthorized access vulnerabilities, weak session management,
privilege escalation, and improper access restrictions.

**OWASP Reference:** A01:2025 - Broken Access Control  
**Platform:** DVWA (http://localhost:8080) + Juice Shop (http://localhost:3000)  
**Security Level:** Low  

---

## 📸 Screenshots

- Screenshot 1: Docker containers running — `screenshots/01-docker-ps-day2-week3.png`
- Screenshot 2: DVWA Dashboard — `screenshots/02-dvwa-dashboard-day2.png`
- Screenshot 3: Weak Session IDs module — `screenshots/03-dvwa-weak-session-ids.png`
- Screenshot 4: Session ID in cookie — `screenshots/04-session-id-cookie.png`
- Screenshot 5: Session ID incremental — `screenshots/05-session-id-incremental.png`
- Screenshot 6: Juice Shop homepage — `screenshots/06-juiceshop-homepage.png`
- Screenshot 7: Juice Shop logged in — `screenshots/07-juiceshop-loggedin.png`
- Screenshot 8: JWT token in storage — `screenshots/08-jwt-token-storage.png`
- Screenshot 9: Admin basket access — `screenshots/09-juiceshop-admin-basket.png`
- Screenshot 10: Admin panel access — `screenshots/10-admin-panel-access.png`
- Screenshot 11: User profile access — `screenshots/11-user-profile-access.png`

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

### Test 1 — Weak Session IDs (DVWA)

- **Module:** Weak Session IDs
- **URL:** http://localhost:8080/vulnerabilities/weak_id/
- **Method:** Click Generate button multiple times
- **Result:** Session ID increments by 1 each time!
- **Cookie Details Found:**
   - dvwaSession = 11 (sequential!)
   - HttpOnly: false
   - Secure: false
   - SameSite: None
- **Observation:** Session IDs are predictable and sequential
   An attacker can guess any valid session ID!

### Test 2 — JWT Token Exposure (Juice Shop)

- **Method:** Login via SQLi bypass
- **Tool:** Browser Developer Tools → Storage
- **Result:** JWT token visible in localStorage
- **Observation:** Token accessible via JavaScript
   HttpOnly flag not set — XSS can steal tokens!

### Test 3 — Admin Panel Unauthorized Access (Juice Shop)

- **URL:** http://localhost:3000/#/administration
- **Result:** Full admin panel accessible to any logged in user!
- **Data Exposed:**
   - 10 registered user emails
   - admin@juice-sh.op
   - jim@juice-sh.op
   - bender@juice-sh.op
   - bjoern.kimminich@gmail.com
   - ciso@juice-sh.op
   - support@juice-sh.op
   - morty@juice-sh.op
   - mc.safesearch@juice-sh.op
   - j12934@juice-sh.op
   - wurstbrot@juice-sh.op
   - Customer feedback visible
- **Observation:** No role-based access control implemented!

### Test 4 — User Profile Access (Juice Shop)

- **URL:** http://localhost:3000/profile
- **Result:** Admin profile fully accessible
- **Data Exposed:**
   - Email: admin@juice-sh.op
   - Can change username
   - Can upload profile picture
- **Observation:** Profile modification possible without proper verification

---

## 🔎 Findings & Results

| # | Finding | Location | Severity |
|---|---|---|---|
| 1 | Sequential Session IDs | DVWA | 🔴 High |
| 2 | HttpOnly: false on session cookie | DVWA | 🔴 High |
| 3 | Secure: false on session cookie | DVWA | 🔴 High |
| 4 | JWT token exposed in localStorage | Juice Shop | 🔴 High |
| 5 | Admin panel accessible to all users | Juice Shop | 🔴 Critical |
| 6 | All user emails exposed | Juice Shop | 🔴 Critical |
| 7 | User profile accessible without auth | Juice Shop | 🔴 High |

---

## ⚠️ Vulnerabilities Identified

### 1. Weak Session IDs — High 🔴
- **Location:** DVWA Weak Session IDs module
- **Impact:** Attacker can predict and hijack any user session
- **Evidence:** dvwaSession increments sequentially (1,2,3...)

### 2. Insecure Cookie Configuration — High 🔴
- **Location:** DVWA Session Cookie
- **Impact:** Session cookie can be stolen via XSS
- **Evidence:** HttpOnly:false, Secure:false, SameSite:None

### 3. Broken Access Control — Critical 🔴
- **Location:** Juice Shop Admin Panel
- **Impact:** Any user can access admin functionality
- **Evidence:** All user data visible at /#/administration

### 4. Sensitive Data Exposure via Profile — High 🔴
- **Location:** Juice Shop /profile
- **Impact:** User data exposed and modifiable
- **Evidence:** admin@juice-sh.op email and profile accessible

---

## 🛡️ Remediation Recommendations

| # | Recommendation |
|---|---|
| 1 | Use cryptographically random session IDs |
| 2 | Set HttpOnly and Secure flags on all cookies |
| 3 | Implement proper role-based access control (RBAC) |
| 4 | Restrict admin panel to admin users only |
| 5 | Store JWT tokens in HttpOnly cookies not localStorage |
| 6 | Implement proper authorization checks on all endpoints |
| 7 | Use SameSite=Strict on session cookies |
| 8 | Implement session timeout and invalidation |

---

## ✅ Task Completion Status

| Team Member | Role | Status |
|---|---|---|
| Sruthi Rajeshkumar | Team Lead | ✅ Completed |
| Abhinaya | Member | Not Completed |
| MD Abdulla | Member | Not Completed |
| Sudarshan Yadav | Member | Not Completed |
