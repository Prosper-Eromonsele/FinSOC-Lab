# Lab Architecture

## Overview
This is a single-laptop enterprise-simulated SOC for a fictional Nigerian fintech.

### Components
- **Wazuh All-in-One Server** (8 GB): Central SIEM, rule engine, dashboard
- **Linux Endpoint** (3-4 GB): Suricata NIDS/IPS + Wazuh agent
- **Windows Endpoint** (4 GB): Host-based detection
- **Kali Attacker** (2-3 GB): Safe simulation platform

### Data Flow
Kali → Network traffic → Suricata (eve.json) → Wazuh Agent → Wazuh Server → Custom Rules → Active Response (Python script → iptables/nftables) → Optional Logstash → Elasticsearch + Kibana

![Architecture](architecture-diagram.png)

## Key Design Decisions
- Single-node Wazuh for lab realism and performance on 16 GB RAM
- Custom Python Active Response for better Suricata field handling
- ELK forwarding for advanced correlation and visualization
