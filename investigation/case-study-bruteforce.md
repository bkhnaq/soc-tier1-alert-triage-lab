### **Scenario Details**
* **External Source:** Attack originated from an external IP `185.156.x.x` (Geographic location: Unknown/Suspect).
* **Attack Sequence:** 15 failed login attempts (Event ID 4625) followed by a **Successful Login** (Event ID 4624).
* **Context:** Incident occurred at 02:30 AM (Outside business hours), which is anomalous for the targeted user.

### **Final Decision**
**Status:** <span style="color:red">**Escalated to Tier 2 (Incident Lead)**</span>

### **Reason for Escalation**
1. **High Risk of Credential Compromise:** The successful login following a brute force chain indicates a high probability of an account takeover.
2. **External Threat Actor:** The source IP has no legitimate business association with the company.
3. **Potential Lateral Movement:** Immediate expert intervention is required to perform an audit of the attacker's activity post-login.

---
**Incident Closed by Tier 1:** No.  
**Action:** Host isolated; credentials disabled; escalated for deep forensics.
