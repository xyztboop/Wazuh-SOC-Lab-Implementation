# Wazuh-SOC-Lab-Implementation

## 📌 Project Overview

This project demonstrates the complete deployment of a **Security Operations Center (SOC)** lab using **Wazuh**.

### 🔹 Key Capabilities

- **Centralized Log Monitoring**
- **Endpoint Detection**
- **File Integrity Monitoring (FIM)**
- **Vulnerability Detection**
- **Security Configuration Assessment (SCA)**
- **Rootcheck**
- **Custom Detection Rules**
- **Intrusion Prevention using Active Response (IPS)**

The lab simulates a real enterprise SOC environment with **attack simulation and automated mitigation**.

##  Lab Architecture

### 🔹 Virtual Environment

| System | Role |
|--------|------|
| **Ubuntu** | Wazuh Manager + Indexer + Dashboard |
| **Kali Linux** | Attacker + Agent |
| **Windows 10** | Agent + Sysmon |

### 🔹 Machine IP Addresses

| Machine      | IP Address        | Role |
|--------------|------------------|------|
| **Ubuntu**   | 192.168.56.104   | Wazuh Manager + Indexer + Dashboard |
| **Kali Linux** | 192.168.56.105 | Attacker + Agent |
| **Windows 10** | 192.168.56.106 | Agent + Sysmon |

## 🔄 Data Flow Architecture

### 📌 Log Processing Workflow
Agent → Manager → Indexer → Dashboard

 Simple Explanation

#### 1️⃣ Agent
- Installed on Windows and Kali
- Collects system and security logs
- Sends logs to the Manager

👉 Agents act like sensors on each machine.

---

#### 2️⃣ Manager
- Receives logs from agents
- Checks logs using detection rules
- Generates alerts if something suspicious happens

👉 Manager is the brain of the SOC.

---

#### 3️⃣ Indexer
- Stores all alerts
- Makes searching fast and organized

👉 Indexer works like a secure database.

---

#### 4️⃣ Dashboard
- Shows alerts in a visual format
- Used by SOC analysts to monitor threats

👉 Dashboard is where we see everything.

---

### ✅ Why This Architecture Matters

- Centralized monitoring
- Real-time detection
- Organized alert storage
- Easy investigation

This setup simulates how a real enterprise SOC works

# 🗓️ WEEK 1 – SOC Deployment

## 🎯 Objective
Deploy Wazuh server and register multiple agents.

---

## ⚙️ Wazuh Installation (Ubuntu)

```bash
sudo apt install curl -y
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
sudo bash wazuh-install.sh -a -i.
```
<img width="940" height="516" alt="image" src="https://github.com/user-attachments/assets/48941feb-1873-4225-afb3-c86cab267a4a" />

## Agent Deployment:

Windows Agent
```
NET START wazuhSvc
```
<img width="940" height="353" alt="image" src="https://github.com/user-attachments/assets/d984f194-7621-4536-bb0d-9bf893955a43" />

Kali Agent:
```
sudo apt install wazuh-agent -y
sudo systemctl start wazuh-agent
```
<img width="940" height="482" alt="image" src="https://github.com/user-attachments/assets/03235140-8bf5-4ebe-9141-e94bcfd7b4f4" />

<img width="940" height="198" alt="image" src="https://github.com/user-attachments/assets/e2abb948-df21-4c32-9275-842c15f84164" />

## Sysmon Installation (Windows)

-Sysmon was installed for:

-Process monitoring

-Network monitoring

-Registry tracking

<img width="533" height="205" alt="image" src="https://github.com/user-attachments/assets/33b0fa3d-5d49-43f9-af6c-71883d4293b7" />

# WEEK 2 – Advanced Monitoring

Monitored directory:
```
/var/www
```
Configuration:
```
<directories realtime="yes" check_all="yes">/var/www</directories>
```
Tested by:

1.Creating file

2.Modifying file

3.Deleting file
<img width="820" height="433" alt="image" src="https://github.com/user-attachments/assets/adfe4ba8-4176-4c35-b04f-af28b236c5e9" />

<img width="940" height="483" alt="image" src="https://github.com/user-attachments/assets/27e852c0-a680-4a6d-be47-1b9db0c8542e" />

Vulnerability Detector
Enabled CVE scanning:
enabled = yes → Turn CVE scanning ON

 interval = 5m → Check every 5 minutes

run_on_start = yes → Scan immediately after restart

<img width="577" height="133" alt="Screenshot 2026-02-21 141319" src="https://github.com/user-attachments/assets/6d5a1a63-ca40-4809-b2a7-d51518d9f8e2" />

