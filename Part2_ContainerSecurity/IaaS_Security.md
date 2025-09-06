# Infrastructure as a Service (IaaS) Security

## What is IaaS?
Infrastructure as a Service provides **virtualized computing resources** over the internet, such as:
- Virtual machines
- Storage
- Networking
- Load balancers

Examples: **AWS EC2, Azure Virtual Machines, Google Compute Engine**

---

## Security Implications

### 1. Shared Responsibility Model
- **Cloud Provider** secures the physical infrastructure, networking, and hypervisor.  
- **Customer** secures the OS, applications, configurations, and data.  

### 2. Common Risks
- Misconfigured storage buckets (data leaks).  
- Weak IAM policies (unauthorized access).  
- Insecure API keys or credentials.  
- Lack of patching for guest OS.  

### 3. Best Practices
- Enforce **Identity and Access Management (IAM)** with least privilege.  
- Use **encryption** at rest and in transit.  
- Enable **logging and monitoring** (e.g., AWS CloudTrail, Azure Monitor).  
- Apply **patch management** to guest VMs.  
- Implement **network segmentation** with VPCs, subnets, and firewalls.  

---

## Summary
While IaaS providers secure the underlying infrastructure, customers must secure:
- **Workloads** (VMs, containers, apps)  
- **Access** (IAM, MFA, RBAC)  
- **Data** (encryption, backups, monitoring)  

This balance ensures a strong security posture in the cloud.  
