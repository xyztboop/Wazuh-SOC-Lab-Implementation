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
sudo bash wazuh-install.sh -a -i

<img width="940" height="516" alt="image" src="https://github.com/user-attachments/assets/120e816c-8d00-4051-8d2d-8a2fc2db07f6" />


