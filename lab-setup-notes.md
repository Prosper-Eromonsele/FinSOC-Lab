# Quick Lab Setup Notes

## Prerequisites
- 16 GB RAM laptop
- Oracle VirtualBox 7.x
- Ubuntu 24.04 LTS ISO
- Windows 11 ISO 
- Kali Linux ISO

## Fast Start
1. Clone this repo
2. Read SETUP-HANDBOOK.md for full 10-phase build
3. Start with Phase 1 (VM creation) to phase 9
4. Use detection-rules/ and active-response/ files directly

## Common Commands
- Wazuh status: `sudo systemctl status wazuh-manager`
- Suricata: `sudo systemctl status suricata`
- Active Response log: `tail -f /var/ossec/logs/active-responses.log`

For issues, open an Issue or check screenshots/.
