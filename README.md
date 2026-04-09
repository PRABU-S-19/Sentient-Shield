# 🛡️ Sentient Shield — Enterprise EDR & Threat Hunting Grid

![Wazuh](https://img.shields.io/badge/Wazuh-4.7.5-blue)
![Status](https://img.shields.io/badge/Status-Complete-green)
![MITRE](https://img.shields.io/badge/MITRE-ATT%26CK-red)
![Platform](https://img.shields.io/badge/Platform-Linux%20%7C%20Windows-lightgrey)

> **Project 2 — Infotact Solutions CDOC (Blue Team Alpha)**
> Enterprise-grade SOC EDR grid using Wazuh SIEM for real-time 
> threat detection, FIM, active response, and threat simulation.

---

## 📌 Project Overview

| Field | Details |
|---|---|
| **Project Name** | Sentient Shield |
| **Organization** | Infotact Solutions — CDOC |
| **Team** | Blue Team Alpha |
| **Role** | Security Operations Trainee |
| **Duration** | 4 Weeks |
| **Status** | ✅ Complete |

---

## 🎯 Problem Statement

Infotact's servers face constant brute-force attacks and ransomware 
threats. Required a centralized real-time system to:
- Detect file integrity violations instantly
- Monitor critical system files 24/7
- Auto-respond to brute force attacks
- Map threats to MITRE ATT&CK framework
- Simulate and detect ransomware kill chains

┌─────────────────────────────────────────────┐
│              VIRTUALBOX LAB                 │
│                                             │
│  ┌──────────────────┐  ┌─────────────────┐  │
│  │  Wazuh Manager   │  │ Windows Server  │  │
│  │  Ubuntu 22.04    │  │  2019 Eval      │  │
│  │  192.168.56.104  │  │ 192.168.56.107  │  │
│  │  - SIEM Backend  │  │  - Wazuh Agent  │  │
│  │  - Rules Engine  │  └─────────────────┘  │
│  │  - Dashboard     │  ┌─────────────────┐  │
│  └──────────────────┘  │  Linux WebServer│  │
│                        │  Ubuntu 24.04   │  │
│                        │  - Wazuh Agent  │  │
│                        │  - SSH Server   │  │
│                        └─────────────────┘  │
└─────────────────────────────────────────────┘

---

## 🛠️ Tech Stack

| Tool | Version | Purpose |
|---|---|---|
| **Wazuh** | 4.7.5 | SIEM/EDR Platform |
| **VirtualBox** | Latest | Virtualization |
| **Ubuntu** | 22.04/24.04 | Linux Endpoints |
| **Windows Server** | 2019 | Windows Endpoint |
| **OpenSearch** | Latest | Log Indexing |
| **Hydra** | 9.5 | Brute Force Simulation |
| **Atomic Red Team** | Latest | Threat Simulation |

---

## 📅 Sprint Results

### ✅ Week 1 — Infrastructure & Agent Deployment

**Objective:** Deploy Wazuh Manager and connect all agents

**Completed:**
- Deployed Wazuh Manager on Ubuntu using all-in-one installer
- Configured isolated Host-Only network environment
- Deployed Wazuh agents on Linux WebServer and Windows Server
- Achieved 100% agent coverage

**Gate Check:** ✅ PASSED

Agent 001: Windows-Server  (192.168.56.107) → Active ✅
Agent 002: Linux-WebServer (192.168.56.110) → Active ✅
Coverage: 100%

---

### ✅ Week 2 — Detection Rules & Logic

**Objective:** Configure FIM, custom rules, vulnerability detection

#### File Integrity Monitoring
- Real-time monitoring on critical directories
- Uses Linux inotify for instant detection
- Alerts within 5 seconds of file change

**Monitored Directories:**
/etc          → System configuration
/usr/bin      → System executables
/usr/sbin     → Admin tools
/var/www/html → Web application files
/var/log      → System logs
/tmp          → Temporary files

#### Custom Detection Rules

| Rule ID | Level | Description | MITRE |
|---|---|---|---|
| 100005 | 6 | Authentication failure | T1110 |
| 100006 | 10 | Brute force detected | T1110.001 |
| 100010 | 12 | File encryption detected | T1486 |
| 100011 | 12 | Credential file accessed | T1003 |
| 100012 | 15 | System log cleared | T1070 |
| 100013 | 12 | Password file dumped | T1003 |

#### Vulnerability Detector
- Automated CVE scanning on all agents
- Feeds: Canonical (Ubuntu) + NVD
- Scan interval: 5 minutes

**Gate Check:** ✅ PASSED

FIM alert generated within 5 seconds ✅
Custom rules firing correctly ✅
Vulnerability detector enabled ✅

---

### ✅ Week 3 — Active Response (IPS)

**Objective:** Auto-ban brute force attackers

**Scenario:**
Attacker → SSH Brute Force → Wazuh Detects → IP Banned!

**Configuration:**
- Rule 5763 triggers firewall-drop command
- Timeout: 3600 seconds (1 hour ban)
- Location: Local (on affected endpoint)

**Gate Check:** ✅ PASSED
```bash
# Attacker IP automatically banned:
DROP  192.168.56.110  ← Confirmed in iptables ✅
```

---

### ✅ Week 4 — Threat Simulation

**Objective:** Simulate ransomware kill chain and visualize

**Simulated Techniques:**

| Technique | ID | Simulation Method |
|---|---|---|
| Log Clearing | T1070 | Cleared /var/log/syslog |
| Credential Dump | T1003 | Accessed /etc/shadow |
| File Encryption | T1486 | Renamed files to .encrypted |
| Backup Deletion | T1490 | Deleted .bak files |
| Password Dump | T1003 | Copied /etc/passwd |

**Gate Check:** ✅ PASSED

Kill chain visualized in dashboard ✅
All techniques detected ✅
Executive report generated ✅

---

## 🎯 MITRE ATT&CK Coverage

| Technique | ID | Detection | Response |
|---|---|---|---|
| Brute Force | T1110 | Rule 100005 | Auto-ban IP |
| Password Guessing | T1110.001 | Rule 100006 | Auto-ban IP |
| Credential Dumping | T1003 | Rule 100011 | Alert Level 12 |
| File Encryption | T1486 | Rule 100010 | Alert Level 12 |
| Log Clearing | T1070 | Rule 100012 | Alert Level 15 |
| Data Manipulation | T1565 | FIM | Alert Level 7 |

---

## 📁 Repository Structure

Sentient-Shield/
│
├── README.md
├── configs/
│   ├── agent-ossec.conf
│   └── manager-ossec.conf
├── rules/
│   └── local_rules.xml
├── decoders/
│   └── local_decoder.xml
└── screenshots/
├── agents-active.png
├── fim-alerts.png
├── security-events.png
├── active-response.png
└── kill-chain.png

---

## 👨‍💻 Author

**Prabu S**
Security Operations Trainee — Blue Team Alpha
Infotact Solutions CDOC

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue)](https://linkedin.com/in/prabu-cybersecurity-s)

---

*"Trust No One. Verify Everything."*


---

## 🏗️ Architecture
