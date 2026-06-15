# 📋 Proof of Concept (PoC) Report
# Web Application Penetration Testing — OWASP Top 10 Focus

- **Prepared by:** Sruthi Rajeshkumar (Team Lead)  
- **Team Members:** Abhinaya | MD Abdulla | Sudarshan Yadav  
- **Organization:** Zaalimaa Development Pvt Ltd  
- **Project:** Project 2 — Web Application Penetration Testing (OWASP Top 10 Focus)  
- **Report Date:** 11.06.2026  
- **Testing Period:** Week 2 — Week 3  
- **Status:** ✅ Completed

---

## 📌 Executive Summary

This report documents all vulnerabilities discovered during penetration testing of DVWA (Damn Vulnerable Web Application) and OWASP Juice Shop using the OWASP Top 10:2025 framework.

A total of **15 vulnerabilities** were identified and exploited across both platforms, ranging from Critical to High severity.

---

## 🎯 Scope of Testing

| Platform | URL | Purpose |
|---|---|---|
| DVWA | http://localhost:8080 | Primary testing platform |
| OWASP Juice Shop | http://localhost:3000 | Secondary testing platform |

## 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| Burp Suite Community v2023.5.4 | Proxy, Intruder, Interception |
| Firefox 102.0 | Browser with proxy configuration |
| Docker 28.5.2 | Container platform |
| Kali Linux | Penetration testing OS |

---

## 📊 Vulnerability Summary

| # | Vulnerability | Platform | Severity | Status |
|---|---|---|---|---|
| 1 | SQL Injection — Error Based | DVWA | 🔴 Critical | ✅ Confirmed |
| 2 | SQL Injection — Boolean Based | DVWA | 🔴 Critical | ✅ Confirmed |
| 3 | SQL Injection — UNION Based | DVWA | 🔴 Critical | ✅ Confirmed |
| 4 | No Account Lockout | DVWA | 🔴 High | ✅ Confirmed |
| 5 | Weak Password Policy | DVWA | 🔴 High | ✅ Confirmed |
| 6 | SQLi Authentication Bypass | Juice Shop | 🔴 Critical | ✅ Confirmed |
| 7 | XSS Reflected | DVWA | 🔴 High | ✅ Confirmed |
| 8 | XSS Stored | DVWA | 🔴 Critical | ✅ Confirmed |
| 9 | Sensitive Data Exposure | DVWA | 🔴 High | ✅ Confirmed |
| 10 | Default Credentials | DVWA | 🔴 High | ✅ Confirmed |
| 11 | Admin Panel Exposed | Juice Shop | 🔴 Critical | ✅ Confirmed |
| 12 | FTP Directory Exposed | Juice Shop | 🔴 Critical | ✅ Confirmed |
| 13 | Weak Session IDs | DVWA | 🔴 High | ✅ Confirmed |
| 14 | Broken Access Control | Juice Shop | 🔴 Critical | ✅ Confirmed |
| 15 | JWT Token Exposure | Juice Shop | 🔴 High | ✅ Confirmed |

---

## 🔴 Critical Vulnerabilities: 7
## 🔴 High Vulnerabilities: 8
## 🟢 Total Vulnerabilities Found: 15

---

# 📝 Detailed PoC Reports

---

## PoC #1 — SQL Injection (Error Based)

| Field | Details |
|---|---|
| **Vulnerability** | SQL Injection — Error Based |
| **OWASP Reference** | A05:2025 - Injection |
| **Platform** | DVWA |
| **URL** | http://localhost:8080/vulnerabilities/sqli/ |
| **Severity** | 🔴 Critical |
| **Status** | ✅ Confirmed |

### Description
The application passes user input directly to the database query without sanitization, causing SQL syntax errors that reveal sensitive database information.

### Steps to Reproduce

1. Navigate to http://localhost:8080/vulnerabilities/sqli/
2. Set DVWA Security Level to Low
3. Enter payload in User ID field: 1' OR '1'='1
4. Click Submit
5. Observe SQL error message revealing MariaDB database type

### Evidence
- Payload: `1' OR '1'='1`
- Result: SQL syntax error revealed
- Database Type Exposed: MariaDB
- Screenshot: sqli-error-message.png

### Impact
- Database type and version exposed to attackers
- Confirms SQL Injection vulnerability exists
- Enables further exploitation

### Remediation
- Use parameterized queries / prepared statements
- Disable detailed error messages in production
- Implement input validation

---

## PoC #2 — SQL Injection (Boolean Based)

