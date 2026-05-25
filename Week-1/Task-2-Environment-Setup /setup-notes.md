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

<img width="958" height="503" alt="Screenshot 2026-05-17 214023" src="https://github.com/user-attachments/assets/aedaf28f-0e00-4114-b0c3-c5b0a56fa1f7" />


- Screenshot 2: DVWA Setup page at localhost:8080 — `screenshots/dvwa-setup-page.png`

<img width="959" height="505" alt="Screenshot 2026-05-17 214151" src="https://github.com/user-attachments/assets/5879d612-f1c9-4cee-acb7-0bbd718ea3bb" />


- Screenshot 3: DVWA Create/Reset Database success — `screenshots/dvwa-database-reset.png`

<img width="959" height="509" alt="Screenshot 2026-05-17 214442" src="https://github.com/user-attachments/assets/c1e87e4d-2076-47fe-9eb5-cb668eca288f" />

<img width="959" height="503" alt="Screenshot 2026-05-17 214501" src="https://github.com/user-attachments/assets/5eb2a83c-a890-43af-8d2f-519e638e8cec" />

<img width="959" height="507" alt="Screenshot 2026-05-17 214821" src="https://github.com/user-attachments/assets/d8dac935-d13a-4d9c-a9b2-6af708119864" />


- Screenshot 4: DVWA Dashboard logged in as admin — `screenshots/dvwa-dashboard.png`

<img width="959" height="504" alt="Screenshot 2026-05-17 214409" src="https://github.com/user-attachments/assets/63c432e6-62f2-467b-86cd-cbf20fc110ed" />


- Screenshot 5: Juice Shop running at localhost:3000 — `screenshots/juice-shop-running.png`

<img width="959" height="506" alt="Screenshot 2026-05-17 215301" src="https://github.com/user-attachments/assets/4f4e8bf2-ef41-475b-940e-d0cc25be2bbb" />

<img width="959" height="500" alt="Screenshot 2026-05-17 215442" src="https://github.com/user-attachments/assets/65ae98e4-4d28-47f5-a9e6-2c834da5f626" />

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
