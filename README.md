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
System	   Role

Ubuntu	   Wazuh Manager + Indexer + Dashboard

Kali Linux	Attacker + Agent

Windows 10	Agent + Sysmon
