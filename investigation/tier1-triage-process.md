
# SOC Tier 1: Incident Triage & Analysis Process

This document outlines the standard operating procedure (SOP) for Tier 1 Analysts to validate, investigate, and respond to security alerts.

---

## Phase 1: Alert Reception & Validation
* **Alert Source:** Monitor central dashboards (Wazuh SIEM) for new security events.
* **Integrity Check:** Verify the authenticity of the alert and ensure it is not a system misconfiguration or testing activity.
* **Severity Assignment:** Re-evaluate alert severity based on the asset’s importance (e.g., Finance Dept vs. Test Lab).

## Phase 2: Initial Investigation (Triage)
* **Context Gathering:** * Identify the **Affected Host** (Hostname/IP) and **User Account**.
    * Analyze **Logon Types** (e.g., Type 2 Interactive vs. Type 10 RDP).
* **Evidence Collection:** Extract raw logs (Event ID 4625 for Brute Force, 4688 for Process Creation).
* **Correlation:** Check if the Source IP or User has triggered other alerts across the network (e.g., Password Spraying or Lateral Movement).

## Phase 3: Classification
* **True Positive (TP):** Confirmed malicious activity that requires immediate response.
* **False Positive (FP):** Authorized administrative activity or known benign user error. Close with documentation.
* **Suspicious:** Potential threat requiring deeper analysis; proceed to Phase 4 or 5.

## Phase 4: Initial Containment (Action)
* **Host Isolation:** Isolate compromised endpoints via Wazuh agent to stop C2 communication.
* **Account Hardening:** Temporarily disable accounts showing signs of compromise.
* **IP Blocking:** Blacklist malicious external IPs on the firewall.

## Phase 5: Escalation Criteria
Escalate to **Tier 2 / Incident Response Lead** if:
1. **Critical Success:** A brute force attack results in a successful login (Event 4624).
2. **High-Value Target:** Targeted accounts are Domain Admins or Service Accounts.
3. **Advanced Persistence:** Detection of obfuscated PowerShell scripts or new registry keys/scheduled tasks.
4. **Out of Scope:** Investigation requires deep memory forensics or malware reverse engineering.

---
**Standardized by:** Khang Bao (Elon)  
**Role:** SOC Analyst Tier 1  
**Last Updated:** 2026-02-06
