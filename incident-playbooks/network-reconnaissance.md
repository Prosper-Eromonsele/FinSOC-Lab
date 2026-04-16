# Incident Playbook: Network Reconnaissance Attack

**Incident ID**: SOC-2026-002  
**Date**: April 2026  
**MITRE ATT&CK**: T1595 (Active Scanning), T1595.001 (Scanning IP Blocks)  
**Severity**: High  
**Playbook Owner**: Project SOC Alerts Lab

## 1. Detection
- **Suricata Rule**: `sid:1000001` – "Project Alert SOC: ICMP Ping Sweep Detected"
- **Wazuh Rule**: `100101` (Level 7) – Escalated reconnaissance alert
- **Trigger**: Multiple ICMP echo requests from a single source IP within 10 seconds
- **Source**: Kali Attacker VM (simulated external threat actor)

## 2. Analysis
- **Source IP**: `192.168.56.105` (Kali VM)
- **Destination**: Lab network subnet (`$HOME_NET`)
- **Indicators**: High volume of ICMP type 8 packets
- **Context**: Typical initial reconnaissance phase before more targeted attacks (e.g., port scanning or brute-force)
- **Correlation**: No prior alerts from this IP in the last 24 hours

**Evidence**:
- Suricata `eve.json` entry
- Wazuh Security Events dashboard screenshot (see `../screenshots/`)

## 3. Containment
- **Automated Action**: Wazuh Active Response (`suricata-block-ip.py`) triggered
- **Action Taken**: IP added to iptables DROP rule for 300 seconds (5 minutes)
- **Escalation**: If repeated, timeout increases to 15 minutes via `repeated_offenders`
- **Manual Verification**: `sudo iptables -L -n -v` confirmed block

## 4. Eradication
- Reviewed Wazuh agent logs on Linux Endpoint
- Confirmed no successful follow-on attacks (no SSH or web attempts from the blocked IP)
- No malware or persistence mechanisms detected

## 5. Recovery
- IP automatically unblocked after timeout
- Continued monitoring for 1 hour post-incident
- Updated Suricata rule threshold if false positives are observed in production

## Lessons Learned
- Early detection of reconnaissance significantly reduces dwell time.
- Combining Suricata network visibility with Wazuh host correlation provides strong defense-in-depth.
- Consider implementing network segmentation for production fintech environments.

**Screenshots**:
- `../screenshots/suricata-eve-log.png`
- `../screenshots/active-response-block.png`
- `../screenshots/full-incident-flow.png`

**Related Rules**:
- Suricata: `sid:1000001`, `sid:1000005`
- Wazuh: `100101`, `100103`
