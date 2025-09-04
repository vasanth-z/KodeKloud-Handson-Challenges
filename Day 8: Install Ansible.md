# 🎯 Task

Install Ansible 4.9.0 on Jump Host using pip3 (not yum/apt).
Make sure it is available globally (i.e., all users can run ansible).

----

## ✅ Step-by-Step Solution

### 1. Make sure pip3 is installed

```bash sudo yum install -y python3-pip   # (for RHEL/CentOS)```
# or
```sudo apt-get install -y python3-pip   # (for Ubuntu/Debian)```


### 2. Install the specific version of Ansible (4.9.0) using pip3

``` sudo pip3 install ansible==4.9.0 ```


sudo → installs globally (not just for current user).

ansible==4.9.0 → forces exactly version 4.9.0.

### 3. Verify installation

```ansible --version```


Expected output (something like):

ansible [core 2.11.6] 
  config file = None
  python version = 3.x.x


Note: Ansible version numbers map to core versions. For Ansible 4.9.0, you’ll see ansible-core 2.11.6 inside. That’s correct ✅.

### 4. Make sure all users can access ansible

Since we installed via sudo pip3, the binary will be in a global path (/usr/local/bin/ansible).

Check:

```bash
which ansible
ls -l $(which ansible)
```


If it’s not in /usr/bin or /usr/local/bin, add it to the system PATH:

echo 'export PATH=$PATH:/usr/local/bin' | sudo tee /etc/profile.d/ansible.sh
source /etc/profile.d/ansible.sh

### OUTPUT

<img width="1707" height="644" alt="Screenshot 2025-09-04 212614" src="https://github.com/user-attachments/assets/d4c6846a-f4e2-4c68-960e-012a49b01d62" />

<img width="1747" height="658" alt="Screenshot 2025-09-04 212627" src="https://github.com/user-attachments/assets/1f056ba5-9651-46ee-b559-1edbce9edd5f" />

<img width="1152" height="691" alt="Screenshot 2025-09-04 212644" src="https://github.com/user-attachments/assets/86953147-288e-4f7a-a689-85978ec88b68" />

----

# 📌 Ansible Installation (Commands & Purpose)

| Command | Purpose |
|---------|---------|
| `sudo yum install -y python3-pip` | Install pip3 package manager on RHEL/CentOS |
| `sudo apt-get install -y python3-pip` | Install pip3 package manager on Ubuntu/Debian |
| `sudo pip3 install ansible==4.9.0` | Install Ansible version **4.9.0** globally using pip3 |
| `ansible --version` | Verify Ansible installation and check the installed version |
| `which ansible` | Show the location/path of the Ansible executable |
| `ls -l $(which ansible)` | List details (permissions, ownership, etc.) of the Ansible binary |
| `echo 'export PATH=$PATH:/usr/local/bin' \| sudo tee /etc/profile.d/ansible.sh` | Add Ansible’s binary path permanently to the system-wide PATH |
| `source /etc/profile.d/ansible.sh` | Reload environment variables so the new PATH takes effect immediately |

