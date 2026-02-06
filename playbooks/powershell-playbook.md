# Incident Response Playbook: Suspicious PowerShell Activity

## 1. Alert Information
* **Detection Tool:** Wazuh SIEM
* **Rule ID:** 61603 / 61613 (Level 12 - High)
* **MITRE ATT&CK Mapping:** [T1059.001 – PowerShell](https://attack.mitre.org/techniques/T1059/001/)
* **Target Host:** `DESKTOP-JT7B9UV` (Windows 10)
* **Process:** `powershell.exe`
* **Log Source:** Windows Security Event Log (Event ID 4688)

---

## 2. Initial Triage (Tier 1 Analysis)
### 2.1. Rule Validation
* **Process Verification:** Confirm the process is indeed `powershell.exe` and not a masqueraded binary (e.g., `powerrshell.exe`).
* **Timestamp Check:** Verify if the execution occurred during non-business hours or follows a suspicious login.
* **Privilege Level:** Check if the process was started with **Elevated Privileges** (Token Elevation Type).

---

## 3. Investigation Steps
### 3.1. Command Line Analysis (Critical)
Analyze the command line for obfuscation or malicious intent:
* **Suspicious Flags:** * `-EncodedCommand` or `-e`: Used to hide script logic.
    * `-ExecutionPolicy Bypass`: Used to run restricted scripts.
    * `-WindowStyle Hidden` or `-w hidden`: Stealth execution.
    * `-NoProfile`: Skips user profile scripts to evade detection.
* **Download Cradles:** Search for strings like `IEX`, `Invoke-Expression`, `WebClient`, or `DownloadString`.

### 3.2. Parent Process Tree Analysis
Determine the origin of the execution:
* **Low Risk:** `explorer.exe`, `services.exe` (if verified admin activity).
* **Medium Risk:** `cmd.exe`, `taskeng.exe`.
* **High Risk:** `winword.exe`, `excel.exe`, `outlook.exe` (Potential Phishing/Macro).
* **Critical Risk:** `sqlservr.exe`, `w3wp.exe` (Web Shell / Database compromise).

### 3.3. Network Correlation
* Check for active network connections from the PowerShell PID to external/unknown IPs.
* Verify DNS queries for suspicious domains initiated by the script.

---

## 4. Response Actions

### Scenario A: Confirmed Malicious (True Positive)
1. **Host Isolation:** Immediately isolate the endpoint via Wazuh Active Response to block Command & Control (C2) communication.
2. **Process Termination:** Kill the malicious `powershell.exe` PID and its parent process.
3. **Forensic Collection:** Capture a memory dump of the PowerShell process for Tier 2 analysis.
4. **Account Lockdown:** Disable the user account involved if it shows signs of compromise.

### Scenario B: Authorized Admin Activity (False Positive)
1. **Verification:** Confirm with the IT/Admin team if the script is part of a scheduled task or legitimate maintenance.
2. **Whitelisting:** If the activity is recurring and safe, suggest tuning the Wazuh rule to exclude this specific authorized command.

---

## 5. Escalation Criteria
Escalate to **Tier 2** if:
* The command line contains an **EncodedCommand** that requires decoding.
* The parent process is a web server or an MS Office application.
* Evidence of **Lateral Movement** (PowerShell Remoting/WinRM) is detected.
* Persistence mechanisms (Scheduled Tasks/Registry Keys) were created.

---

## 6. Recommendations & Mitigation
* **Logging:** Ensure **PowerShell Script Block Logging (Event ID 4104)** is enabled via GPO for full visibility.
* **Constrained Language Mode:** Implement PowerShell Constrained Language Mode where possible.
* **AppLocker:** Use AppLocker or Windows Defender Application Control (WDAC) to restrict PowerShell access to authorized users only.

---
**Analyst:** Khang Bao (Elon) | **Department:** SOC Tier 1 | **Status:** Escalated to Tier 2 – Pending Deep Analysis
