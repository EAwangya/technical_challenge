# Network Security Measures

## Objective
Enhance the organization's defense posture by strengthening network security and reducing attack vectors.

---

## Recommended Security Technologies & Practices

### 1. Intrusion Detection/Prevention Systems (IDS/IPS)
- Monitor network traffic for suspicious activity.  
- Automatically block or alert on intrusion attempts.  
- Example: Snort, Suricata, AWS GuardDuty, Azure Defender.  

---

### 2. Firewalls
- Enforce strict inbound and outbound traffic rules.  
- Apply segmentation rules between application tiers (web, app, database).  
- Use next-generation firewalls (NGFW) for deep packet inspection.  

---

### 3. Network Segmentation
- Separate critical systems into distinct security zones.  
- Limit lateral movement of attackers if one segment is breached.  
- Implement **Zero Trust Network Architecture (ZTNA)** principles.  

---

### 4. Security Monitoring & Logging
- Centralize logs using a SIEM (e.g., Splunk, ELK, Azure Sentinel).  
- Continuously monitor network events and generate alerts.  
- Enable automated responses to common attack signatures.  

---

### 5. Multi-Factor Authentication (MFA) for Remote Access
- Enforce MFA for VPNs, cloud services, and administrative access.  
- Reduces the risk of credential-based attacks.  
