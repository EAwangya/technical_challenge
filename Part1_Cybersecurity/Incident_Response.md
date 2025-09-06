# Incident Response Plan

## Objective
To effectively contain, eradicate, and recover from the security breach while minimizing business impact.

---

## 1. Containment
- **Isolate affected systems** from the network to prevent further spread.  
- **Disable compromised user accounts** and revoke suspicious access tokens.  
- **Redirect traffic** through Web Application Firewall (WAF) for inspection.  

---

## 2. Eradication
- **Identify root cause** by analyzing logs and forensic evidence.  
- **Remove malware, backdoors, and unauthorized accounts** from compromised systems.  
- **Apply patches** to the vulnerable web application.  
- **Harden configurations** to prevent re-exploitation.  

---

## 3. Recovery
- **Restore services** from clean backups.  
- **Monitor systems** for unusual activity using SIEM tools.  
- **Validate integrity** of applications before reconnecting to production.  
- **Gradual reintegration** of systems into the production environment.  

---

## 4. Post-Incident Activities
- Conduct a **lessons learned review** with all stakeholders.  
- Update **incident response playbooks** with findings.  
- Implement **continuous monitoring** and recurring penetration tests.  
