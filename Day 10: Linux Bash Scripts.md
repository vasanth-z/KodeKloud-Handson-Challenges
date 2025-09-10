#📌 Task:
The production support team of **xFusionCorp Industries** required a bash script to automate the backup of website files on **App Server 1**.  
The script should:
1. Create a zip archive of the `/var/www/html/official` directory.
2. Save the archive inside `/backup/` on **App Server 1**.
3. Copy the archive to the **Nautilus Backup Server** at `/backup/` location.
4. Ensure no password prompt while copying (using SSH key-based authentication).
5. Avoid using `sudo` inside the script.

---

## ⚠️ Challenge Faced:
While starting, the **zip package was not installed** on the server.  
Since `zip` is essential for creating compressed archives, it had to be installed manually before proceeding.

```bash
# Install zip package
sudo yum install -y zip     # For RHEL/CentOS
# OR
sudo apt-get install -y zip # For Ubuntu/Debian
```

## 🛠️ Steps :

### 1️⃣ Connect to App Server:
```bash
ssh banner@stapp01 #replace server given to you
```

### 2️⃣ Navigate to Scripts Directory:
```bash
cd /scripts
```

### 3️⃣ Create the Backup Script:

Created a script named official_backup.sh.

```bash
vi official_backup.sh #replace the script name given for you.
```
Added the following content:

Note: "change the file names as given to you !!"
```bash
Copy code
#!/bin/bash
echo "zip archiving file.."
zip -r /backup/xfusioncorp_official.zip /var/www/html/official

echo "copying zip archive..."
scp /backup/xfusioncorp_official.zip clint@stbkp01:/backup

echo "successfully backed up"
```
Save and exit:

```ruby
:wq
```
### 4️⃣ Make Script Executable

```bash
chmod +x official_backup.sh
```

### 5️⃣ Setup SSH Key Authentication

To avoid password prompts during SCP:

```bash
ssh-keygen -t rsa
```
- Here Just press the "Enter" button for the following...

Then run:
```bash
ssh-copy-id clint@stbkp01 #replce with your backup server
```

### 6️⃣ Run the Script

```bash
./official_backup.sh

(or)

bash official_backup.sh
```

### ✅ Verification

Checked if the zip archive was created in /backup/ on Backup App Server 1:

Exit from the current server and login to Backup Server:
```bash
ssh clint@stbkp01
```

Now then run this command and that backup file that you created in App server is showing here:

```bash
ls -la /backup/
```
Verified the archive exists on Nautilus Backup Server in /backup/:

```bash
ssh clint@stbkp01 "ls -l /backup/"
```

OUTPUT IMAGES:

<img width="1775" height="850" alt="Screenshot 2025-09-10 231129" src="https://github.com/user-attachments/assets/dbdc580e-70d5-40c1-8d24-8d2082b2581f" />


<img width="285" height="209" alt="Screenshot 2025-09-10 230433" src="https://github.com/user-attachments/assets/d18b5127-1a4a-49a8-805c-c717f83750f9" />

SCRIPT:

<img width="1731" height="878" alt="Screenshot 2025-09-10 215007" src="https://github.com/user-attachments/assets/5c126be5-0ecd-4121-bbe0-a441df85c115" />

<img width="1766" height="848" alt="Screenshot 2025-09-10 231140" src="https://github.com/user-attachments/assets/1a61187f-43e1-4ddc-8e6a-72741396f278" />

<img width="1762" height="854" alt="Screenshot 2025-09-10 231156" src="https://github.com/user-attachments/assets/af8b7535-4e6e-47d9-b284-e0f5f51c0948" />

<img width="1780" height="849" alt="Screenshot 2025-09-10 231212" src="https://github.com/user-attachments/assets/ed0818c0-2a3b-43c0-9e24-7ae3c2e13fe7" />

<img width="1826" height="897" alt="Screenshot 2025-09-10 231316" src="https://github.com/user-attachments/assets/bf93df3e-7e71-43a3-922c-978e89ce2a0b" />
