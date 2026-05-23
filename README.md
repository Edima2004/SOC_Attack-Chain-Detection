# 🛡️ SOC_Attack-Chain-Detection Lab

## 📌 Project Overview

This project simulates a realistic cyber attack campaign against a Linux-based environment and demonstrates how various detection engineering techniques can be used to identify, monitor, and analyze attacker behavior using Wazuh, Suricata, auditd, and osquery.


The objective of this lab was to build a practical SOC-focused detection environment capable of identifying:

* reconnaissance activity,
* web exploitation attempts,
* credential attacks,
* authenticated access,
* and data exfiltration activity.

---

# 🎯 Objectives

* Simulate a realistic attacker lifecycle
* Develop custom Wazuh and Suricata detection rules
* Monitor Linux authentication and process activity
* Detect network reconnaissance techniques
* Detect SSH brute-force attacks
* Simulate SSH-based data exfiltration
* Analyze attacker behavior using MITRE ATT&CK mapping
* Build a portfolio-ready SOC detection engineering project

---


# 🧱 Lab Architecture

## Machines Used

| Machine       | Role                        |
| ------------- | --------------------------- |
| Kali Linux    | Attacker Machine            |
| Ubuntu Server | Victim Machine              |
| Wazuh Server  | SIEM / Log Analysis         |
| Suricata      | Network Intrusion Detection |
| osquery       | Endpoint Telemetry          |

---


# 🛠️ Technologies Used

| Tool        | Purpose                                 |
| ----------- | --------------------------------------- |
| Wazuh       | SIEM & Log Analysis                     |
| Suricata    | Network Intrusion Detection System      |
| auditd      | Linux Auditing                          |
| osquery     | Endpoint Telemetry & Process Monitoring |
| Hydra       | SSH Brute Force Simulation              |
| Nmap        | Network Reconnaissance                  |
| DVWA        | Vulnerable Web Application              |


---


# ⚔️ Simulated Attack Chain

The following attack sequence was simulated:

```text
Reconnaissance
    ↓
SQL Injection Exploitation
    ↓
Credential Harvesting
    ↓
SSH Brute Force / Password Spraying
    ↓
Successful SSH Authentication
    ↓
SSH-Based Data Exfiltration
    
```

---


# 🔍 Attack Simulation & Detection

---

## 1️⃣ Reconnaissance Detection

### Attack

Nmap scanning techniques were used against the victim machine:

```xml
nmap -sS <target-ip>
nmap -sX <target-ip>
nmap -sF <target-ip>
nmap -sU <target-ip>
```

### Detection

Custom Suricata rules were created to detect:

* SYN scans
* Xmas scans
* FIN scans
* UDP scans

Wazuh was also configured to generate alerts for suspicious scanning behavior.

### MITRE ATT&CK

| Technique       | ID    |
| --------------- | ----- |
| Active Scanning | T1595 |

_The rules implemented can be found in [suricata rules](/detection_rules/suricata_rules.md)_

---

## 2️⃣ SQL Injection Exploitation

### Attack

DVWA was configured with low security settings and tested using SQL injection payloads such as:

```sql
' OR 1=1--
```

### Detection

Apache and application logs were monitored through Wazuh to detect:

* SQL injection keywords
* suspicious query patterns
* authentication bypass attempts

### MITRE ATT&CK

| Technique                         | ID    |
| --------------------------------- | ----- |
| Exploit Public-Facing Application | T1190 |

_The configs added can be found in [sql configs](/detection-rules/wazuh_rules.md)_

---

## 3️⃣ SSH Brute Force Detection

### Attack

Hydra was used to perform SSH brute-force attacks using harvested credentials:

```bash
hydra -L usernames.txt -P passwords.txt ssh://<target-ip>
```

### Detection

Wazuh monitored:

* failed SSH authentication attempts
* repeated login failures
* successful SSH logins following failed attempts

### MITRE ATT&CK

| Technique      | ID    |
| -------------- | ----- |
| Brute Force    | T1110 |
| Valid Accounts | T1078 |

_The ssh rules added can be found in [ssh rules](/detection-rules/wazuh_rules.md)_

---

## 4️⃣ SSH-Based Data Exfiltration

### Attack

Sensitive files were transferred from the victim machine using SCP:

```bash
scp -r user@<target-ip>:~/sensitive_data .
```

### Detection

Detection methods included:

* SSH session monitoring
* osquery process monitoring
* Suricata network monitoring
* Wazuh correlation rules

### MITRE ATT&CK

| Technique                              | ID    |
| -------------------------------------- | ----- |
| Exfiltration Over Alternative Protocol | T1048 |

_The scp data exfiltration rules implemented can be found in[exfiltration config](/detection-rules/wazuh_rules.md)_

---


# 🧠 MITRE ATT&CK Mapping Summary

| Attack Phase         | MITRE Technique                        | ID    |
| -------------------- | -------------------------------------- | ----- |
| Reconnaissance       | Active Scanning                        | T1595 |
| SQL Injection        | Exploit Public-Facing Application      | T1190 |
| SSH Brute Force      | Brute Force                            | T1110 |
| Successful SSH Login | Valid Accounts                         | T1078 |
| Data Exfiltration    | Exfiltration Over Alternative Protocol | T1048 |
| Defense Evasion      | Rootkit                                | T1014 |

---

# 📸 Screenshots

The `screenshots/` directory contains:

* Wazuh alerts
* Suricata detections
* Hydra brute-force attempts
* Nmap scan detections
* Diamorphine detection evidence
* SCP exfiltration activity

---

# 🔧 Custom Detection Engineering

Custom rules were written for:

* reconnaissance detection
* SSH brute-force attacks
* suspicious authentication behavior
* SCP-based exfiltration activity
* Diamorphine-related anomalies

Rule files can be found in:

```xml
[detection rules](/detection-rules)
```

---

# 📚 Key Lessons Learned

* Network-based and host-based detections complement each other
* SIEM correlation significantly improves visibility
* SSH remains a common attack vector in Linux environments
* Defense evasion techniques can still leave detectable artifacts
* Detection engineering requires balancing visibility and noise reduction

---

# 🚀 Future Improvements

Potential future enhancements include:

* automated active response
* Sigma rule conversion
* malware sandbox integration
* threat intelligence enrichment
* automated incident response workflows

---

# 👨‍💻 Author

Vincent-Thompson Edima
Electrical/Electronics Engineer | SOC & Detection Engineering Enthusiast
