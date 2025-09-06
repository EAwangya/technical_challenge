## Infrastructure as a Service (IaaS) 

IaaS provides on-demand, over-the-internet, basic computing infrastructure (such as storage and compute) on a pay-as-you-go basis. Instead of purchasing and maintaining physical servers and data centers, an organization can “rent” virtualized computing resources from a cloud provider.

### Security Implications 

The shared responsibility model is the key security implication of IaaS. The shared responsibility model defines who is responsible for what security controls and tasks between the cloud provider and the customer. The security of the cloud is the cloud provider’s (AWS, Azure, etc.) responsibility. This includes all the physical infrastructure, hardware, data centers, and the virtualization layer (hypervisor). On the other hand, the security in the cloud is the customer’s responsibility. This includes everything the customer runs or deploys on top of the infrastructure. In an IaaS environment, this typically means: 

* **Operating Systems (OS):** Customers are responsible for patching and configuring the OS that runs on their virtual machines.
* **Applications and Data:** Customers must secure and encrypt their own applications and data.
* **Identity and Access Management (IAM):** Customers must manage user accounts and permissions and implement multi-factor authentication (MFA) for accessing the cloud environment.
* **Network Security:** Customers are responsible for configuring firewalls, network access controls, and virtual private clouds (VPCs) to secure their workloads.
* **Monitoring and Logging:** Customers should implement monitoring to detect and respond to security threats.

The mistake is often cloud customers assume the cloud provider is responsible for everything in terms of security. This leads to IaaS customers misconfiguring their environments, which leads to vulnerabilities that can easily be exploited by attackers.


____________________

# ☁️ Infrastructure as a Service (IaaS) Security

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
