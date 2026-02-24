# Wazuh-SOC-Lab-Implementation

Project Overview

This project demonstrates the complete deployment of a Security Operations Center (SOC) lab using Wazuh, including:

Centralized log monitoring,
Endpoint detection,
File Integrity Monitoring (FIM),
Vulnerability Detection,
Security Configuration Assessment (SCA),
Rootcheck,
Custom Detection Rules,
Intrusion Prevention using Active Response (IPS).

The lab simulates a real enterprise SOC environment with attack simulation and automated mitigation.

Lab Architecture
🔹 Virtual Environment

Ubuntu	   Wazuh Manager + Indexer + Dashboard

Kali Linux	Attacker + Agent

Windows 10	Agent + Sysmon

🔹 Network Configuration

Host-Only Adapter → Internal SOC traffic

NAT Adapter → Internet updates

Machine	         IP Address

Ubuntu	          192.168.56.104

Kali	            192.168.56.105

Windows 10	      192.168.56.106
