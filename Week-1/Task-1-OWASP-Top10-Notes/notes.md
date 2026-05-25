# 📋 Week 1 — Task 1: OWASP Top 10:2025 Study Notes

**Intern (Team Lead):** Sruthi Rajeshkumar  

**Team Members:** Abhinaya | MD Abdulla | Sudarshan Yadav  

**Organization:** Zaalimaa Development Pvt Ltd  

**Project:** Project 2 — Web Application Penetration Testing (OWASP Top 10 Focus)  

**Week:** Week 1  

**Date:** 19.05.2026  

**Status:** ✅ Completed

---

## 📌 Objective
Study and document all 10 vulnerabilities from the OWASP Top 10:2025 framework — 
understanding each vulnerability's definition, real-world impact, attack examples, 
and prevention techniques.

**Reference:** https://owasp.org/Top10/2025/

---

## 📸 Screenshots
- Screenshot 1: OWASP Top 10:2025 Homepage — `screenshots/owasp-homepage.png`

 <img width="1600" height="791" alt="OWASP Top 10" src="https://github.com/user-attachments/assets/8a466da5-5dc7-4eb0-b549-20520c5ed523" />
 
- Screenshot 2: A01 Broken Access Control page — `screenshots/a01-broken-access-control.png`

  <img width="1600" height="786" alt="WhatsApp Image 2026-05-25 at 8 36 48 PM" src="https://github.com/user-attachments/assets/b6b4b5c5-9437-4f88-bf73-d17de034ed06" />
  
- Screenshot 3: A05 Injection page — `screenshots/a05-injection.png`

 <img width="1600" height="788" alt="WhatsApp Image 2026-05-25 at 8 36 48 PM (1)" src="https://github.com/user-attachments/assets/44aa3d9b-e269-4797-b7c8-74b035ac3032" />
 
- Screenshot 4: A07 Authentication Failures page — `screenshots/a07-authentication-failures.png`

  <img width="1600" height="788" alt="WhatsApp Image 2026-05-25 at 8 36 48 PM (2)" src="https://github.com/user-attachments/assets/5d4f684f-c1ee-4ae5-bd6c-5cc308f564f3" />

---

## 🔐 A01:2025 - Broken Access Control
**Definition:** Users are able to act outside their intended permissions —
accessing, modifying, or deleting data they shouldn't be allowed to.

**Impact:** Unauthorized data access, privilege escalation, full system compromise.

**Real-World Examples:**
- Changing a URL parameter (e.g., /account?id=123 → /account?id=456) 
  to view another user's data
- Accessing admin pages without admin privileges
- Manipulating JWT tokens to gain elevated roles

**Prevention:**
- Deny access by default — whitelist what is allowed
- Enforce access control checks server-side, not just client-side
- Log and monitor access control failures
- Invalidate session tokens after logout

---

## 🔐 A02:2025 - Security Misconfiguration
**Definition:** Insecure default settings, incomplete configurations, open cloud
storage, verbose error messages, or unnecessary features left enabled.

**Impact:** Attackers can exploit exposed settings to gain unauthorized access
or extract sensitive information.

**Real-World Examples:**
- Default admin credentials not changed (admin/admin)
- Detailed error messages exposing stack traces to users
- Unnecessary services or ports left open
- Missing HTTP security headers

**Prevention:**
- Remove or disable unused features, ports, and services
- Change all default credentials immediately after setup
- Use automated tools to verify configurations
- Display generic error messages — never expose stack traces

---

## 🔐 A03:2025 - Software Supply Chain Failures
**Definition:** Vulnerabilities introduced through third-party libraries, plugins,
or dependencies that are outdated, unverified, or compromised.

**Impact:** A single compromised dependency can affect thousands of applications.

**Real-World Examples:**
- Using outdated npm/pip packages with known CVEs
- Downloading plugins from untrusted sources
- SolarWinds-style attack — malicious code injected into a legitimate software update

**Prevention:**
- Regularly audit and update third-party dependencies
- Use tools like OWASP Dependency-Check or Snyk
- Only use packages from official, trusted repositories
- Verify checksums and signatures of downloaded packages

---

## 🔐 A04:2025 - Cryptographic Failures
**Definition:** Sensitive data transmitted or stored without proper encryption,
or using weak/outdated algorithms.

**Impact:** Exposure of sensitive data leading to identity theft, fraud,
or regulatory violations.

**Real-World Examples:**
- Storing passwords in plain text or with weak MD5/SHA1 hashing
- Transmitting sensitive data over HTTP instead of HTTPS
- Using weak encryption keys or outdated algorithms like DES

**Prevention:**
- Use strong algorithms: AES-256 for encryption, bcrypt/Argon2 for passwords
- Always enforce HTTPS for data in transit
- Never store sensitive data unnecessarily
- Use up-to-date TLS (1.2 or 1.3) configurations

---

