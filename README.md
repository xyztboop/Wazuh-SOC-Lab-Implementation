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

# WEEK 3 – Intrusion Prevention System (IPS)

## Aim:
Simulate an SSH brute force attack and automatically block attacker IP using Wazuh Active Response.
## SSH Setup (Ubuntu)
```
sudo apt install openssh-server -y
sudo systemctl start ssh
```
<img width="940" height="533" alt="image" src="https://github.com/user-attachments/assets/e422ace1-80b1-48f8-aa99-cd9925302aba" />

##  Brute Force Attack (Kali)
```
hydra -l sakshi -P /usr/share/wordlists/rockyou.txt -t 4 ssh://192.168.56.104
```
<img width="940" height="266" alt="image" src="https://github.com/user-attachments/assets/9bd6b04e-8342-448c-8d90-e48bade2a1c7" />
##  Detection in Wazuh

Search query used:
```
rule.id:5710 OR rule.id:5712 OR rule.id:5716
```
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/fdf5be6f-9283-4fd2-93cf-d95ba3c72663" />

##  Active Response Configuration:

Added inside ossec.conf:
```
<active-response>
  <command>firewall-drop</command>
  <location>local</location>
  <rules_id>5710,5712,5716</rules_id>
  <timeout>600</timeout>
</active-response>
```
##  Restarted service:
```
sudo systemctl restart wazuh-manager
```
<img width="756" height="263" alt="image" src="https://github.com/user-attachments/assets/c1a98623-31c7-4c8e-bc69-474ae8b643f5" />

<img width="940" height="77" alt="image" src="https://github.com/user-attachments/assets/399a3e3d-567d-4bec-8a82-d38c2e85bc42" />
##  Automatic IP Blocking:

After attack:

Hydra stopped

SSH connection denied

Firewall rule inserted automatically
Verification:
```
ssh sakshi@192.168.56.104
```
<img width="940" height="63" alt="image" src="https://github.com/user-attachments/assets/2492ef90-4d83-45b6-bb84-bf383521a9fc" />

<img width="940" height="276" alt="image" src="https://github.com/user-attachments/assets/d96069a0-0c7f-46db-87f4-348522c52404" />

## Alerts summary
<img width="940" height="391" alt="image" src="https://github.com/user-attachments/assets/033fcc3c-c294-466c-92f5-8d28e1ad9884" />

| Phase       | Action Performed              | Outcome |
|------------|------------------------------|----------|
| **Attack** | SSH brute force using Hydra  | Multiple failed login attempts generated |
| **Detection** | Wazuh rules 5710 / 5712 triggered | Security alerts created in dashboard |
| **Response** | `firewall-drop` active response executed | Attacker IP automatically blocked |
| **Validation** | SSH connection retried from Kali | Access denied / Connection blocked |

---

# 🧰 Technologies Used

- **Wazuh SIEM**
- **Ubuntu Linux**
- **Kali Linux**
- **Windows 10**
- **Sysmon**
- **Hydra**
- **VirtualBox**
- **Linux Firewall (iptables)**

---

# 🎓 Skills Demonstrated

- **SOC architecture deployment**
- **Log monitoring and analysis**
- **Attack simulation**
- **Detection rule validation**
- **Intrusion prevention configuration**
- **Firewall automation**
- **Real-time incident validation**
- **Troubleshooting and debugging**

---

# 🏁 Final Conclusion

This project successfully demonstrates a complete SOC lifecycle:

> **Monitoring → Detection → Alerting → Automated Response → Validation**

The lab replicates enterprise-level security monitoring and automated threat mitigation using Wazuh. It highlights practical implementation of defensive security engineering and real-world SOC operations.
