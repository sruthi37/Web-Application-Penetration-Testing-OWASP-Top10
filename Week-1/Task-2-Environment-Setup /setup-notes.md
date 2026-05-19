# 🛠️ Week 1 — Task 2: Test Environment Setup

**Intern (Team Lead):** Sruthi Rajeshkumar  

**Team Members:** Abhinaya | MD Abdulla | Sudarshan Yadav  

**Organization:** Zaalimaa Development Pvt Ltd  

**Project:** Project 2 — Web Application Penetration Testing (OWASP Top 10 Focus)  

**Week:** Week 1  

**Date:** 19.05.2026  

**Status:** ✅ Completed

---

## 📌 Objective
Install and configure both DVWA (Damn Vulnerable Web Application) and OWASP
Juice Shop on Kali Linux. Verify that both environments are running correctly
and accessible for penetration testing.

---

## 📸 Screenshots
- Screenshot 1: Terminal showing docker ps (both containers running) — `screenshots/docker-ps.png`
- Screenshot 2: DVWA Setup page at localhost:8080 — `screenshots/dvwa-setup-page.png`
- Screenshot 3: DVWA Create/Reset Database success — `screenshots/dvwa-database-reset.png`
- Screenshot 4: DVWA Dashboard logged in as admin — `screenshots/dvwa-dashboard.png`
- Screenshot 5: Juice Shop running at localhost:3000 — `screenshots/juice-shop-running.png`

---

## 🖥️ System Information
- **OS:** Kali Linux (VMware Workstation)
- **Docker Version:** 28.5.2

---

## ⚙️ Setup Process

### Step 1 — Docker Installation
```bash
sudo apt update
sudo apt install -y docker.io
sudo systemctl start docker
sudo systemctl enable docker
sudo docker --version
```

### Step 2 — DVWA Setup
```bash
sudo docker pull vulnerables/web-dvwa
sudo docker run -d -p 8080:80 vulnerables/web-dvwa
```
- Accessed at: http://localhost:8080
- Login credentials: admin / password
- Clicked "Create / Reset Database" — Setup successful

### Step 3 — OWASP Juice Shop Setup
```bash
sudo docker pull bkimminich/juice-shop
sudo docker run -d -p 3000:3000 bkimminich/juice-shop
```
- Accessed at: http://localhost:3000

### Step 4 — Verify Both Running
```bash
sudo docker ps
```
- DVWA: Running ✅ (0.0.0.0:8080->80/tcp)
- Juice Shop: Running ✅ (0.0.0.0:3000->3000/tcp)

---

## ✅ Task Completion Status

| Team Member | Role | Status |
|---|---|---|
| Sruthi Rajeshkumar | Team Lead | ✅ Completed |
| Abhinaya | Member | ✅ Completed |
| MD Abdulla | Member | ✅ Completed |
| Sudarshan Yadav | Member | ✅ Completed |
