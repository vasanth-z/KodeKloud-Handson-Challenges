## Task
Grant executable permissions to the `/tmp/xfusioncorp.sh` script on **App Server 2**.  
Additionally, ensure that **all users** have the capability to execute it.

---

## Steps

1. **SSH into App Server 2** from the jump host:
   ```bash
   ssh steve@stapp02
   ```

2. **Grant execute permissions to all users**:
   ```bash
   sudo chmod a+x /tmp/xfusioncorp.sh
   ```
   *(Alternatively, you can use `sudo chmod 755 /tmp/xfusioncorp.sh`)*

3. **Verify the permissions**:
   ```bash
   ls -l /tmp/xfusioncorp.sh
   ```
   Expected output:
   ```
   -rwxr-xr-x  1 root root  <size> <date> /tmp/xfusioncorp.sh
   ```

4. **Exit the server**:
   ```bash
   exit
   ```
   
<img width="1730" height="850" alt="Screenshot 2025-08-10 204315" src="https://github.com/user-attachments/assets/50500d89-2446-411a-8c4e-0fd9d783fbae" />

| Command | Purpose |
|---------|---------|
| `ssh steve@stapp02` | Connect to **App Server 2** as the user `steve`. |
| `sudo chmod 755 /tmp/xfusioncorp.sh` | Grant executable permissions to all users for the script. Owner gets read, write, execute; group and others get read and execute. |
| `ls -l /tmp/xfusioncorp.sh` | Verify that the permissions have been updated correctly (`-rwxr-xr-x`). |
| `exit` | Logout from **App Server 2** and return to the jump host. |
