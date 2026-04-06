# 🛡️ Sentient Shield — Enterprise EDR & Threat Hunting Grid

![Wazuh](https://img.shields.io/badge/Wazuh-4.7.5-blue)
![Status](https://img.shields.io/badge/Status-Active-green)
![Platform](https://img.shields.io/badge/Platform-Linux%20%7C%20Windows-lightgrey)
![MITRE](https://img.shields.io/badge/MITRE-ATT%26CK-red)

> **Project 2 — Infotact Solutions CDOC (Blue Team Alpha)**  
> Built a centralized, real-time SOC EDR grid using Wazuh SIEM to detect 
> threats, monitor file integrity, and map adversary tactics to MITRE ATT&CK.

---

## 📌 Project Overview

| Field | Details |
|---|---|
| **Project Name** | Sentient Shield |
| **Organization** | Infotact Solutions — CDOC |
| **Team** | Blue Team Alpha |
| **Role** | Security Operations Trainee |
| **Duration** | 4 Weeks |
| **Status** | Weeks 1 & 2 Complete ✅ |

---

## 🎯 Problem Statement

Infotact's servers are under constant brute-force and ransomware attacks.
The organization needed a centralized, real-time system to:
- Detect file integrity violations
- Monitor critical registry keys
- Map adversary tactics to MITRE ATT&CK
- Execute automated active response actions

---
┌───────────────────────────────────────────────┐
│              VIRTUALBOX LAB                   │
│                                               │
│  ┌───────────────────┐  ┌──────────────────┐  │
│  │  Wazuh Manager    │  │ Windows Server   │  │
│  │  Ubuntu 22.04     │  │  2019 Eval       │  │
│  │  IP:192.168.56.104│  │ IP:192.168.56.107 │ │
│  │  - SIEM Backend   │  │  - Wazuh Agent   │  │
│  │  - Rules Engine   │  └──────────────────┘  │
│  │  - Dashboard      │  ┌──────────────────┐  │
│  └───────────────────┘  │  Linux WebServer │  │
│                         │  Ubuntu 24.04    │  │
│                         │  - Wazuh Agent   │  │
│                         │  - Apache/Nginx  │  │
│                         └──────────────────┘  │
└───────────────────────────────────────────────┘

## 🏗️ Architecture

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| **Wazuh 4.7.5** | SIEM/EDR Platform |
| **VirtualBox** | Virtualization |
| **Ubuntu 22.04/24.04** | Linux Endpoints |
| **Windows Server 2019** | Windows Endpoint |
| **OpenSearch** | Log Indexing |
| **Wazuh Dashboard** | Visualization |

---

## 📅 Sprint Progress

### ✅ Week 1 — Infrastructure & Agent Deployment

**Objective:** Deploy Wazuh Manager and connect all agents

**What I Did:**
- Deployed Wazuh Manager on Ubuntu using all-in-one installer
- Configured Host-Only network for isolated lab environment
- Deployed Wazuh agents on Linux Web Server and Windows Server
- Verified 100% agent coverage with Active status

**Gate Check Result:** ✅ PASSED

Agent 001: Windows-Server  → Active ✅
Agent 002: Linux-WebServer → Active ✅
Coverage: 100%

---

### ✅ Week 2 — Detection Rules & Logic

**Objective:** Configure FIM, custom rules, and vulnerability detection

#### 🔍 File Integrity Monitoring (FIM)
- Configured real-time monitoring on critical directories:
  - `/etc` — System configuration
  - `/usr/bin` — System executables  
  - `/usr/sbin` — System admin tools
  - `/var/www/html` — Web application files
- Uses Linux **inotify** for instant detection
- Alerts generated within **5 seconds** of file change

**Gate Check Result:** ✅ PASSED

Alert: /etc/fim_test_file — File added    Level 5 ✅
Alert: /etc/fim_test_file — Modified     Level 7 ✅


#### 📝 Custom Decoder & Rules
- Wrote custom XML decoder for proprietary application logs
- Created detection rules mapped to MITRE ATT&CK:

| Rule ID | Level | Description | MITRE |
|---|---|---|---|
| 100005 | 6 | Authentication failure detected | T1110 |
| 100006 | 10 | Brute force attack detected | T1110.001 |

#### 🔒 Vulnerability Detector
- Enabled automated CVE scanning on all agents
- Configured feeds: Canonical (Ubuntu) + NVD (Windows)
- Scan interval: 5 minutes (lab) / 6 hours (production)

---

## 📊 Dashboard Screenshots

> *(Add your screenshots here)*

### Agents Overview
![Agents](screenshots/agents.png)

### FIM Alerts
![FIM](screenshots/fim.png)

### Security Events
![Events](screenshots/events.png)

---

## 🗂️ Repository Structure
Sentient-Shield/
│
├── README.md
├── configs/
│   ├── agent-ossec.conf        # Agent configuration
│   ├── manager-ossec.conf      # Manager configuration
│   └── vulnerability-detector.conf
├── rules/
│   └── local_rules.xml         # Custom detection rules
├── decoders/
│   └── local_decoder.xml       # Custom log decoders
└── screenshots/
├── agents.png
├── fim.png
└── events.png

---

## 🎯 MITRE ATT&CK Coverage

| Technique | ID | Detection Method |
|---|---|---|
| Brute Force | T1110 | Custom Rule 100005 |
| Password Guessing | T1110.001 | Custom Rule 100006 |
| Data Manipulation | T1565 | FIM Monitoring |
| File Deletion | T1107 | FIM Real-time |

---

## 📈 Coming Next

- ⬜ Week 3: Active Response — Auto-ban brute force IPs
- ⬜ Week 4: Threat Simulation — Atomic Red Team

---

## 👨‍💻 Author

**Prabu**  
Security Operations Trainee — Blue Team Alpha  
Infotact Solutions CDOC  

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue)](https://www.linkedin.com/in/prabu-cybersecurity-s)

---

*"Trust No One. Verify Everything."*
