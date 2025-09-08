# 🎯 Task

The Nautilus app in Stratos DC cannot connect to the database.

Root cause: MariaDB service is down on the database server.

Fix: Start (and enable) the MariaDB service.

---

## ✅ Step-by-Step Solution

### 1. SSH into the database server

If you’re on the jump host, first connect to the DB server.
Example:

```bash
ssh peter@stdb01   # replace with the actual DB server and user
```

### 2. Check MariaDB service status

```bash
sudo systemctl status mariadb
```

If it shows inactive/dead/failed, we need to start it.


### ✅ Fix: Recreate and Initialize the Data Directory

Run these commands step by step:

1. Create the MySQL data directory
```bash
sudo mkdir -p /var/lib/mysql
```

2. Set ownership to mysql user
```bash
sudo chown -R mysql:mysql /var/lib/mysql
sudo chmod -R 755 /var/lib/mysql
```

3. Initialize the MariaDB system database
```bash
sudo mariadb-install-db --user=mysql --basedir=/usr --datadir=/var/lib/mysql
# (if "mariadb-install-db" is not found, try "mysql_install_db" instead)
```

### 4. Start MariaDB
```bash
sudo systemctl start mariadb
sudo systemctl enable mariadb
```

### 5. Check status
```bash
systemctl status mariadb
```

## OUTPUT IMAGES:
<img width="1708" height="787" alt="Screenshot 2025-09-08 124046" src="https://github.com/user-attachments/assets/32b74f7a-e36b-4332-b843-dd416b7d269a" />

<img width="1713" height="826" alt="Screenshot 2025-09-08 124418" src="https://github.com/user-attachments/assets/aabc176c-31b7-4696-b67f-fab939740905" />

<img width="1715" height="838" alt="Screenshot 2025-09-08 124424" src="https://github.com/user-attachments/assets/0e1195e5-6194-436b-b58f-1ae4dda2e4f3" />
