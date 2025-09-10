# 📌 Task Description:

The Nautilus application development team has built a Java-based web application (as a ROOT.war file).
You need to deploy this application on App Server 3 using the Tomcat application server with the following requirements:

Install Tomcat on App Server 3.

Configure Tomcat to run on port 8088.

Copy the provided ROOT.war file (available on Jump Host under /tmp) to Tomcat’s deployment directory on App Server 3.

----

## Step by Step Procedure:

### 1.Move to "/tmp":
```bash
cd /tmp
```


### 2.Check for "ROOT.war file" in /tmp:

```bash
ls -la
```

### 3.Move the ROOT.war file to the given App Server:

```bash
scp /tmp/ROOT.war banner@stapp03:/tmp
```

### 4.Now Connect to the App Server:

```bash
ssh baner@stapp02
```

### 5.Move to the /tmp file in App Server":
```bash
cd /tmp
```
And list all files to view "ROOT.war"
```bash
ls -la
```
### 6.Chech for tomcat:
```bash
sudo systemctl status tomcat
```
It shows tomcat.service not found....

### 7. Install tomcat:
```bash
sudo yum install tomcat -y
```

### 8.Again check for Tomcat Status:
```bash
sudo systemctl status tomcat
```

### 9. Locate to tomcat file check installation and change port:
```bash
cd /etc/tomcat
```

### 10. lookup for server.xml:
```bash
cat server.xml
```

Now change the port in "server.xml"
```bash
sudo vi server.xml
```
- Here change connection port that is given for you eg:8088.


### 11. Now check for the tomcat status:

Restart tomcat:
```bash
sudo systemctl restart tomcat
```

status of tomcat:
```bash
sudo systemctl status tomcat
```
-The active status: Running...

### 12. Copy the ROOT war file to user tomcat:
```bash
sudo cp/tmp/ROOT.war /usr/share/tomcat
```

### 13.Now restart and check status:
Restart tomcat:
```bash
sudo systemctl restart tomcat
```

status of tomcat:
```bash
sudo systemctl status tomcat
```

### 14. Now paste the Url:
example:
"curl http://stapp03:8088"

------

OUPTUT IMAGES:

<img width="1771" height="862" alt="Screenshot 2025-09-10 235535" src="https://github.com/user-attachments/assets/125569d6-727f-44be-b579-f656ae361df6" />

<img width="1733" height="847" alt="Screenshot 2025-09-10 235553" src="https://github.com/user-attachments/assets/5aba8832-71f3-40b5-8869-af99c4923514" />

<img width="1790" height="906" alt="Screenshot 2025-09-10 235625" src="https://github.com/user-attachments/assets/9ac398f9-abcd-4a97-bb7d-5d1715d968aa" />

<img width="1752" height="825" alt="Screenshot 2025-09-10 235733" src="https://github.com/user-attachments/assets/9c774c09-bf2c-4aec-a88c-897a577088e4" />

<img width="1783" height="866" alt="Screenshot 2025-09-10 235806" src="https://github.com/user-attachments/assets/20e003e6-d9ca-4448-bbbc-78b1254b1a5a" />

<img width="1785" height="873" alt="Screenshot 2025-09-10 235747" src="https://github.com/user-attachments/assets/a3611c2b-25fd-4df4-afee-5875c5d61616" />

<img width="1748" height="810" alt="Screenshot 2025-09-10 235902" src="https://github.com/user-attachments/assets/4ae52dd3-8379-446e-b22a-ab80e9b21730" />
