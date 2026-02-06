# SOC-Detection-and-Alert-Triage-Lab

## 📌 Project Overview
This project demonstrates a comprehensive **SOC Tier 1 Alert Triage Workflow** using the Wazuh SIEM/EDR platform. The lab simulates real-world attack scenarios, including Brute Force attacks and malicious PowerShell execution, followed by a structured incident response and escalation process.

The goal is to showcase the ability to validate alerts, perform deep-dive investigations using Windows Event Logs, and execute containment actions.

---

## 🏗️ System Architecture
The lab is built on a **Wazuh All-in-One deployment** hosted on an Ubuntu Server. While co-located for lab purposes, the architecture reflects a logically separated production design:

* **Wazuh Manager:** The engine responsible for log analysis, file integrity monitoring, and active response.
* **Wazuh Indexer:** A highly scalable full-text search and analytics engine to store and index security events.
* **Wazuh Dashboard:** The visualization layer for alert monitoring and incident management.
* **Endpoints:** Windows 10 workstations equipped with Wazuh Agents for real-time telemetry collection.

[Image of Wazuh SIEM architecture and data flow]

---

## 🛡️ Core Competencies Demonstrated
* **SIEM Monitoring:** Real-time alert monitoring and severity assessment.
* **Log Analysis:** Investigating Windows Event IDs (4625 - Failed Logon, 4624 - Success Logon, 4688 - Process Creation).
* **Threat Hunting:** Identifying attack patterns like **T1110 (Brute Force)** and **T1059.001 (PowerShell)**.
* **Incident Response:** Executing Tier 1 triage, host isolation, and account hardening.
* **Documentation:** Creating professional Playbooks and Escalation Tickets for Tier 2/SOC Leads.

---

## 📂 Project Structure
* `SOC-Documentation/`
    * [`tier1-triage-process.md`](./tier1-triage-process.md): Standard Operating Procedure (SOP) for alert validation.
    * [`Brute-Force-Playbook.md`](./Brute-Force-Playbook.md): Step-by-step response guide for credential attacks.
* `Case-Studies/`
    * [`Brute-Force-Case-Study.md`](./Brute-Force-Case-Study.md): Detailed analysis from initial failures to successful compromise.
    * [`Suspicious-PowerShell-Alert.md`](./Suspicious-PowerShell-Alert.md): Post-exploitation detection using command-line analysis.
* `Screenshots/`: Visual evidence from the Wazuh Dashboard.

---

## 🚀 Attack Scenario & Triage Workflow

### Scenario: The "Full Kill Chain" Attack
1.  **Initial Access:** Attacker initiates an RDP Brute Force attack against `DESKTOP-JT7B9UV`.
2.  **Compromise:** Attacker successfully guesses the password for `testuser`.
3.  **Persistence/Execution:** Attacker executes an **Encoded PowerShell** command to download a second-stage payload.

[Image of Cyber Kill Chain stages]

### Triage Actions Taken:
* **Detection:** Wazuh triggered Level 10 & 12 alerts for repeated failures followed by a success.
* **Analysis:** Analyzed **Logon Type 3** and decoded suspicious PowerShell flags (`-EncodedCommand`, `-ExecutionPolicy Bypass`).
* **Containment:** Performed **Host Isolation** via Wazuh agent to sever the attacker's connection.
* **Escalation:** Drafted a formal Incident Ticket for Tier 2 forensics.

---

## 🛠️ Lab Setup & Tools
* **Platform:** Wazuh v4.x (All-in-One)
* **OS:** Ubuntu 22.04 LTS (Server), Windows 10 (Target)
* **Log Sources:** Windows Security Event Logs, Sysmon
* **Frameworks:** MITRE ATT&CK, NIST Incident Response Framework

---

## ⚠️ Lab Limitations
- Single endpoint environment (no lateral movement simulation)
- No SOAR integration (manual response actions)
- Limited attack diversity (credential-based attacks only)

---

## 👤 Author
**Khang Bao (bkhnaq)**
* **Role:** Aspiring SOC Analyst / 3rd Year IT Student
* **Interests:** Cybersecurity, SIEM/EDR, Malware Analysis
* **Contact:** lebaokhang22092005@gmail.com

---
*This lab is for educational purposes only. All attacks were performed in a controlled environment.*
