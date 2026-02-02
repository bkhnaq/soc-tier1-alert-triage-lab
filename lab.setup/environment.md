# Lab Environment

## Overview
This lab simulates a real-world SOC Tier 1 environment using Wazuh SIEM to monitor Windows endpoint activities, generate security alerts, and practice alert triage & escalation.

## Wazuh Deployment
- **Deployment type**: All-in-One (Manager, Indexer, Dashboard on single host)
- **OS**: Ubuntu Server 22.04 LTS (64-bit)
- **Wazuh Version**: 4.14.2 (latest stable release as of February 2026; use the assisted installer script)
- **Components**:
  - Wazuh Manager (analysis & alert generation)
  - Wazuh Indexer (storage & search)
  - Wazuh Dashboard (Kibana-based visualization & querying)

## Monitored Endpoint
- **OS**: Windows 10 (64-bit, Pro recommended for Sysmon)
- **Wazuh Agent**: Installed and active (version matching manager)
- **Agent Name**: win10-endpoint
- **Additional**: Sysmon configured for process creation, network connections, PowerShell logging

## Network Configuration
- **Wazuh Server IP**: 192.168.x.x (static recommended, e.g., 192.168.56.10)
- **Windows Endpoint IP**: 192.168.x.x
- **Network Mode**: Host-only adapter (preferred for isolation) or NAT with port forwarding
- **Key Ports** (ensure open):
  - 1514/UDP: Agent → Manager (log collection)
  - 1515/TCP: Agent registration/auth
  - 55000/TCP: API & remote commands
  - 5601/TCP: Dashboard access (HTTPS)
- Tip: Test connectivity from endpoint to manager before agent install.

## Purpose
- Generate realistic security alerts (brute-force, suspicious PowerShell, malware simulation)
- Perform SOC Tier 1 alert triage (review, filter false positives, manual queries)
- Document investigation steps, findings, and escalation decisions (to Tier 2)

Reference: [Wazuh Quickstart](https://documentation.wazuh.com/current/quickstart.html) | [Installation Guide](https://documentation.wazuh.com/current/installation-guide/index.html)
