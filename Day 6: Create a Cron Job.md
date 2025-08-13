# Task
Set up a cron job for the root user that runs every 5 minutes and writes the word **"hello"** into the file `/tmp/cron_text`.

---

## **Objective**
- Learn how to use **cron** to schedule tasks in Linux.
- Understand how to:
  - Install and configure the `cronie` package.
  - Start and enable the `crond` service to ensure scheduled jobs run.
  - Add a cron job for the root user.
  - Verify the cron job setup.
- Automate a simple repetitive task (writing to a file) to demonstrate cron job execution.

## STEPS

### 1. Install `cronie` package
```bash
sudo yum install -y cronie
```

### 2. Start and enable crond service
```bash
sudo systemctl start crond
sudo systemctl enable crond
```

### 3. Add the cron job for root user
Edit the root's crontab:

```bash
sudo crontab -e
```

### 4. Verify the cron job
```bash
sudo crontab -l
```

## TASK IMAGES:

<img width="1709" height="877" alt="Screenshot 2025-08-12 220955" src="https://github.com/user-attachments/assets/f6eaf5b3-1a91-4d6b-acd1-6c5cd849c9ba" />

<img width="1695" height="835" alt="Screenshot 2025-08-12 221006" src="https://github.com/user-attachments/assets/7877c7db-cf65-4840-b864-0dce8f9c2eb2" />

<img width="1040" height="843" alt="Screenshot 2025-08-12 221554" src="https://github.com/user-attachments/assets/d4e93778-60fa-498c-b22f-5c71269c3b38" />

- Reapt the same steps for all appservers to change !.

  ---

  | **Command** | **Purpose** |
|-------------|-------------|
| `sudo yum install -y cronie` | Installs the `cronie` package, which provides the cron daemon and related utilities for scheduling tasks. |
| `sudo systemctl start crond` | Starts the cron daemon (`crond`) so it can run scheduled jobs. |
| `sudo systemctl enable crond` | Ensures the cron daemon starts automatically at system boot. |
| `sudo crontab -e` | Opens the root user's crontab file for editing to add or modify scheduled jobs. |
| `*/5 * * * * echo hello > /tmp/cron_text` | Cron expression to run the command `echo hello > /tmp/cron_text` every 5 minutes. This overwrites the file `/tmp/cron_text` with the text "hello". |
| `sudo crontab -l` | Lists all cron jobs scheduled for the root user to verify they are set correctly. |

