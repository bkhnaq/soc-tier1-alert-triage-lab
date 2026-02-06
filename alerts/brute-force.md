## Alert: Brute Force Login Attempt

- Detection Tool: Wazuh
- Rule ID: 60204
- Rule Level: High (10)
- Affected Host: DESKTOP-JT7B9UV (Windows 10)
- User: PC1
- Source IP: Not available (local authentication)

### Description
Multiple failed Windows logon attempts (Event ID 4625) were detected
within a short time period on the same host.

The repeated authentication failurs triggered a correlated Wazuh alert
indicating a potential brute force login attempt.

### Evidence
- Windows Security Event ID: 4625 (Logon Failure)
- Multiple events detected within minutes
- Same target username and workstation

### MITRE ATT&CK
- T1110 – Brute Force

