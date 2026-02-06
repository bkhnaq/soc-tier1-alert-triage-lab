
# Incident Response Playbook – Brute Force Login Attempt

## Alert Information
- Detection Tool: Wazuh
- Rule ID: 60122
- Rule Level: Medium
- MITRE ATT&CK: T1110 – Brute Force
- Affected Host: DESKTOP-JT7B9UV (Windows 10)
- User: Local User
- Log Source: Windows Security Event Logs

---

## Alert Description
This alert is triggered when multiple failed login attempts are detected
within a short time period.

Brute force attacks are commonly used by attackers to gain unauthorized
access to systems using credential guessing techniques.

---

## Initial Triage (Tier 1 Analysis)

### 1. Validate Alert
- Confirm alert source is Wazuh
- Review rule ID and severity
- Confirm multiple failed logon events (Event ID 4625)

### 2. Identify Affected Assets
- Hostname
- Target user account
- Time range of failed logins

---

## Investigation Steps

### 1. Analyze Login Failures
- Count number of failed attempts
- Identify logon type (Interactive / Network / RDP)
- Determine time interval between attempts

### 2. Check Source IP
- Internal IP:
  - Possible user error
  - Password change issue
- External IP:
  - High risk
  - Possible brute force attack

### 3. Look for Successful Login
- Check for Event ID 4624
- Verify if successful login followed failures
- Identify if privileges were assigned

### 4. User Context Analysis
- Is the user a privileged account?
- Is the login attempt during working hours?
- Is the behavior consistent with normal activity?

---

## Evidence Collected
- Windows Event ID: 4625 (Failed Logon)
- Rule ID: 60122
- Host: DESKTOP-JT7B9UV
- Source IP: Internal

![Brute Force Alert Evidence](../screenshots/brute-force-alert.png)

---

## Assessment
- Severity: Medium
- Confidence: Medium
- Classification:
  - False Positive (internal user mistake)
  - OR Suspicious Activity (external IP / high volume attempts)

---

## Response Actions

### If False Positive
- Close alert
- Document user login behavior
- Recommend password verification

### If Confirmed Brute Force
- Block source IP
- Force password reset
- Monitor for lateral movement
- Escalate to Tier 2 SOC

---

## Escalation Criteria
Escalate if:
- External IP detected
- Admin or service account targeted
- Successful login after multiple failures
- High frequency attempts in short period

---

## Recommendations
- Enforce account lockout policy
- Enable MFA where possible
- Monitor authentication logs continuously

---

## Status
- Alert Status: Closed / Escalated
- Analyst: SOC Tier 1
- Date: 2026-02-06