| Field | Details |
|---|---|
| **Vulnerability** | SQL Injection — Boolean Based |
| **OWASP Reference** | A05:2025 - Injection |
| **Platform** | DVWA |
| **URL** | http://localhost:8080/vulnerabilities/sqli/ |
| **Severity** | 🔴 Critical |
| **Status** | ✅ Confirmed |

### Description
Boolean-based SQL Injection allows extraction of all database records by manipulating the query logic.

### Steps to Reproduce

1. Navigate to http://localhost:8080/vulnerabilities/sqli/
2. Enter payload in User ID field: ' OR 1=1#
3. Click Submit
4. Observe all 5 users dumped from database

### Evidence
- Payload: `' OR 1=1#`
- Result: All 5 users extracted
- Users Found: admin, Gordon Brown, Hack Me, Pablo Picasso, Bob Smith
- Screenshot: sqli-all-users-dumped.png

### Impact
- Full database user table exposed
- Sensitive user information compromised
- Can be used for credential attacks

### Remediation
- Use parameterized queries
- Implement input sanitization
- Apply principle of least privilege to DB accounts

---

## PoC #3 — SQL Injection (UNION Based)

| Field | Details |
|---|---|
| **Vulnerability** | SQL Injection — UNION Based |
| **OWASP Reference** | A05:2025 - Injection |
| **Platform** | DVWA |
| **URL** | http://localhost:8080/vulnerabilities/sqli/ |
| **Severity** | 🔴 Critical |
| **Status** | ✅ Confirmed |

### Description
UNION-based SQL Injection allows extraction of database metadata including database name and current user credentials.

### Steps to Reproduce

1. Navigate to http://localhost:8080/vulnerabilities/sqli/
2. Enter payload: ' OR 1=1 UNION SELECT user(),database()#
3. Click Submit
4. Observe database credentials in output

### Evidence
- Payload: `' OR 1=1 UNION SELECT user(),database()#`
- Result: Database credentials extracted
- DB User: app@localhost
- DB Name: dvwa
- Screenshot: sqli-union-db-info.png

### Impact
- Critical database information exposed
- Attacker gains full knowledge of DB structure
- Can lead to complete database compromise

### Remediation
- Use parameterized queries
- Use Web Application Firewall (WAF)
- Restrict database user privileges

---

## PoC #4 — No Account Lockout

| Field | Details |
|---|---|
| **Vulnerability** | No Account Lockout / Brute Force |
| **OWASP Reference** | A07:2025 - Authentication Failures |
| **Platform** | DVWA |
| **URL** | http://localhost:8080/vulnerabilities/brute/ |
| **Severity** | 🔴 High |
| **Status** | ✅ Confirmed |

### Description
The application does not implement account lockout after multiple failed login attempts, allowing unlimited password guessing.

### Steps to Reproduce

1. Navigate to DVWA Brute Force module
2. Open Burp Suite — configure proxy
3. Submit login form — intercept request
4. Send to Intruder
5. Set password field as payload position
6. Add password list: password, 123456, admin, letmein, test...
7. Start attack
8. Observe no lockout occurs
9. Identify correct password by response length difference

### Evidence
- Tool: Burp Suite Intruder
- Payloads Tested: 8 common passwords
- Correct Password Found: "password" (Length: 4704 vs 4666)
- No lockout triggered after 8 attempts
- Screenshot: burp-intruder-attack-results.png

### Impact
- Unlimited password guessing allowed
- Weak passwords easily cracked
- Account takeover possible

### Remediation
- Implement account lockout after 3-5 failed attempts
- Add CAPTCHA after multiple failures
- Implement rate limiting
- Enforce strong password policy

---

## PoC #5 — Weak Password Policy

| Field | Details |
|---|---|
| **Vulnerability** | Weak Password Policy |
| **OWASP Reference** | A07:2025 - Authentication Failures |
| **Platform** | DVWA |
| **Severity** | 🔴 High |
| **Status** | ✅ Confirmed |

### Description
The application allows weak passwords that can be easily guessed or cracked using common password lists.

### Steps to Reproduce

1. Use Burp Suite Intruder brute force attack
2. Test common passwords: password, 123456, admin, letmein
3. Observe "password" is accepted as valid credential

### Evidence
- Cracked Password: "password"
- Method: Burp Suite Intruder
- Time to Crack: Seconds
- Screenshot: burp-intruder-password-found.png

