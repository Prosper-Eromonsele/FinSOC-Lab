# Incident Playbook: Web Application Attack Attempt

**Incident ID**: SOC-2026-003  
**Date**: April 2026  
**MITRE ATT&CK**: T1190 (Exploit Public-Facing Application)  
**Severity**: Critical  
**Playbook Owner**: Project SOC Alerts Lab

## 1. Detection
- **Suricata Rule**: `sid:1000003` – "Project Alert SOC: Suspicious Admin/Login Page Access"
- **Wazuh Rule**: `100104` (Level 11) – High-severity web attack alert
- **Trigger**: HTTP request containing `/admin` or `/login` URI from external source

## 2. Analysis
- **Source IP**: `192.168.56.105` (Kali Attacker VM)
- **Target**: Simulated fintech web portal on Linux Endpoint
- **Indicators**: Multiple rapid requests to sensitive paths (potential credential stuffing or directory brute-forcing)
- **Risk**: Could lead to account takeover or data breach in a real fintech environment

**Evidence**:
- Suricata HTTP logging in `eve.json`
- Wazuh alert with full request details

## 3. Containment
- **Automated Action**: Wazuh Active Response (`suricata-block-ip.py`) immediately blocked the source IP
- **Duration**: Initial 300 seconds (5 minutes), with escalation on repeat attempts
- **Additional Layer**: Suricata rule could be upgraded to `drop` action in IPS mode for inline prevention

## 4. Eradication
- Inspected Linux Endpoint web server logs
- Confirmed no successful authentication or payload delivery
- Checked for any unauthorized files or processes

## 5. Recovery
- IP automatically removed from blocklist after timeout
- Enhanced monitoring rule added for similar patterns
- Recommended: Implement Web Application Firewall (WAF) and rate limiting in production

## Lessons Learned
- Web-facing applications are high-value targets in fintech.
- Combining signature-based detection (Suricata) with SIEM correlation (Wazuh) catches attacks early.
- Active Response provides critical time to investigate without manual intervention.

**Screenshots**:
- `../screenshots/web-attack-alert.png` (placeholder – replace with actual)
- `../screenshots/active-response-block.png`
- `../dashboards/kibana-suricata-correlation.png`

**Related Rules**:
- Suricata: `sid:1000003`
- Wazuh: `100104`
