## Lab Requirements

### Host Machine (Physical Hardware for Virtualization)
- **CPU**: 4–6 cores minimum (8+ cores recommended for smooth concurrent VM execution).
- **RAM**: 12–16 GB minimum (16–24 GB recommended to account for virtualization overhead + Wazuh components).
- **Storage**: 100–120 GB free space (SSD preferred for significantly better indexer performance).
- **OS**: Windows, Linux, or macOS supporting VMware Workstation or VirtualBox.

### Virtualization Software
- **Hypervisor**: VMware Workstation or Oracle VM VirtualBox.
- **BIOS/UEFI**: Ensure Hardware Virtualization (VT-x/AMD-V) is enabled.
- Tip: Enable nested virtualization if needed for advanced features inside VMs.

### Virtual Machines

1. **Wazuh All-in-One Server (Manager + Indexer + Dashboard)**
   - **OS**: Ubuntu Server 22.04 LTS (64-bit).
   - **CPU**: 4 cores (Minimum 2 cores, but 4 recommended for analysis and indexing).
   - **RAM**: 8 GB (Official quickstart recommendation for 1–25 agents).
   - **Storage**: 60–100 GB (SSD recommended; ~50 GB sufficient for 90 days logs with low agent count).

2. **Monitored Endpoint**
   - **OS**: Windows 10 (64-bit, Pro edition recommended for Sysmon).
   - **CPU**: 2 cores.
   - **RAM**: 4 GB.
   - **Storage**: 40 GB.

### Network Configuration
- **Adapter Type**: Host-only (preferred for isolation) or NAT with port forwarding (if access dashboard from host).
- **Connectivity**: All VMs must ping each other and reach Wazuh Manager on:
  - 1514/UDP: Agent log collection
  - 1515/TCP: Agent registration/authentication
  - 55000/TCP: Wazuh API/remote commands
- **IP Addressing**: Static IP for Wazuh Server (e.g., 192.168.56.10) to simplify agent config.
- Tip: Test early – use `telnet <wazuh-ip> 1514` or `nc -zv` from endpoint.

**Note**: Specs tailored for learning lab with 1 endpoint and basic tests (brute-force, PowerShell, malware). High log volumes (full Sysmon config) may require scaling RAM/CPU on Wazuh VM.

**Reference**: [Wazuh Official Quickstart Guide](https://documentation.wazuh.com/current/quickstart.html)