### Impact
- Accounts easily compromised
- No complexity requirements enforced
- Vulnerable to dictionary attacks

### Remediation
- Enforce minimum 8 character passwords
- Require uppercase, lowercase, numbers, special chars
- Check passwords against common password lists
- Implement password strength meter

---

## PoC #6 — SQLi Authentication Bypass

| Field | Details |
|---|---|
| **Vulnerability** | SQL Injection — Authentication Bypass |
| **OWASP Reference** | A05:2025 - Injection |
| **Platform** | OWASP Juice Shop |
| **URL** | http://localhost:3000/#/login |
| **Severity** | 🔴 Critical |
| **Status** | ✅ Confirmed |

### Description
The login form is vulnerable to SQL Injection allowing attackers to bypass authentication and gain admin access without valid credentials.

### Steps to Reproduce

1. Navigate to http://localhost:3000/#/login
2. Enter in Email field: ' OR 1=1--
3. Enter anything in Password field: test
4. Click Login
5. Observe successful admin login!

### Evidence
- Payload: `' OR 1=1--`
- Result: Logged in as admin@juice-sh.op
- No valid credentials required
- Screenshot: juiceshop-auth-bypass-success.png

### Impact
- Complete authentication bypass
- Admin access without credentials
- Full application compromise possible

### Remediation
- Use parameterized queries for login
- Implement input validation
- Use ORM frameworks
- Apply WAF rules

---

## PoC #7 — XSS Reflected

| Field | Details |
|---|---|
| **Vulnerability** | Cross-Site Scripting — Reflected |
| **OWASP Reference** | A05:2025 - Injection |
| **Platform** | DVWA |
| **URL** | http://localhost:8080/vulnerabilities/xss_r/ |
| **Severity** | 🔴 High |
| **Status** | ✅ Confirmed |

### Description
User input is directly reflected in the page response without sanitization, allowing execution of arbitrary JavaScript.

### Steps to Reproduce

1. Navigate to DVWA XSS Reflected module
2. Enter payload: <script>alert('XSS')</script>
3. Click Submit
4. Observe alert popup fires!

### Evidence
- Payload: `<script>alert('XSS')</script>`
- Result: Alert popup showing "XSS" fired
- Input reflected in URL and page
- Screenshot: xss-reflected-alert.png

### Impact
- Script execution in victim's browser
- Session cookie theft possible
- Phishing attacks possible
- Credential harvesting

### Remediation
- Encode all user output
- Implement Content Security Policy (CSP)
- Validate and sanitize all inputs
- Use HTTPOnly cookies

---

## PoC #8 — XSS Stored

| Field | Details |
|---|---|
| **Vulnerability** | Cross-Site Scripting — Stored |
| **OWASP Reference** | A05:2025 - Injection |
| **Platform** | DVWA |
| **URL** | http://localhost:8080/vulnerabilities/xss_s/ |
| **Severity** | 🔴 Critical |
| **Status** | ✅ Confirmed |

### Description
Malicious script is permanently stored in the database and executes automatically for every user who visits the page.

### Steps to Reproduce

1. Navigate to DVWA XSS Stored module
2. Enter Name: Test
3. Enter Message: <script>alert('Stored XSS')</script>
4. Click Sign Guestbook
5. Observe alert fires!
6. Refresh page — alert fires AGAIN automatically!

### Evidence
- Payload: `<script>alert('Stored XSS')</script>`
- Result: Persistent alert on every page load
- Affects ALL visitors not just attacker
- Screenshot: xss-stored-persistent.png

### Impact
- Affects every user visiting the page
- Persistent attack without attacker interaction
- Can steal sessions of all visitors
- More dangerous than Reflected XSS

### Remediation
- Sanitize all stored user input
- Encode output before rendering
- Implement CSP headers
- Regular security scanning of stored content

---

## PoC #9 — Sensitive Data Exposure

| Field | Details |
|---|---|
| **Vulnerability** | Sensitive Data Exposure |
| **OWASP Reference** | A04:2025 - Cryptographic Failures |
| **Platform** | DVWA |
| **URL** | http://localhost:8080/phpinfo.php |
| **Severity** | 🔴 High |
| **Status** | ✅ Confirmed |

### Description
PHP Info page publicly accessible revealing complete server configuration, internal paths, and session information.

### Steps to Reproduce

1. Navigate to http://localhost:8080/phpinfo.php
2. Observe full server configuration exposed
3. Note PHP version, Apache version, server paths
4. Note session cookies visible in HTTP headers

