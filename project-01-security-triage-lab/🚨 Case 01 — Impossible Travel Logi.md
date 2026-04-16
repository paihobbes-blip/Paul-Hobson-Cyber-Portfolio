# 🚨 Case 01 — Impossible Travel Login

## 🧾 Alert Summary

**Alert Type:** Impossible Travel Login  
**User:** j.smith@company.com  
**Timeframe:**  
- Login 1: 10:02 AM — Sydney, Australia  
- Login 2: 10:07 AM — Moscow, Russia  

**Trigger:** Authentication system flagged logins from geographically distant locations within an unrealistic timeframe.

---

## 🔍 Initial Assessment

This alert is **highly suspicious**.

Travel between Australia and Russia within 5 minutes is physically impossible, indicating one of the following:
- Account compromise  
- Use of VPN or proxy  
- Logging anomaly  

---

## 📊 Evidence Review

### Relevant Authentication Events

| Event Time (UTC)       | Event Name     | User    | Source IP      | Region         | MFA Used | User Agent Summary |
|------------------------|----------------|---------|----------------|----------------|----------|--------------------|
| 2026-04-15T00:02:14Z   | ConsoleLogin   | j.smith | 203.0.113.45   | ap-southeast-2 | Yes      | Windows / Chrome   |
| 2026-04-15T00:07:39Z   | ConsoleLogin   | j.smith | 185.220.101.2  | eu-central-1   | No       | Linux / Chrome     |

### Observations

- Two successful AWS console login events were recorded for the same user within approximately five minutes.
- The source IP addresses were associated with different geographic regions.
- The first login used MFA, while the second did not.
- User agent patterns differed between the two events, suggesting different host profiles or access paths.
- The second IP was consistent with anonymised or privacy-focused infrastructure.

---

## 🧠 Hypotheses

### 1. Account Compromise (Most Likely)
Credentials may have been stolen and used by an attacker in a different region.

### 2. VPN Usage
User may be using a VPN that routes traffic through Russia.

### 3. Logging Error
System may have incorrectly recorded geolocation data.

### 4. Shared Credentials
Credentials may be used by another individual in a different location.

---

## ⚖️ Risk Assessment

**Likelihood:** High  
**Impact:** High  

If compromised, attacker may:
- Access sensitive systems  
- Exfiltrate data  
- Move laterally within the environment  

---

## 🚨 Recommended Actions

### Immediate Actions
- Force password reset  
- Invalidate active sessions  
- Trigger MFA re-authentication  

### Investigation Actions
- Review recent login history  
- Check for unusual activity (file access, email rules, etc.)  
- Confirm user’s location and VPN usage  

### Escalation
- Escalate to Security Operations / Incident Response team  
- Monitor account for further suspicious behaviour  

---

## 📝 Conclusion

This alert likely represents a **potential account compromise**, based on:

- Impossible travel pattern  
- Unusual IP origin  
- Device inconsistency  

Immediate containment and further investigation are required.

---

## 🤖 AI Usage & Validation

AI was used to assist with:
- Structuring investigation flow  
- Summarising observations  

Validation steps included:
- Cross-checking all conclusions against known attack patterns  
- Ensuring no assumptions were made without supporting evidence  

> Final decisions were made based on **human judgement and security reasoning**.