# Incident Playbook: Correlation & Escalation – High-Volume Brute Force

**Incident ID**: SOC-2026-004  
**Date**: April 2026  
**MITRE ATT&CK**: T1110 (Brute Force), T1110.001 (Password Guessing)  
**Severity**: Critical  
**Playbook Owner**: Project SOC Alerts Lab

## 1. Detection
- **Initial Trigger**: Suricata rule `sid:1000002` (SSH Brute Force Attempt)
- **Wazuh Rule**: `100102` (Level 10) fired on individual attempts
- **Correlation Rule**: `100110` (Level 12) – 5+ brute-force attempts within 120 seconds

## 2. Analysis
- **Source IP**: `192.168.56.105`
- **Target Service**: SSH on Linux Endpoint (port 22)
- **Pattern**: Rapid failed login attempts using common usernames/passwords
- **Business Impact**: High risk of credential compromise in a fintech environment handling sensitive customer data

**Evidence**:
- Wazuh correlation alert
- Timeline view in Wazuh/Kibana dashboard

## 3. Containment
- **Automated Action**: Custom Active Response script (`suricata-block-ip.py`) blocked the IP
- **Timeout Strategy**: Initial 300 seconds → escalated to 15–60 minutes via `repeated_offenders`
- **Defense-in-Depth**: iptables DROP rule applied on the affected endpoint

## 4. Eradication
- Reviewed SSH logs on Linux Endpoint
- Confirmed no successful login occurred
- Checked for any backdoors or persistence created during the attack window

## 5. Recovery
- IP automatically unblocked after escalated timeout
- Strengthened SSH security recommendations (key-based auth, fail2ban, port knocking)
- Updated monitoring rules to lower threshold for similar patterns

## Lessons Learned
- Frequency-based correlation rules dramatically improve detection of automated attacks.
- Stateful Active Response with escalating timeouts balances security and operational continuity.
- Combining Suricata network visibility with Wazuh host-level rules creates powerful defense layers.

**Screenshots**:
- `../screenshots/correlation-alert.png` (placeholder)
- `../screenshots/active-response-block.png`
- `../dashboards/alert-timeline.png`

**Related Rules**:
- Suricata: `sid:1000002`
- Wazuh: `100102`, `100110`
