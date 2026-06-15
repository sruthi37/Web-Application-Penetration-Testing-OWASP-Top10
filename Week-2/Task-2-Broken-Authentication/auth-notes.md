# 🔐 Week 2 — Task 2: Broken Authentication Testing

**Intern (Team Lead):** Sruthi Rajeshkumar  
**Team Members:** Abhinaya | MD Abdulla | Sudarshan Yadav  
**Organization:** Zaalimaa Development Pvt Ltd  
**Project:** Project 2 — Web Application Penetration Testing (OWASP Top 10 Focus)  
**Week:** Week 2  
**Date:** 04.06.2026  
**Status:** ✅ Completed

---

## 📌 Objective
Perform Broken Authentication testing on DVWA and OWASP Juice Shop
to understand how authentication vulnerabilities work, perform brute
force attacks using Burp Suite Intruder, and bypass login
authentication using SQL Injection.

**OWASP Reference:** A07:2025 - Authentication Failures  
**Platform:** DVWA (http://localhost:8080) + Juice Shop (http://localhost:3000)  
**Security Level:** Low  
**Module:** Brute Force + Login Bypass

---

## 📸 Screenshots

- Screenshot 1: Docker containers running — 

<img width="1600" height="838" alt="WhatsApp Image 2026-06-04 at 12 40 52 PM" src="https://github.com/user-attachments/assets/1f2d7205-2c87-44af-b9bb-56c5f52a4a48" />


- Screenshot 2: DVWA Dashboard — 

<img width="1600" height="842" alt="WhatsApp Image 2026-06-04 at 12 47 33 PM" src="https://github.com/user-attachments/assets/ce2e6bae-7cbc-4067-a25c-7f427b1b67e6" />


- Screenshot 3: Brute Force module —

<img width="1600" height="839" alt="WhatsApp Image 2026-06-04 at 1 08 36 PM" src="https://github.com/user-attachments/assets/c0492650-95af-4a2a-996b-c999271e38de" />


- Screenshot 4: Valid login success — 

<img width="1600" height="841" alt="WhatsApp Image 2026-06-04 at 1 10 06 PM" src="https://github.com/user-attachments/assets/1562ffd1-91da-479a-ac44-3fd078a2242d" />


- Screenshot 5: Failed login attempt —

<img width="1600" height="842" alt="WhatsApp Image 2026-06-04 at 1 11 59 PM" src="https://github.com/user-attachments/assets/f30268dd-d99d-4b93-aa65-8778a660f93f" />


- Screenshot 6: Login attempt captured — 

<img width="1600" height="845" alt="WhatsApp Image 2026-06-04 at 1 36 10 PM" src="https://github.com/user-attachments/assets/0577e0cf-eccd-44af-bb72-ea0bac81878f" />


- Screenshot 7: Burp Intercept capturing request — 

<img width="1600" height="845" alt="WhatsApp Image 2026-06-04 at 1 36 10 PM" src="https://github.com/user-attachments/assets/e7679185-632a-43ff-9afd-2c8559942171" />

- Screenshot 8: Intruder positions page — 

<img width="1600" height="843" alt="WhatsApp Image 2026-06-04 at 1 47 49 PM" src="https://github.com/user-attachments/assets/52b6100f-fde6-4af7-9c75-4f64d84f6839" />

- Screenshot 9: Intruder positions set — 

<img width="1600" height="843" alt="image" src="https://github.com/user-attachments/assets/37be0fc2-b989-4c84-b8b9-0ed4d08a36f4" />


- Screenshot 10: Intruder payloads added — 

<img width="1600" height="842" alt="image" src="https://github.com/user-attachments/assets/5c0cabac-65ec-4585-8f80-a89507776d05" />


- Screenshot 11: Intruder attack results —

<img width="1600" height="842" alt="image" src="https://github.com/user-attachments/assets/fa41a2a0-0255-44f7-98da-3c8eebb5dd2b" />


- Screenshot 12: Password found — 

<img width="1600" height="842" alt="image" src="https://github.com/user-attachments/assets/ec144da6-b801-47df-9f26-2b88ced52c30" />


- Screenshot 13: Intruder response — 

<img width="1600" height="846" alt="image" src="https://github.com/user-attachments/assets/7e62611f-ac76-43b1-8679-9efb86cd2f49" />


- Screenshot 14: Juice Shop login page —

<img width="1600" height="841" alt="image" src="https://github.com/user-attachments/assets/9ee2d500-42d0-4e48-bb34-f6fcb077e76f" />


- Screenshot 15: Juice Shop auth bypass — 

<img width="1600" height="842" alt="image" src="https://github.com/user-attachments/assets/bc831ac1-43d0-4d78-b64c-643f7c6bc033" />

<img width="1600" height="842" alt="image" src="https://github.com/user-attachments/assets/2488a803-1033-4648-911b-dd2b099ab140" />


---

## 🛠️ Environment Setup

| Field | Details |
|---|---|
| **OS** | Kali Linux (VMware Workstation) |
| **Platform 1** | DVWA v1.10 — http://localhost:8080 |
| **Platform 2** | OWASP Juice Shop — http://localhost:3000 |
| **Tool** | Burp Suite Community Edition v2023.5.4 |
| **Security Level** | Low |

---

## 🧪 Testing Process

### Test 1 — Valid Login (Baseline)

- **Input:** Username: admin | Password: password
- **Result:** Welcome to the password protected area admin
- **Observation:** Valid credentials work successfully
- Credentials visible in plain text in URL — security risk!

### Test 2 — Invalid Login

- **Input:** Username: admin | Password: wrongpassword
- **Result:** Username and/or password incorrect
- **Observation:** No account lockout after failed attempts
- No CAPTCHA or rate limiting implemented

### Test 3 — Burp Suite Brute Force Attack

- **Tool:** Burp Suite Intruder
- **Target:** http://localhost:8080/vulnerabilities/brute/
- **Method:** Sniper attack on password parameter
- **Payload:** Common password list (8 passwords)
- **Result:** Password "password" identified
- Length 4704 vs 4666 for others
- **Observation:** No lockout mechanism — full brute force possible

### Test 4 — Juice Shop SQLi Authentication Bypass

- **Platform:** OWASP Juice Shop
- **Email Field:** ' OR 1=1--
- **Password:** test
- **Result:** Successfully logged in as admin!
- **Observation:** SQL Injection in login field bypasses authentication

---

## 🔎 Findings & Results

| # | Test | Payload | Result | Severity |
|---|---|---|---|---|
| 1 | Valid Login | admin/password | Login successful | — |
| 2 | Invalid Login | admin/wrongpassword | No lockout found | 🔴 High |
| 3 | Brute Force | 8 common passwords | Password cracked: password | 🔴 Critical |
| 4 | SQLi Bypass | ' OR 1=1-- | Admin bypass successful | 🔴 Critical |

---

## 🔑 Credentials Discovered

| Platform | Username | Password | Method |
|---|---|---|---|
| DVWA | admin | password | Brute Force |
| Juice Shop | admin | N/A | SQLi Bypass |

---

## ⚠️ Vulnerabilities Identified

### 1. No Account Lockout — High 🔴
- **Location:** DVWA Brute Force module
- **Impact:** Allows unlimited password guessing
- **Evidence:** 8 passwords tested without any lockout

### 2. Weak Password Policy — High 🔴
- **Location:** DVWA
- **Impact:** Password "password" easily cracked
- **Evidence:** Brute force successful in first 8 attempts

### 3. Credentials in Plain Text URL — High 🔴
- **Location:** DVWA Brute Force module
- **Impact:** Credentials exposed in browser history
- **Evidence:** username=admin&password=password in URL

### 4. SQLi Authentication Bypass — Critical 🔴
- **Location:** Juice Shop login page
- **Impact:** Full admin access without valid credentials
- **Evidence:** ' OR 1=1-- bypassed login successfully

---

## 🛡️ Remediation Recommendations

| # | Recommendation |
|---|---|
| 1 | Implement account lockout after 3-5 failed attempts |
| 2 | Enforce strong password policy |
| 3 | Use POST method for login — never expose in URL |
| 4 | Implement CAPTCHA after multiple failed attempts |
| 5 | Use parameterized queries to prevent SQLi in login |
| 6 | Implement Multi-Factor Authentication (MFA) |
| 7 | Use rate limiting on login endpoints |

---

## ✅ Task Completion Status

| Team Member | Role | Status |
|---|---|---|
| Sruthi Rajeshkumar | Team Lead | ✅ Completed |
| Abhinaya | Member | ✅ Completed |
| MD Abdulla | Member | ✅ Completed |
| Sudarshan Yadav | Member | ✅ Completed |
