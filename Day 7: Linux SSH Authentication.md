# Task
Set up password-less SSH authentication from your local machine to a remote server using the ssh-copy-id command, so you can log in without entering a password every time.

---

## Objective
- Eliminate the need to manually type your SSH password for every connection.

- Increase login speed and reduce repetitive authentication steps.

- Use a simple one-command method (ssh-copy-id) instead of manually editing remote authorized_keys files.

- Maintain secure authentication by using SSH key pairs instead of storing plain passwords.

  ----
## Steps

### 1) Check if an SSH key already exists (skip creation if it does)
```bash
ls -l ~/.ssh/id_rsa ~/.ssh/id_rsa.pub 2>/dev/null
```
If you see both files, you already have a key → jump to step 2.

If not, create one:

Create a new RSA key (no passphrase so jobs can run unattended):

```bash
ssh-keygen -t rsa -b 4096 -N "" -f ~/.ssh/id_rsa
```

This creates:

private key: ~/.ssh/id_rsa

public key: ~/.ssh/id_rsa.pub

### 2) Copy your public key to each app server
This appends your key to the server’s ~/.ssh/authorized_keys and sets permissions.

```bash
ssh-copy-id -o StrictHostKeyChecking=no tony@stapp01
ssh-copy-id -o StrictHostKeyChecking=no steve@stapp02
ssh-copy-id -o StrictHostKeyChecking=no banner@stapp03
```
You’ll be asked once for each user’s password. After that, key auth is set.

If ssh-copy-id isn’t available, use this manual method (example for stapp01):

```bash
cat ~/.ssh/id_rsa.pub | ssh tony@stapp01 \
'mkdir -p ~/.ssh && chmod 700 ~/.ssh && \
 cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys'
```

Note : Repeat for the other servers changing the user/host.

### 3) Test password-less login (should not prompt for a password)
```bash
ssh -o PasswordAuthentication=no tony@stapp01 'whoami && hostname'
ssh -o PasswordAuthentication=no steve@stapp02 'whoami && hostname'
ssh -o PasswordAuthentication=no banner@stapp03 'whoami && hostname'
```
Expected: prints the user and hostname, no password prompts.

### 4) (Optional) Fix common permission issues on the remote server
If you still get password prompts, log in once with a password and run:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

### TASK IMAGES:

<img width="1735" height="839" alt="Screenshot 2025-08-13 210048" src="https://github.com/user-attachments/assets/01904f63-8cad-4448-a491-fa7828fd6779" />

<img width="1729" height="849" alt="Screenshot 2025-08-13 210055" src="https://github.com/user-attachments/assets/7ad16c7a-30a4-41f2-a5d3-af2798a51dbe" />
