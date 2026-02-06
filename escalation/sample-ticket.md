
## Incident Escalation Ticket: [INC-2026-0042]
1. Incident Overview
Title: Suspicious PowerShell Execution with Encoded Command

Status: Escalated to Tier 2

Severity: <span style="color:red">High</span> (Due to potential Persistence/C2 activity)

Detection Tool: Wazuh SIEM

Timestamp: 2026-02-06 23:45:10 (UTC +7)

2. Alert Information
Rule ID: 61603 (Level 12 - High)

Rule Description: PowerShell executed with suspicious command line arguments.

MITRE ATT&CK: T1059.001 (Command and Scripting Interpreter: PowerShell)

Affected Host: DESKTOP-JT7B9UV (Finance Department)

User: LocalAdmin

3. Evidence & Investigation (Tier 1)
Process Tree: explorer.exe (PID: 2450) -> powershell.exe (PID: 8812)

Event ID: 4688 (Process Creation)

Command Line: powershell.exe -ExecutionPolicy Bypass -WindowStyle Hidden -EncodedCommand JABzAD0ATgBlAHcALQBPAGIAagBlAGMAdAAgAEkATwAu...

Investigation Notes:

Context: Execution occurred outside of standard business hours (11:45 PM).

User Verification: No scheduled maintenance or Change Request (CR) recorded for this period.

Anomaly: The use of -EncodedCommand and -WindowStyle Hidden is a common technique for evading detection.

4. Tier 1 Assessment
The activity is deemed highly suspicious.

Initial check on the source IP of the host shows an outbound connection attempt to an unidentified external IP (185.x.x.x) immediately after script execution.

The script appears to be trying to establish a reverse shell or download a second-stage payload.

5. Actions Taken & Recommendations
Action Taken: Host DESKTOP-JT7B9UV has been isolated via Wazuh agent to prevent lateral movement.

Recommendation for Tier 2: 1. Decode the Base64 command to identify the full intent of the script. 2. Perform memory forensics on PID 8812. 3. Scan the file system for persistence (Registry keys, Scheduled tasks).
