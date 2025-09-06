## Kubernetes Security Features

**Network Policies:**     
This feature lets you define rules that control the traffic between pods and namespaces. You can specify which pods can communicate with each other and block all other traffic. This helps you isolate your workloads and prevent unauthorized access to your microservices.

**Role-Based Access Control (RBAC):**   
RBAC is a system that allows you to define roles with specific permissions and assign them to users, groups, or service accounts. For example, you can create a role that can only read pods and bind it to a user. This helps you manage who can access what resources in your Kubernetes cluster and follow the principle of least privilege.

**Pod Security Standards (PSS):**   
PSS is a set of security policies that you can enforce on pods. It has three levels: Privileged, Baseline, and Restricted. These policies ensure that your pods are not running with insecure settings, such as running as root or with elevated privileges.

**Here is a Kubernetes Pod YAML configuration that includes securityContext settings to enhance its security.** 

```
apiVersion: v1
kind: Pod
metadata:
  name: secure-pod
spec:
  securityContext:
    runAsUser: 1000
    runAsGroup: 3000
    fsGroup: 2000
  containers:
  - name: secure-container
    image: nginx
    ports:
    - containerPort: 80
    securityContext:
      allowPrivilegeEscalation: false
      readOnlyRootFilesystem: true
      runAsNonRoot: true
      capabilities:
        drop:
        - ALL
```