## 🔐 A05:2025 - Injection
**Definition:** Malicious data is sent to an interpreter as part of a command
or query — the attacker's input is executed as code.

**Impact:** Full database compromise, authentication bypass, remote code execution.

**Real-World Examples:**
- SQL Injection: ' OR 1=1-- in a login field bypasses authentication
- XSS: script tag injected into a comment field executes malicious code
- Command Injection: passing system commands through unsanitized input fields

**Prevention:**
- Use parameterized queries / prepared statements for database calls
- Validate and sanitize ALL user input
- Use a Web Application Firewall (WAF)
- Apply the principle of least privilege to database accounts

---

## 🔐 A06:2025 - Insecure Design
**Definition:** Security flaws baked into the architecture or design — not
implementation bugs, but missing security controls from the start.

**Impact:** Fundamental weaknesses that are expensive to fix after deployment.

**Real-World Examples:**
- No rate limiting on login — allows brute force attacks
- Password reset flow that reveals whether an email exists
- No separation of duties in critical transactions

**Prevention:**
- Apply threat modeling during the design phase
- Use security design patterns and principles
- Conduct design reviews with security teams before development
- Create secure user stories with misuse/abuse cases

---

## 🔐 A07:2025 - Authentication Failures
**Definition:** Weaknesses in authentication or session management that allow
attackers to impersonate users or steal sessions.

**Impact:** Account takeover, unauthorized access to sensitive data, identity theft.

**Real-World Examples:**
- Allowing weak passwords like 123456 or password
- Session tokens exposed in URLs
- No lockout after multiple failed login attempts

**Prevention:**
- Enforce multi-factor authentication (MFA) for all users
- Implement account lockout after repeated failed logins
- Use secure, random session IDs and invalidate them after logout
- Never expose session tokens in URLs or logs

---

## 🔐 A08:2025 - Software or Data Integrity Failures
**Definition:** Code or data pipelines not protected against unauthorized
modification — involving auto-updates, CI/CD pipelines, or serialized data.

**Impact:** Malicious code execution, data tampering, backdoor installation.

**Real-World Examples:**
- Application auto-updates from untrusted CDN without signature verification
- Deserialization of untrusted data leading to remote code execution
- Malicious code pushed through a compromised CI/CD pipeline

**Prevention:**
- Verify digital signatures of downloaded software/updates
- Use trusted repositories and enforce dependency integrity checks
- Never deserialize data from untrusted sources
- Implement code review and approval gates in CI/CD pipelines

---

## 🔐 A09:2025 - Security Logging and Alerting Failures
**Definition:** Insufficient logging and monitoring means attacks go undetected
with no ability to respond to breaches in time.

**Impact:** Breaches go undetected for long periods, increasing damage and
recovery cost.

**Real-World Examples:**
- Failed login attempts are not logged
- No alerts triggered for suspicious activity like mass data downloads
- Logs stored locally and can be deleted by an attacker

**Prevention:**
- Log all authentication events and access control failures
- Use a centralized, tamper-proof SIEM system
- Set up automated alerts for suspicious patterns
- Regularly review and test your monitoring system

---

## 🔐 A10:2025 - Mishandling of Exceptional Conditions
**Definition:** Errors, exceptions, or edge cases not properly handled —
revealing sensitive information or causing insecure application failures.

**Impact:** Information disclosure, denial of service, unexpected exploitable behavior.

**Real-World Examples:**
- Unhandled exceptions revealing full stack traces to end users
- Application crashes when given unexpected input types
- Error messages disclosing internal server paths or database names

**Prevention:**
- Implement global exception handlers — never show raw errors to users
- Show generic error messages; log detailed errors server-side only
- Test all edge cases and boundary conditions thoroughly
- Fail securely — ensure errors don't leave the app vulnerable

---

## 📊 Summary Table

| ID | Vulnerability | Key Risk | Primary Fix |
|---|---|---|---|
| A01 | Broken Access Control | Unauthorized data access | Deny by default |
| A02 | Security Misconfiguration | Exposed settings | Remove unused features |
| A03 | Supply Chain Failures | Compromised dependencies | Audit dependencies |
| A04 | Cryptographic Failures | Data exposure | Use AES-256 / bcrypt |
| A05 | Injection | Database compromise | Parameterized queries |
| A06 | Insecure Design | Architectural flaws | Threat modeling |
| A07 | Authentication Failures | Account takeover | Enforce MFA |
| A08 | Integrity Failures | Malicious code execution | Verify signatures |
| A09 | Logging Failures | Undetected breaches | Centralized SIEM |
| A10 | Exceptional Conditions | Info disclosure | Generic error messages |

---

## ✅ Task Completion Status

| Team Member | Role | Status |
|---|---|---|
| Sruthi Rajeshkumar | Team Lead | ✅ Completed |
| Abhinaya | Member | ✅ Completed |
| MD Abdulla | Member | ✅ Completed |
| Sudarshan Yadav | Member | ✅ Completed |