### Evidence
- PHP Version: 7.0.30-0+deb9u1
- Apache Version: 2.4.25 (Debian)
- Server Root: /etc/apache2
- Document Root: /var/www/html
- PHPSESSID Cookie: Fully visible
- Screenshot: php-info-page.png

### Impact
- Server fingerprinting enabled
- Known vulnerabilities can be targeted
- Internal paths disclosed
- Session information exposed

### Remediation
- Remove phpinfo.php from production
- Restrict access to configuration pages
- Hide server version headers
- Use generic error pages

---

## PoC #10 — Default Credentials

| Field | Details |
|---|---|
| **Vulnerability** | Default Credentials |
| **OWASP Reference** | A02:2025 - Security Misconfiguration |
| **Platform** | DVWA |
| **URL** | http://localhost:8080 |
| **Severity** | 🔴 High |
| **Status** | ✅ Confirmed |

### Description
Application uses default credentials that were never changed, allowing anyone with knowledge of defaults to gain access.

### Steps to Reproduce

1. Navigate to http://localhost:8080
2. Enter Username: admin
3. Enter Password: password
4. Click Login
5. Observe successful login!

### Evidence
- Username: admin
- Password: password (default)
- Result: Full admin access granted
- Screenshot: dvwa-dashboard-week3.png

### Impact
- Unauthorized access to application
- Admin privileges obtained
- All application functions accessible

### Remediation
- Change all default credentials immediately
- Enforce strong password policy
- Implement password rotation policy
- Monitor for default credential usage

---

## PoC #11 — Admin Panel Exposed

| Field | Details |
|---|---|
| **Vulnerability** | Exposed Admin Panel |
| **OWASP Reference** | A02:2025 - Security Misconfiguration |
| **Platform** | OWASP Juice Shop |
| **URL** | http://localhost:3000/#/administration |
| **Severity** | 🔴 Critical |
| **Status** | ✅ Confirmed |

### Description
Administration panel accessible to any authenticated user without proper role-based access control.

### Steps to Reproduce

1. Login to Juice Shop with any account
2. Navigate to http://localhost:3000/#/administration
3. Observe full admin panel accessible!
4. Note all user emails visible
5. Note customer feedback visible

### Evidence
- URL: /#/administration
- Users Exposed: 10 registered users
- admin@juice-sh.op visible
- Customer feedback accessible
- Screenshot: juice-shop-admin-page.png

### Impact
- All user data exposed
- Admin functions available to non-admins
- User privacy violated
- Potential for data manipulation

### Remediation
- Implement role-based access control (RBAC)
- Restrict admin panel to admin role only
- Add proper authorization checks
- Log and monitor admin panel access

---

## PoC #12 — FTP Directory Exposed

| Field | Details |
|---|---|
| **Vulnerability** | Public FTP Directory |
| **OWASP Reference** | A02:2025 - Security Misconfiguration |
| **Platform** | OWASP Juice Shop |
| **URL** | http://localhost:3000/ftp |
| **Severity** | 🔴 Critical |
| **Status** | ✅ Confirmed |

### Description
FTP directory publicly accessible without authentication, exposing sensitive business files and password databases.

### Steps to Reproduce

1. Navigate to http://localhost:3000/ftp
2. Observe directory listing exposed!
3. Note sensitive files accessible
5. Download incident-support.kdbx
6. Observe KeePass database downloaded!

### Evidence
- URL: /ftp
- Files Exposed: 10 sensitive files
- Critical File: incident-support.kdbx (3.2KB)
- KeePass database downloaded without authentication
- Screenshot: juice-shop-ftp-exposed.png

### Impact
- Sensitive business data exposed
- Password database downloadable
- Legal documents accessible
- Encryption scripts exposed

### Remediation
- Disable public directory listing
- Implement authentication for file access
- Move sensitive files outside web root
- Remove backup files from production

---

## PoC #13 — Weak Session IDs

| Field | Details |
|---|---|
| **Vulnerability** | Weak Session IDs |
| **OWASP Reference** | A01:2025 - Broken Access Control |
| **Platform** | DVWA |
| **URL** | http://localhost:8080/vulnerabilities/weak_id/ |
| **Severity** | 🔴 High |
| **Status** | ✅ Confirmed |

### Description
Session IDs are sequential integers that can be easily predicted by an attacker to hijack other users' sessions.

### Steps to Reproduce

1. Navigate to DVWA Weak Session IDs module
2. Click Generate button
3. Open Developer Tools → Storage → Cookies
4. Note dvwaSession value
5. Click Generate again
6. Observe value increments by 1!

