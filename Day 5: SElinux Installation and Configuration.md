# **Task: Install and Temporarily Disable SELinux on App Server 3**

## **Purpose**
Following a security audit, the **xFusionCorp Industries** security team decided to enhance server security by implementing **SELinux**. For now, the requirement is to **install SELinux packages** but keep it **disabled** until necessary configurations are completed. After the next reboot, SELinux should still be disabled.

---

## **What is SELinux?**
**Security-Enhanced Linux (SELinux)** is a Linux kernel security module that enforces **Mandatory Access Control (MAC)**.  
- Developed by the **NSA** and open-source community.  
- Adds a fine-grained security layer beyond traditional Linux permissions.  
- Restricts applications, processes, and users to a predefined set of rules.  
- Protects the system even if an application is compromised.

**Modes of SELinux:**
1. **Enforcing** – Policies are enforced; violations are blocked and logged.  
2. **Permissive** – Violations are only logged; no blocking.  
3. **Disabled** – SELinux is turned off.  

For this task, the required mode is **Disabled**.

---

## **Step-by-Step Instructions**

Steps
### 1. SSH into App Server 3 :

```bash
ssh banner@stapp03
```

### 2. Switch to root user (if required):

```bash
sudo -i
```

### 3. Install SELinux packages

```bash
yum install -y selinux-policy selinux-policy-targeted policycoreutils
```

### 4.Edit the SELinux configuration file to disable SELinux permanently

```bash
vi /etc/selinux/config
```
Change:

```bash
SELINUX=enforcing
```

To:
```bash
SELINUX=disabled
```
Save and exit (:wq in vi).

### 5. Verify configuration change

```bash
grep SELINUX= /etc/selinux/config
```

### 6. Exit from the server

```bash
exit
```

---

## **Why Install but Disable?**
- **Audit compliance:** Ensures SELinux is present on the system.  
- **Operational safety:** Disabling avoids breaking apps that aren’t configured for SELinux yet.  
- **Future readiness:** Teams can enable SELinux later when all policies are tested and ready.  

---

## **End Goal**
After the **next reboot**, `sestatus` should return:
```lua
SELinux status:                 disabled
```

### Task Images:

<img width="1743" height="859" alt="Screenshot 2025-08-11 200700" src="https://github.com/user-attachments/assets/beefc603-5ebc-4bf7-af6e-b17788a28878" />

<img width="1803" height="849" alt="Screenshot 2025-08-11 200715" src="https://github.com/user-attachments/assets/f9276b57-332c-44fc-844a-c5556d84386a" />

---

| Command | Purpose |
|---------|---------|
| `sudo yum install -y selinux-policy selinux-policy-targeted policycoreutils` | Install the required SELinux packages. |
| `sudo vi /etc/selinux/config` | Open the SELinux configuration file for editing. |
| *(Inside the file)* Change `SELINUX=enforcing` or `SELINUX=permissive` to `SELINUX=disabled` | Permanently disable SELinux so it remains off after reboot. |
| `:wq` | Save changes and exit the editor. |
| `sestatus` | Check the current status of SELinux. |

