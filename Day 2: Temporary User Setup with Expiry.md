# 🔧 Task

Creating a user named kirsty with an account expiration date and password policies.

---

## ✅ Steps
### 1. SSH into App Server 3:

```bash
ssh banner@stapp03
```
You're connecting to App Server 3 as user banner from the jump host.

### 2. Create the User with Account Expiry:

```bash
sudo useradd -e 2024-04-15 kirsty
```
🔍 Explanation:

useradd: command to add a new user.

`-e` stands for `--expirydate`

`-e 2024-04-15`: sets the account expiration date for the user kirsty. After this date, the account will be disabled (not deleted).

#### 📌 Syntax:
```bash
useradd -e YYYY-MM-DD <username>
```

kirsty: the username being created.

### 3. Set Password for the User:
```bash
sudo passwd kirsty
```
Prompts you to set a password for kirsty.

### 4. Check Password Expiration and Account Info:
```bash
sudo chage -l kirsty
```
`chage` stands for "change age".
`-l` stands for "list".

🔍 chage -l shows password aging info:
Output:

```
Last password change                                    : Aug 06, 2025  
Password expires                                        : never  
Password inactive                                       : never  
Account expires                                         : Apr 15, 2024  
Minimum number of days between password change          : 0  
Maximum number of days between password change          : 99999  
Number of days of warning before password expires       : 7
```

### 📝 Explanation of Each Field

| Field                            | Meaning                                                                 |
|----------------------------------|-------------------------------------------------------------------------|
| Last password change             | Date the password was last set or updated                               |
| Password expires                 | When the password will expire (forces user to change)                   |
| Password inactive                | Days after password expiration before the account is disabled           |
| Account expires                  | The date when the account itself will be disabled (not just the password) |
| Min days between password change | How soon the user can change the password again                         |
| Max days between password change | How long the user can keep the same password                            |
| Warning days                     | How many days before expiration the user will be warned to change the password |


<img width="838" height="677" alt="Screenshot 2025-08-07 181712" src="https://github.com/user-attachments/assets/6dcd8e40-b8c0-4d8f-998b-1df0e9ac488c" />


#### Some Usecases:

### 🔁 How to remove the expiry date later?
```bash
sudo usermod -e "" john
```
This removes the expiration, making the account permanent.

