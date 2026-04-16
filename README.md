# FinSOC-Lab
Enterprise-grade virtual SOC lab simulating a Nigerian fintech environment using Wazuh, Suricata, custom Active Response, and ELK Stack. Built to demonstrate real-world SIEM, NIDS, and automated incident response skills.
# 🚨 FinSOC Lab

**Enterprise Virtual Security Operations Center (SOC) for Fintech**  
**Built to demonstrate real-world SIEM, NIDS, and Automated Response capabilities**

![Wazuh](https://img.shields.io/badge/Wazuh-4.14.4-00A1E6)  
![Suricata](https://img.shields.io/badge/Suricata-8.0.4-FF0000)  
![ELK Stack](https://img.shields.io/badge/ELK-Stack-005571)  
![VirtualBox](https://img.shields.io/badge/Hypervisor-VirtualBox-2C3E50)  
**Lagos, Nigeria • April 2026**

---

### 🎯 Why This Project Stands Out

**FinSOC Lab** is a complete, production-grade virtual SOC simulating a Nigerian fintech environment.  

It showcases the exact practical skills hiring managers look for in SOC Analyst and Junior SOC Engineer roles:

- End-to-end threat lifecycle: Detection → Correlation → Automated Containment  
- Deep Suricata NIDS integration with Wazuh SIEM  
- Custom Python Active Response scripting for real automated blocking  
- ELK Stack integration for advanced Kibana analytics  
- NIST-aligned incident response playbooks with full documentation  

This is a **professional-grade SOC simulation**, not a basic home lab.

---

### 🏗️ Architecture

![Architecture Diagram](architecture-diagram.png)

**Core Components**:
- **Wazuh All-in-One Server** – Central SIEM (Manager + Indexer + Dashboard)
- **Linux Endpoint** – Suricata NIDS/IPS + Wazuh agent
- **Windows Endpoint** – Host-based detection
- **Kali Attacker VM** – Safe attack simulation
- **ELK Stack** – Advanced visualization and correlation layer

**Flow**: Attacker → Suricata (`eve.json`) → Wazuh Agent → Wazuh Server → Custom Rules → Active Response (`suricata-block-ip.py`) → Kibana

---

### ✨ Key Features

- Custom Suricata rules tailored for fintech threats (brute-force, reconnaissance, web attacks)
- Wazuh custom rules with MITRE ATT&CK mapping and correlation logic
- Robust custom Active Response Python script with iptables/nftables fallback and logging
- ELK Stack integration via Logstash for richer dashboards
- Stateful timeout strategies with repeated offender escalation
- Four fully documented NIST-based incident playbooks

---

### 📂 Repository Contents

| Folder                    | Content |
|---------------------------|-------|
| `detection-rules/`        | Custom Suricata & Wazuh rules |
| `active-response/`        | Production-ready Python Active Response script |
| `elk-integration/`        | Logstash pipeline configuration |
| `incident-playbooks/`     | 4 complete NIST incident playbooks |
| `dashboards/`             | Wazuh + Kibana dashboard screenshots |
| `screenshots/`            | Detection and response evidence |

---

### 📋 Incident Playbooks

- [SSH Brute-Force Attack](incident-playbooks/ssh-brute-force.md)
- [Network Reconnaissance Attack](incident-playbooks/network-reconnaissance.md)
- [Web Application Attack Attempt](incident-playbooks/web-application-attack.md)
- [Correlation & Escalation – High-Volume Brute Force](incident-playbooks/correlation-escalation.md)

---

### 🚀 Quick Start

1. Clone the repository
2. Follow `SETUP-HANDBOOK.md` for the complete 10-phase build guide
3. Recommended: 16 GB RAM laptop with Oracle VirtualBox
4. Full lab setup time: 4–6 hours

**Live Demo Video** → [Watch 4-minute full incident walkthrough](https://youtu.be/YOUR-UNLISTED-LINK) *(replace with your video)*

---

### 📊 Lab Results

- **SSH Brute-Force**: Detected by Suricata → Correlated in Wazuh → IP auto-blocked in under 8 seconds
- **Network Reconnaissance**: Early ICMP ping sweep detected and contained
- **Web Application Attack**: Suspicious admin portal access blocked automatically
- **Correlation Rule**: High-volume attacks escalated with longer timeouts

---

### 💼 How This Prepares Me for Your SOC Team

- Hands-on experience operating a real SIEM + NIDS environment
- Custom rule writing, tuning, and correlation skills
- Implementation of automated response and SOAR concepts
- Professional incident documentation using NIST framework
- Visualization and analytics using both Wazuh and ELK Stack

**Ready to contribute from Day 1** in a Lagos or remote SOC role.

---

### 📬 Connect

- **LinkedIn**: [Your Profile Link]
- **Email**: [your.email@domain.com]

**Built in Lagos with ❤️ for the next generation of Nigerian cybersecurity professionals.**

⭐ Star this repo if it helped your SOC journey!

**Topics**: wazuh, suricata, soc, siem, active-response, elk-stack, cybersecurity-lab, incident-response, mitre-attack, threat-detection, fintech-security, lagos-tech, portfolio-project
