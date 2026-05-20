# 🔍 Week 1 — Task 3: Burp Suite Reconnaissance & Spidering

**Intern (Team Lead):** Sruthi Rajeshkumar  

**Team Members:** Abhinaya | MD Abdulla | Sudarshan Yadav

**Organization:** Zaalimaa Development Pvt Ltd  

**Project:** Project 2 — Web Application Penetration Testing (OWASP Top 10 Focus)  

**Week:** Week 1  

**Date:** 19.05.2026  

**Status:** ✅ Completed

---

## 📌 Objective
Install and configure Burp Suite Community Edition. Perform basic reconnaissance
and spidering on OWASP Juice Shop, capture live HTTP requests, and document
all discovered endpoints.

---

## 📸 Screenshots
- Screenshot 1: Burp Suite Dashboard — `screenshots/burp-suite-dashboard.png`
- Screenshot 2: Proxy Settings (port 8081) — `screenshots/proxy-settings.png`
- Screenshot 3: Firefox Proxy Configuration — `screenshots/firefox-proxy-config.png`
- Screenshot 4: Intercept capturing live HTTP request — `screenshots/intercept-live-request.png`
- Screenshot 5: Site Map showing localhost:3000 endpoints — `screenshots/site-map-endpoints.png`

---

## 🛠️ Tool Information
- **Tool:** Burp Suite Community Edition v2023.5.4
- **Target:** OWASP Juice Shop (http://localhost:3000)

---

## ⚙️ Configuration Steps

### Step 1 — Launch Burp Suite
```bash
burpsuite
```
- Selected: Temporary Project → Burp Defaults → Start Burp

### Step 2 — Proxy Configuration
- Default port 8080 conflicted with DVWA
- Changed Burp proxy listener to: 127.0.0.1:8081

### Step 3 — Firefox Proxy Setup
- Settings → Network → Manual Proxy Configuration
- HTTP Proxy: 127.0.0.1 | Port: 8081
- Enabled "Also use this proxy for HTTPS"
- Enabled localhost proxying via about:config:
  network.proxy.allow_hijacking_localhost = true

### Step 4 — Reconnaissance
- Turned Intercept ON
- Browsed Juice Shop — captured live HTTP requests
- Turned Intercept OFF — passive traffic monitoring
- Site Map built automatically as pages were browsed

---

## 🔎 Discovered Endpoints

| Endpoint | Method | Type | Status |
|---|---|---|---|
| /rest/products/search | GET | JSON API | 200 |
| /rest/admin/application-configuration | GET | JSON API | 304 |
| /api/Challenges/ | GET | JSON API | 304 |
| /socket.io/ | GET | WebSocket | 200 |
| /main.js | GET | Script | 200 |
| /polyfills.js | GET | Script | 200 |
| /favicon.ico | GET | HTML | 200 |

---

## 📝 Observations
- Juice Shop exposes multiple REST API endpoints without authentication
- Admin configuration endpoint /rest/admin/application-configuration is accessible
- WebSocket connections established via /socket.io/
- Multiple JavaScript chunk files discovered revealing application structure

---

## ✅ Task Completion Status

| Team Member | Role | Status |
|---|---|---|
| Sruthi Rajeshkumar | Team Lead | ✅ Completed |
| Abhinaya | Member | ✅ Completed |
| MD Abdulla | Member | ✅ Completed |
| Sudarshan Yadav | Member | ✅ Completed |
