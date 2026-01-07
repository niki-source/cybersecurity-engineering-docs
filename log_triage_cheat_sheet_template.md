## Document Metadata
- **Title:** Log Triage Cheat Sheet  
- **Version:** v1.0  
- **Author:** <Your Name / Team>  
- **Last Updated:** <Date>  
- **Audience:** SOC Tier 1 / Tier 2 Analysts  
- **Purpose:** Rapid, consistent log analysis during alert investigation

---

## 1. Triage Philosophy (Read First)

**Goal of log triage:**  
Quickly determine:
- Is this **malicious**, **benign**, or **needs escalation**?
- What is the **scope**?
- What is the **next action**?

**Golden rule:**  
> Do not over-investigate before classifying severity.

---

## 2️. Core Triage Questions (Universal)

Ask these **for every alert**, regardless of log source:

| Question | Why it matters |
|--------|---------------|
| Who triggered this? | User, system, service account |
| What happened? | Action taken |
| When did it happen? | Timing & sequence |
| Where did it originate? | IP, host, country |
| How did it happen? | Tool, protocol, process |
| Is this expected behavior? | Baseline comparison |
| Has it happened before? | Repetition = risk |

---

## 3️. Log Source Quick Reference

| Log Source | What it tells you |
|----------|------------------|
| Authentication logs | Logins, failures, MFA |
| Process creation | Execution behavior |
| Network logs | Connections & traffic |
| DNS logs | Domain lookups |
| Proxy/Web logs | Web access |
| EDR logs | Endpoint activity |
| Cloud logs | API & identity actions |

---

## 4️. Authentication Log Triage

### Common Fields to Check
- Username  
- Source IP  
- Result (Success / Failure)  
- Authentication method  
- Time window  
- MFA status  

### Red Flags 
- Multiple failures → success  
- Login from new country  
- Service account interactive login  
- Disabled account activity  
- MFA bypass or MFA fatigue  

### Benign Indicators 
- Known VPN IP  
- User confirmed activity  
- Expected geolocation  

### Initial Action
- [ ] Document  
- [ ] Reset credentials  
- [ ] Escalate  
- [ ] Close as benign  

---

## 5️. Process Execution Log Triage

### Key Fields
- Image / Process Name  
- Command Line  
- Parent Process  
- User context  
- Execution time  

### Suspicious Patterns 
- LOLBins (PowerShell, certutil, mshta)  
- Encoded commands  
- Office spawning shell  
- SYSTEM account running user tools  

### Benign Patterns 
- Signed binaries  
- Known admin scripts  
- IT automation tools  

---

## 6️. Network & DNS Log Triage

### Key Fields
- Source IP  
- Destination IP / Domain  
- Port & protocol  
- Frequency  
- Direction (inbound/outbound)  

### High-Risk Indicators 
- Beaconing patterns  
- Known malicious domains  
- Unusual outbound ports  
- Internal host scanning  

### Questions to Ask
- Is the destination known?  
- Is traffic periodic?  
- Does the host normally talk externally?  

---

## 7️. IOC Enrichment Checklist

For **any IOC**, check:
- Threat intelligence reputation  
- Historical sightings  
- Associated malware/campaigns  
- Related alerts in SIEM  

> ⚠️ Do not directly interact with suspicious infrastructure unless authorized.

---

## 8️. Severity Classification Guide

| Severity | Definition |
|--------|------------|
| Low | Expected or benign |
| Medium | Suspicious but contained |
| High | Confirmed malicious |
| Critical | Active compromise |

---

## 9️. Escalation Criteria

Escalate when you observe:
- Credential compromise  
- Lateral movement  
- Command & Control  
- Privilege escalation  
- Data exfiltration  

---

## 10. Documentation Checklist (Mandatory)

Before closing or escalating:
- [ ] Alert summary  
- [ ] Logs reviewed  
- [ ] Findings  
- [ ] Decision rationale  
- [ ] Next steps taken  

---

## 11. One-Minute Triage Summary (For Tickets)

> **Summary:**  
> Alert triggered by `<event>` from `<source>`.  
> Reviewed `<log sources>`.  
> Determined activity is `<classification>` due to `<reason>`.  
> **Action taken:** `<action>`.

---

## 12. Analyst Reminders

- Speed > perfection at Tier 1  
- Patterns matter more than single events  
- If unsure → escalate early  
- Always document reasoning  

---

###  Pro Tip
This cheat sheet should be:
- Open next to your SIEM  
- Printed or pinned  
- Used every shift
