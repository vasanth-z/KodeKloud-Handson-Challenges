# TASK:
In Stratos Datacenter, one of the app servers (stapp01) has an issue.

The Apache service is not reachable on port 5000.

You must troubleshoot why Apache is down or unreachable and fix it so that curl http://stapp01:5000 works from the jump host.

----

## Step by Step Procedure:
### 1. Checked connectivity from the Jump Host:
```bash
telnet stapp01 5000 #replace the port given
```
* Repeat the same steps for the other app server to check whether It is connected or not.

Output:
Check that which App server doesnt have route to host...
```
telenet: connect to addreess 172.16.238.10: No route to host
```

First attempt failed (No route to host), so you tested with stapp02 and stapp03 for comparison.

* Confirmed connectivity issue specifically on stapp01.

### 2. Logged in to stapp01:
```bash
ssh tony@stapp01
```
Then get super user access for configurations:
```bash
sudo su -
```
Switched to root user to investigate Apache directly.

### 3. Checked Apache service status:
```bash
systemctl status httpd
```
" Found that httpd failed to start. "

Error logs showed:

Address already in use: AH00072: make_sock: could not bind to address 0.0.0.0:5000

👉 This means port 5000 is already being used by another process.

### 4. Identified which process is using port 5000
```bash
netstat -lnpt | grep 5000
```
Found that process 451 (sendmail) was already bound to port 5000.

### 5. Killed the conflicting process
```bash
kill 451
```
Stopped the sendmail process that was occupying port 5000.

### 6. Restarted Apache service
```
systemctl restart httpd
systemctl status httpd
```
After killing the conflicting process, Apache started successfully.

Verified Apache is now running on port 5000.

### 7. Verified connectivity again

From jump host:
```
curl http://stapp01:5000
```

This confirmed Apache was now serving content properly.

OUTPUT IMAGES:
<img width="1745" height="876" alt="Screenshot 2025-09-15 101805" src="https://github.com/user-attachments/assets/841d83b7-f31b-4bf4-94c5-f0a21bf4f2a1" />

<img width="1723" height="830" alt="Screenshot 2025-09-15 101815" src="https://github.com/user-attachments/assets/fb421b8c-f289-4024-b4d1-70331c5e4c7c" />

<img width="1728" height="826" alt="Screenshot 2025-09-15 101826" src="https://github.com/user-attachments/assets/ea04ab55-6c23-4f99-bc5a-b4459010b3cd" />

<img width="1749" height="838" alt="Screenshot 2025-09-15 101847" src="https://github.com/user-attachments/assets/59c53f76-062d-4c0e-8072-c6ee8c4999d2" />

<img width="1751" height="707" alt="Screenshot 2025-09-15 101857" src="https://github.com/user-attachments/assets/91413da5-64ba-48ce-9069-fc83e5c43b61" />

-----

## Commands Used and Their Purpose

`telnet stapp01 5000` -	Test if port 5000 on stapp01 is reachable from the jump host.

`ssh tony@stapp01`    -	Log in to stapp01 server as user tony.

`sudo su`             -	Switch to root user for admin access.

`systemctl status httpd` -	Check the status of Apache (httpd) service.

`netstat -lnpt | grep 5000` - netstat-shows the active and listening ports, grep - searches for pattern in text.

`kill 451` -	Kill process with PID 451 (sendmail) that was blocking port 5000.

`systemctl restart httpd`	- Restart the Apache service.

`systemctl status httpd` - 	Confirm Apache is active and running on port 5000.

`curl http://stapp01:5000` - 	Verify Apache is accessible on port 5000 from the jump host.
