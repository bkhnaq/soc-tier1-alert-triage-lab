# Incident Response Playbook: Brute Force Login Attempt

## 1. Alert Information
* **Detection Tool:** Wazuh SIEM
* **Rule ID:** 60122 (Level 10)
* **MITRE ATT&CK:** [T1110 – Brute Force](https://attack.mitre.org/techniques/T1110/)
* **Target Host:** `DESKTOP-JT7B9UV`
* **Log Source:** Windows Security Event Logs (Event ID 4625)

## 2. Investigation Workflow
### 2.1. Logon Type Analysis
Identify the attack vector using the **Logon Type** field:
* **Type 2 (Interactive):** Physical access to the machine.
* **Type 3 (Network):** SMB, IIS, or Shared Folder access.
* **Type 10 (RemoteInteractive):** Remote Desktop Protocol (RDP) attack.

### 2.2. Source & Correlation
* **Source Attribution:** Identify if the Source IP is Internal or External.
* **Error Code Check:**
    * `0xc000006a`: Correct username, wrong password.
    * `0xc0000064`: Non-existent account (Username harvesting).
* **Scope Check:** Check for **Password Spraying** activity across other endpoints.

## 3. Response Actions
### Scenario A: Confirmed Malicious (True Positive)
1. **Block IP:** Blacklist the Source IP on the Edge Firewall/Wazuh Agent.
2. **Account Hardening:** Disable the targeted account temporarily if feasible.
3. **Check for Success:** Look for **Event ID 4624** (Success) following the failures.
4. **Isolate:** If a successful login is confirmed, **Isolate the Host** immediately.

### Scenario B: User Error (False Positive)
1. **Verification:** Confirm with the user/owner regarding password issues.
2. **Documentation:** Close the alert and document as a False Positive.

## 4. Escalation Criteria
Escalate to **Tier 2** if:
* Successful login (Event 4624) is detected after brute force.
* Targeted user is a **Domain Admin** or **System Account**.
* Attack originates from a known malicious C2 IP.

---
**Status:** Active | **Version:** 1.0 | **Analyst:** Khang Bao (Elon)
