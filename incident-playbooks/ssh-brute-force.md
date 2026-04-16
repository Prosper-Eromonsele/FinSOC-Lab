# Incident Playbook: SSH Brute-Force Attack (FinSOC Lab)

**Incident ID**: SOC-2026-001  
**Date**: April 2026  
**MITRE ATT&CK**: T1110 (Brute Force), T1110.001 (Password Guessing)  
**Severity**: High  
**Playbook Owner**: Project SOC Alerts Lab

## 1. Detection
- **Suricata Rule**: `sid:1000002` – "Project Alert SOC: SSH Brute Force Attempt"
- **Wazuh Rule**: `100102` (Level 10) – SSH brute-force escalation
- **Trigger**: 5+ failed SSH login attempts within 30 seconds from a single source IP
- **Source**: Kali Attacker VM simulating external threat actor

## 2. Analysis
- **Source IP**: `192.168.56.105` (Kali VM)
- **Target**: SSH service (port 22) on Linux Endpoint
- **Indicators**: Rapid authentication failures with common usernames (admin, root, etc.)
- **Business Context**: High risk in a fintech environment where SSH is used for server management
- **Correlation**: No successful login occurred; attack was caught in early stage

**Evidence**:
- Suricata `eve.json` alert
- Wazuh Security Events with full log details

## 3. Containment
- **Automated Action**: Wazuh Active Response triggered `suricata-block-ip.py`
- **Action Taken**: Attacker IP added to iptables DROP chain for initial 300 seconds (5 minutes)
- **Escalation**: Repeated attempts trigger longer blocks (15 min → 60 min) via `repeated_offenders`
- **Verification**: `sudo iptables -L -n -v` confirmed the block

## 4. Eradication
- Reviewed `/var/log/auth.log` on Linux Endpoint
- Confirmed no successful compromise or persistence
- Checked for any unauthorized SSH keys or user accounts

## 5. Recovery
- IP automatically unblocked after timeout period
- Enhanced monitoring enabled for SSH service
- Recommended production controls: SSH key-only authentication, fail2ban, and non-standard port

## Lessons Learned
- Early network-level detection (Suricata) combined with SIEM correlation (Wazuh) stops brute-force attacks before they succeed.
- Custom Active Response scripting provides fast, reliable containment without manual intervention.
- Stateful timeout escalation prevents persistent attackers while avoiding permanent lockouts.

**Screenshots**:
- `../screenshots/active-response-block.png`
- `../screenshots/suricata-eve-log.png`
- `../dashboards/alert-timeline.png`

**Related Rules**:
- Suricata: `sid:1000002`
- Wazuh: `100102`, `100110` (correlation rule)
