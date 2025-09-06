# Ansible Playbook: Deploy NGINX Web Server with Custom Homepage

This Ansible playbook automates the deployment of an **NGINX web server** with a custom homepage (`index.html`).  
It ensures that NGINX is installed, running, enabled on boot, and configured to serve a custom HTML file.  

---

## Playbook Overview

### Playbook Name
**Deploy NGINX Web Server with Custom Homepage**

### Target Hosts
- `webservers`

### Privilege Escalation
- Uses `become: yes` to execute tasks with elevated privileges.

---

## Variables

- **`nginx_package`** → The package name of NGINX (`nginx`).  
- **`web_root`** → Default NGINX web root (`/usr/share/nginx/html`).  
- **`index_file`** → Path to the NGINX index file (`/usr/share/nginx/html/index.html`).  
- **`local_index_path`** → Location of your custom homepage (`files/index.html`).

---

## Tasks

1. **Install NGINX**  
   Ensures the `nginx` package is installed.

2. **Ensure NGINX is running and enabled**  
   Starts NGINX and enables it on boot.

3. **Upload custom `index.html`**  
   Copies a custom HTML file (`files/index.html`) from your local machine to the server’s web root.  
   - Destination: `/usr/share/nginx/html/index.html`  
   - Ownership: `root:root`  
   - Permissions: `0644`

4. **Open HTTP port in firewall (RedHat only)**  
   - If the target system belongs to the **RedHat family**, this task configures **firewalld** to allow HTTP traffic.

5. **Reload firewalld (RedHat only)**  
   - Reloads firewall rules to apply changes.  
   - Triggers handler to restart NGINX.

---

## Handlers

- **Restart NGINX**  
  Ensures NGINX reloads its configuration whenever notified (e.g., after firewall reload).

---

## How to Run

```bash
ansible-playbook -i inventory deploy-nginx.yml
