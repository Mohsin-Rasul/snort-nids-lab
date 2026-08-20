# Intrusion Detection and Log Analysis Using Snort & Splunk 🛡️

## 📌 Project Overview
This repository contains the configuration, implementation, and operational guidelines for a **Network Intrusion Detection System (NIDS)**. The project integrates **Snort** as the primary detection sensor to monitor network traffic for malicious activity in real-time, alongside **Splunk** for log indexing, visualization, and analysis. It serves as a lightweight, educational security tool designed to detect cyber-attacks and display them on a graphical dashboard for easy analysis.

## 🚀 Features & Capabilities
*   **Real-time Traffic Analysis:** Monitors network traffic and detects malicious patterns using signature-based detection.
*   **Custom Rule Implementation:** Capable of detecting specific network threats, including ICMP DDoS attacks (Ping floods) and SSH Port Scanning.
*   **Log Generation:** Automatically generates alerts in `alert_fast.txt` format upon detecting suspicious traffic.
*   **Analysis Integration:** Formats structured log outputs for ingestion into SIEM tools like Splunk for visual categorization based on severity and type.

## 🛠️ Technologies & Tools
*   **IDS Engine:** Snort++ 3.10.0.0
*   **Virtualization:** VMware Workstation Pro (Host-Only configuration)
*   **Sensor Environment:** Ubuntu Linux (Interface: `ens33`)
*   **Attacker Environment:** Kali Linux
*   **Attack Tools:** Nmap (Network Mapper), standard ICMP tools

## 📂 Implementation Details

### 1. Snort Configuration
The Snort engine runs in daemon mode (`-D`) listening on the `ens33` interface. Configuration is managed via the Lua configuration file and validated successfully upon deployment:
```bash
sudo snort -c /usr/local/etc/snort/snort.lua
