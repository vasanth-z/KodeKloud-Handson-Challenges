# Task: Disable Direct SSH Root Login on All App Servers

## Objective
Following security audits, the **xFusionCorp Industries** security team has restricted direct root SSH login.  
Your task is to **disable direct SSH root login** on all app servers in the **Stratos Datacenter**.

"ssh" - Secure Shell.

"sshd" - Secure Shell Daemon.

---

## Steps

### 1. SSH into the Target Server
Connect to the server as a non-root user (e.g., `tony`).
```bash
ssh tony@stapp01
```
-Replace stapp01 with the correct server hostname or IP address.

-Enter the user password when prompted.

----

### 2. Switch to Root User

Once logged in, elevate privileges to root.

```bash
sudo su -
```
`sudo` - "Superuser do"

`su` - "Switch User"

`-` - hyphen signifies "Login Shell"

- You’ll need to enter the password for the non-root user (tony in this case).

---

### 3. Edit the SSH Configuration File

Open the SSH daemon configuration file with vi editor.

```bash
vi /etc/ssh/sshd_config
```
"vi" - text editor
"etc" - contains configuration files for system and application.

"

Locate the line:
```shell
#PermitRootLogin yes
```
Change it to:
```nginx
PermitRootLogin no
```

If the line is commented (# at the start), remove the #.

Save and exit in vi:

```ruby
use "i" to insert
Esc - to backstate

:wq -where "w" to write and "q" to exit
Enter
```

----

### 4. Test the SSH Configuration
Before applying changes, ensure there are no syntax errors.

```bash
sshd -t
```
- If there’s no output, it means there are no configuration errors.

- If an error appears, fix it before restarting the service.

----

### 5. Restart the SSH Service
Apply the changes by restarting the SSH service.

```bash
systemctl restart sshd
```

To Check Status:
```
systemctl status sshd
```

### Exit the Server

After completing the task, to exit the server 

```
exit or logout
```

---

Task Images:

<img width="1919" height="930" alt="Screenshot 2025-08-09 115123" src="https://github.com/user-attachments/assets/3f44feb2-4df0-49bc-bf7b-84ee490a3e74" />

<img width="1824" height="912" alt="Screenshot 2025-08-09 115745" src="https://github.com/user-attachments/assets/db0f8d21-97eb-4209-99b6-728b406adea5" />

----
# Disable Direct SSH Root Login – Commands & Purpose

| Command | Purpose |
|---------|---------|
| `ssh tony@stapp01` | Connect to the server as the non-root user `tony`. |
| `sudo su -` | Switch to the root user with full privileges. |
| `vi /etc/ssh/sshd_config` | Open the SSH daemon configuration file for editing. |
| *(Inside vi)*<br>`#PermitRootLogin yes` → `PermitRootLogin no` | Disable direct SSH root login by changing the setting. |
| `sshd -t` | Test the SSH configuration for syntax errors before applying changes. |
| `systemctl restart sshd` | Restart the SSH service to apply the new configuration. |
| `exit` | Log out from the server session. |