### Evidence
- dvwaSession = 11 (sequential)
- HttpOnly: false
- Secure: false
- SameSite: None
- Screenshot: session-id-cookie.png

### Impact
- Session hijacking possible
- Any valid session can be guessed
- Account takeover without credentials
- Affects all active users

### Remediation
- Use cryptographically random session IDs
- Set HttpOnly and Secure flags
- Set SameSite=Strict
- Implement session timeout

---

## PoC #14 — Broken Access Control

| Field | Details |
|---|---|
| **Vulnerability** | Broken Access Control |
| **OWASP Reference** | A01:2025 - Broken Access Control |
| **Platform** | OWASP Juice Shop |
| **URL** | http://localhost:3000/#/administration |
| **Severity** | 🔴 Critical |
| **Status** | ✅ Confirmed |

### Description
Application fails to enforce proper access controls allowing users to access admin functionality and other users' data.

### Steps to Reproduce

1. Login to Juice Shop as any user
2. Navigate to /#/administration
3. ccess admin panel successfully!
4. Navigate to /profile
5. View and modify admin profile!

### Evidence
- Admin panel accessible to regular users
- 10 user emails exposed
- Profile modification possible
- Screenshot: admin-panel-access.png

### Impact
- Privilege escalation
- Unauthorized data access
- User data manipulation
- Complete access control bypass

### Remediation
- Implement proper RBAC
- Server-side authorization checks
- Deny by default approach
- Regular access control audits

---

## PoC #15 — JWT Token Exposure

| Field | Details |
|---|---|
| **Vulnerability** | JWT Token in localStorage |
| **OWASP Reference** | A07:2025 - Authentication Failures |
| **Platform** | OWASP Juice Shop |
| **Severity** | 🔴 High |
| **Status** | ✅ Confirmed |

### Description
JWT authentication token stored in localStorage instead of HttpOnly cookie, making it accessible via JavaScript and vulnerable to XSS attacks.

### Steps to Reproduce

1. Login to Juice Shop
2. Open Developer Tools (F12)
3. Go to Storage → Local Storage
4. Navigate to localhost:3000
5. Observe JWT token stored in plain text!

### Evidence
- Token Location: localStorage
- Accessible via JavaScript
- Not protected by HttpOnly flag
- Screenshot: jwt-token-storage.png

### Impact
- Token theft via XSS attacks
- Session hijacking
- Account takeover
- Persistent unauthorized access

### Remediation
- Store JWT in HttpOnly cookies
- Implement token expiration
- Use short-lived tokens
- Implement token refresh mechanism

---

## 📊 Final Statistics

| Metric | Value |
|---|---|
| Total Vulnerabilities Found | 15 |
| Critical Vulnerabilities | 7 |
| High Vulnerabilities | 8 |
| Platforms Tested | 2 (DVWA + Juice Shop) |
| OWASP Categories Covered | 5 |
| Testing Duration | 2 Weeks |

---

## 🛡️ Overall Remediation Priority

| Priority | Vulnerability | Action |
|---|---|---|
| 🔴 Immediate | SQL Injection | Parameterized queries |
| 🔴 Immediate | SQLi Auth Bypass | Input validation |
| 🔴 Immediate | Stored XSS | Output encoding |
| 🔴 Immediate | Admin Panel Exposed | Implement RBAC |
| 🔴 Immediate | FTP Directory Exposed | Disable public access |
| 🟠 High | No Account Lockout | Rate limiting |
| 🟠 High | Weak Session IDs | Random session IDs |
| 🟠 High | Default Credentials | Change immediately |
| 🟠 High | JWT Token Exposure | Use HttpOnly cookies |
| 🟡 Medium | Sensitive Data Exposure | Remove phpinfo.php |

---

## ✅ Conclusion

This penetration test successfully identified 15 vulnerabilities
across DVWA and OWASP Juice Shop. The most critical findings include
SQL Injection vulnerabilities that allow complete database compromise,
authentication bypass, and broken access control that exposes
admin functionality to all users.

Immediate remediation is recommended for all Critical findings.
Regular security testing and code reviews should be implemented
to prevent these vulnerabilities in production environments.

---

*Report prepared by: Sruthi Rajeshkumar (Team Lead)*  
*Zaalimaa Development Pvt Ltd Internship*  
*Project 2 — Web Application Penetration Testing*  
*© 2026 — Confidential*
