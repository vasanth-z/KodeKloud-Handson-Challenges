# 🔧 Task

You are asked to:
Create a user named yousuf with a non-interactive shell (/sbin/nologin) on App Server 1.
This is a typical task in system administration where a user is added for automated tasks (like a backup agent), and you don't want them to have shell access (i.e., they can't log in to the terminal).

### 📟 Terminal Walkthrough

Connecting to App Server 1:

```bash
ssh tony@stapp01 #tony-user, stapp01-servername
```
You are connecting from a jump host (the main control server) to the App Server 1 using the ssh (Secure Shell) command.
The server IP and key fingerprint are verified and saved for the first time.

### Creating A User:

```bash
sudo useradd -s /sbin/nologin yousuf
```
This runs successfully, meaning the user is now created.

### Verifying the user:

```bash
grep yousuf /etc/passwd
```
This shows user details from the /etc/passwd file:

```ruby
yousuf:x:1002:1002::/home/yousuf:/sbin/nologin
```
Interactive, so the user can't log in via terminal.

<img width="1896" height="922" alt="Screenshot 2025-08-06 233649" src="https://github.com/user-attachments/assets/7fa92622-d714-4861-a396-de77ec0e75ae" />

## Explanation:

| Command                                 | Purpose                                              |
|-----------------------------------------|------------------------------------------------------|
| `ssh tony@stapp01`                      | Connect to App Server 1                              |
| `useradd -s /sbin/nologin yousuf`       | Add user with non-interactive shell (failed without sudo) |
| `sudo useradd -s /sbin/nologin yousuf`  | Add user with elevated permissions                   |
| `grep yousuf /etc/passwd`              | Verify user details                                  |

#### ✅ Why use `/sbin/nologin?`
- Used for service accounts or automation (e.g., backup agents).
- Ensures the user can’t access the system via shell or SSH.

#### 🔹 grep yousuf /etc/passwd
✅ Purpose:
Searches for the line in the /etc/passwd file that contains information about the yousuf user.

##### 🔍 Breakdown:
Part	Meaning:
`grep`	Command-line search tool used to look for text patterns.
`yousuf`	The search keyword — here, it's the username.
`/etc/passwd` -	A system file that contains user account information.

#### ✅ -s stands for --shell
It is used to specify the login shell for the user being created.

📌 Syntax:
```bash
useradd -s <shell_path> <username>
```
🔍 Example:
```bash
useradd -s /sbin/nologin yousuf
```
Here, the -s /sbin/nologin part tells the system:
Create the user yousuf
Set their shell to /sbin/nologin
Meaning: the user cannot log in interactively (no terminal or SSH access)

