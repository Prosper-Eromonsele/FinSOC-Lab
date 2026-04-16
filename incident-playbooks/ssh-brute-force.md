# Incident Playbook: SSH Brute-Force Attack

**Incident ID**: SOC-2026-001  
**NIST Phase**: Detection → Analysis → Containment → Eradication → Recovery

## Detection
- Suricata rule 1000002 triggered
- Wazuh rule 100102 (level 10) fired

## Analysis
- Source IP: [attacker IP]
- Multiple failed login attempts in 30 seconds
- MITRE ATT&CK: T1110 (Brute Force)

## Containment
- Wazuh Active Response (suricata-block-ip.py) automatically blocked the IP for 300 seconds
- Escalation to 15 minutes on repeat offense

## Eradication
- Reviewed endpoint logs
- Confirmed no successful compromise

## Recovery
- IP unblocked after timeout
- Monitored for recurrence
- Updated rules if false positive

**Screenshots**: See ../screenshots/

**Lessons Learned**: Enable fail2ban as secondary layer.
