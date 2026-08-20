
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

```

### 2. Custom Detection Rules

The system utilizes a custom ruleset located at `/usr/local/etc/snort/rules/local.rules`.
Key rules include:

* **ICMP Ping Detection:**
`alert icmp any any -> any any (msg:"ICMP Ping Detected"; sid:1000001; rev:1;)`
* **SSH Port Scan Detection:**
`alert tcp any any -> any 22 (msg: "Potential SSH Scan Detected"; sid: 1000002; rev:1;)`

### 3. Attack Simulation & Results

The lab environment was rigorously tested using two isolated Virtual Machines:

* **ICMP Flood:** Simulated using `ping -c 4 8.8.8.8`. Snort successfully captured the traffic and generated a Priority 0 `ICMP Ping Detected` alert in under 1 second.
* **Port Scanning:** Simulated using `nmap -p 22 <target_ip>`. The system successfully detected the TCP SYN packets and generated a `Potential SSH Scan Detected` alert.

## 🔮 Future Enhancements

* **Intrusion Prevention System (IPS):** Transitioning the architecture to actively block traffic using mechanisms like Fail2Ban or SnortSam.
* **Dedicated Hardware:** Migrating the IDS sensor to a dedicated hardware device, such as a Raspberry Pi, for 24/7 network monitoring outside a workstation environment.
* **Advanced Analytics:** Expanding the SIEM integration with Splunk Enterprise and updating rules to detect complex application-layer attacks like SQL Injections.
* **Encrypted Traffic Analysis:** Configuring SSL decryption to inspect HTTPS packet payloads.

