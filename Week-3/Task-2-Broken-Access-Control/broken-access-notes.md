# 🔓 Week 3 — Task 2: Broken Access Control Testing

- **Intern (Team Lead):** Sruthi Rajeshkumar  
- **Team Members:** Abhinaya | MD Abdulla | Sudarshan Yadav  
- **Organization:** Zaalimaa Development Pvt Ltd  
- **Project:** Project 2 — Web Application Penetration Testing (OWASP Top 10 Focus)  
- **Week:** Week 3  
- **Date:** 10.06.2026  
- **Status:** ✅ Completed

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

- Screenshot 1: Docker containers running — 

<img width="1600" height="830" alt="01-docker-ps-day2-week3 png" src="https://github.com/user-attachments/assets/77590836-5c8c-453b-ac90-c7e4fde43cb6" />



- Screenshot 2: DVWA Dashboard — 

<img width="1600" height="843" alt="02-dvwa-dashboard-day2 png" src="https://github.com/user-attachments/assets/14877ce4-0eb8-4538-9bfd-f6929267193d" />



- Screenshot 3: Weak Session IDs module —

<img width="1600" height="843" alt="03-dvwa-weak-session-ids png" src="https://github.com/user-attachments/assets/173806ba-943e-4b36-ac72-e83df97502bb" />



- Screenshot 4: Session ID in cookie — 

<img width="1600" height="838" alt="04-session-id-cookie png" src="https://github.com/user-attachments/assets/e3c7c1a2-5261-4a6f-bfd3-d7b49ab65abb" />



- Screenshot 5: Session ID incremental — 

<img width="1600" height="839" alt="05-session-id-incremental png" src="https://github.com/user-attachments/assets/d5d1c1f1-7874-48e9-8eb2-e0ed2ff9dacb" />



- Screenshot 6: Juice Shop homepage — 

<img width="1600" height="842" alt="06-juiceshop-homepage png" src="https://github.com/user-attachments/assets/6f85bd87-9935-4855-801f-c711a5be158c" />



- Screenshot 7: Juice Shop logged in —

<img width="1600" height="838" alt="07-juiceshop-loggedin png" src="https://github.com/user-attachments/assets/a0d032b5-fef4-4f29-bb6b-8fff7ff5d860" />



- Screenshot 8: JWT token in storage — 

<img width="1600" height="834" alt="08-jwt-token-storage png" src="https://github.com/user-attachments/assets/db9dca4a-b051-4101-809d-10ccb27b64e4" />

- Screenshot 9: Admin basket access — 

<img width="1600" height="839" alt="image" src="https://github.com/user-attachments/assets/107e6eb3-3edb-46ae-84b7-4a603f3f6964" />



- Screenshot 10: Admin panel access — 

<img width="1600" height="841" alt="image" src="https://github.com/user-attachments/assets/37a53923-5f91-41c1-8ff2-87bef67f2b8a" />



- Screenshot 11: User profile access — 

<img width="1600" height="838" alt="image" src="https://github.com/user-attachments/assets/bf1ddf12-da7c-4e17-92dd-9b724b8a0ea0" />


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
