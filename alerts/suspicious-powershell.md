# Security Alert: Suspicious PowerShell Activity (Post-Login)

## 1. Alert Information
* **Detection Tool:** Wazuh SIEM
* **Rule ID:** 18107 (Level 12 - High)
* **MITRE ATT&CK Mapping:** [T1059.001 – PowerShell](https://attack.mitre.org/techniques/T1059/001/)
* **Affected Asset:** `Windows 10` (DESKTOP-JT7B9UV)
* **User:** `Local User`
* **Process:** `powershell.exe`

---

## 2. Incident Context
This alert is highly critical as it was detected **immediately following a successful brute-force login**. The use of PowerShell in this context strongly indicates an attacker attempting to establish persistence or execute a malicious payload.

## 3. Evidence & Investigation
* **Event ID:** 4688 (Process Creation)
* **Technical Observation:** PowerShell executed with obfuscation flags.
* **Visual Proof:**

![Suspicious Powershell Evidence](../screenshots/suspicious-powershell-after-success-login.png)

* **Key Indicators Found:**
    * `-EncodedCommand`: Used to obfuscate the script's intent.
    * `-ExecutionPolicy Bypass`: Used to circumvent restricted execution settings.



## 4. Analyst Assessment
* **Classification:** **True Positive (TP) - Post-Exploitation Activity**.
* **Analysis:** The timing of this process creation (Post-Success Login) suggests the attacker is using automated scripts to download secondary malware or scan the internal network (Discovery).

## 5. Response Actions
1. **Kill Process:** Terminated the suspicious `powershell.exe` process tree.
2. **Persistence Check:** Audited Scheduled Tasks and Registry Run keys for any newly created entries.
3. **Full System Scan:** Initiated a deep malware scan on the affected host.
4. **Log Retention:** Exported all PowerShell operational logs (Event ID 4104) for script de-obfuscation and further analysis.

---
**Analyst:** Khang Bao (Elon)
**Incident Status:** **Escalated for Forensics**
**Date:** 2026-02-06
