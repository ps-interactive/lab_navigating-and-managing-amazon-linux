Library
/
solutions-reviewed.md


# Solutions

## Configure SSH password and key-based access

### Step 1 — Connect to the EC2 instance using the generated password

```bash
ssh ec2-user@<public-IP>
```

Replace `<public-IP>` with the public IP address shown in the Lab Credentials panel.

### Step 2 — Confirm the host key

When prompted, type:

```text
yes
```

### Step 3 — Authenticate with the generated password

Paste the instance password from the Lab Credentials panel and press `Enter`.

### Step 4 — Generate an Ed25519 SSH key pair on the EC2 instance

```bash
ssh-keygen -t ed25519 -C "lab-key"
```

### Step 5 — Accept the key-generation prompts

Press `Enter` to accept the default path:

```text
/home/ec2-user/.ssh/id_ed25519
```

Press `Enter` twice to leave the passphrase empty.

### Step 6 — Add the generated public key to `authorized_keys`

```bash
cat ~/.ssh/id_ed25519.pub >> ~/.ssh/authorized_keys
```

### Step 7 — Set the required SSH directory and file permissions

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

### Step 8 — Display and copy the private key

```bash
cat ~/.ssh/id_ed25519
```

Copy the entire block, including both header and footer:

```text
-----BEGIN OPENSSH PRIVATE KEY-----
...
-----END OPENSSH PRIVATE KEY-----
```

### Step 9 — Disconnect from the EC2 instance

```bash
exit
```

### Step 10 — Create the SSH directory in the learner terminal

```bash
mkdir -p ~/.ssh
```

### Step 11 — Open the lab key editor

```bash
add_key
```

The lab utility writes the key to:

```text
/home/cloud_user/.ssh/id_dropbear
```

### Step 12 — Paste and save the private key

In the editor:

1. Press `i`.
2. Paste the entire private-key block.
3. Press `Esc`.
4. Type `:wq`.
5. Press `Enter`.

### Step 13 — Set restrictive permissions on the private key

```bash
chmod 600 /home/cloud_user/.ssh/id_dropbear
```

### Step 14 — Connect to EC2 using the private key

```bash
ssh -i /home/cloud_user/.ssh/id_dropbear ec2-user@<public-IP>
```

Replace `<public-IP>` with the public IP address from the Lab Credentials panel.

### Step 15 — Confirm the host key if prompted

```text
yes
```

### Step 16 — Update installed packages

```bash
sudo dnf update -y
```

### Step 17 — Install Git

```bash
sudo dnf install git -y
```

---

# Perform filesystem navigation and file management tasks

### Step 1 — Change to `/srv`

```bash
cd /srv
```

### Step 2 — Clone the sample application repository

```bash
sudo git clone https://github.com/ps-interactive/lab_navigating-and-managing-amazon-linux.git
```

### Step 3 — Display the current working directory

```bash
pwd
```

Expected location:

```text
/srv
```

### Step 4 — List the directory contents

```bash
ls
```

Verify that this directory appears:

```text
lab_navigating-and-managing-amazon-linux
```

### Step 5 — Change to the project directory

```bash
cd /srv/lab_navigating-and-managing-amazon-linux
```

### Step 6 — Change to the `Frontend` directory using a relative path

```bash
cd Frontend
```

### Step 7 — List the current directory

```bash
ls
```

Confirm that `health.html` is not in the current directory.

### Step 8 — Locate `health.html`

```bash
find . -name "health.html"
```

Expected result:

```text
./public/health.html
```

### Step 9 — Change to the `public` directory

```bash
cd public
```

### Step 10 — Verify that `health.html` is present

```bash
ls
```

### Step 11 — Return to the `Frontend` directory

```bash
cd ..
```

### Step 12 — Display the current working directory

```bash
pwd
```

Expected path:

```text
/srv/lab_navigating-and-managing-amazon-linux/Frontend
```

### Step 13 — Search recursively for `DB_NAME`

```bash
grep -R "DB_NAME" .
```

The expected matching file is:

```text
config/database.conf
```

### Step 14 — Change to the `config` directory

```bash
cd config
```

### Step 15 — Display the database configuration

```bash
cat database.conf
```

### Step 16 — Return to the `ec2-user` home directory using an absolute path

```bash
cd /home/ec2-user
```

### Step 17 — Verify the current working directory

```bash
pwd
```

Expected path:

```text
/home/ec2-user
```

### Step 18 — Return to the project directory

```bash
cd /srv/lab_navigating-and-managing-amazon-linux
```

### Step 19 — Create the `Backend` directory

```bash
sudo mkdir Backend
```

### Step 20 — Change to the new directory

```bash
cd Backend
```

### Step 21 — Create `server.js`

```bash
sudo touch server.js
```

### Step 22 — Verify that `server.js` exists

```bash
ls
```

---

# Create and configure users, groups, and sudo access for a multi-team application environment

### Step 1 — Create the frontend group

```bash
sudo groupadd frontend_group
```

### Step 2 — Create the backend group

```bash
sudo groupadd backend_group
```

### Step 3 — Create the administrator group

```bash
sudo groupadd admin_group
```

Optional verification:

```bash
getent group frontend_group
getent group backend_group
getent group admin_group
```

### Step 4 — Create `frontend1`

```bash
sudo useradd -m frontend1
```

### Step 5 — Create the remaining users

```bash
sudo useradd -m frontend2
sudo useradd -m backend1
sudo useradd -m backend2
sudo useradd -m admin1
```

### Step 6 — Add `frontend1` to `frontend_group`

```bash
sudo usermod -aG frontend_group frontend1
```

### Step 7 — Add every remaining user to the appropriate group

```bash
sudo usermod -aG frontend_group frontend2
sudo usermod -aG backend_group backend1
sudo usermod -aG backend_group backend2
sudo usermod -aG admin_group admin1
```

Verify the memberships:

```bash
groups frontend1
groups frontend2
groups backend1
groups backend2
groups admin1
```

### Step 8 — Return to the project directory

```bash
cd /srv/lab_navigating-and-managing-amazon-linux
```

### Step 9 — Assign `frontend_group` ownership to `Frontend`

```bash
sudo chown -R root:frontend_group Frontend
```

### Step 10 — Assign `backend_group` ownership to `Backend`

```bash
sudo chown -R root:backend_group Backend
```

Verify ownership:

```bash
ls -ld Frontend Backend
```

### Step 11 — Give the owner and group full access to `Frontend`

```bash
sudo chmod -R 770 Frontend
```

### Step 12 — Temporarily make `Backend` world-writable for the later audit exercise

```bash
sudo chmod -R 777 Backend
```

This setting is intentionally insecure and will be corrected later.

### Step 13 — Add `admin1` to both development groups

```bash
sudo usermod -aG frontend_group admin1
```

```bash
sudo usermod -aG backend_group admin1
```

Verify all of `admin1`'s groups:

```bash
groups admin1
```

Expected memberships include:

```text
admin_group frontend_group backend_group
```

### Step 14 — Grant sudo access to `admin_group`

Use a validated sudoers drop-in rather than editing the main sudoers file directly:

```bash
echo '%admin_group ALL=(ALL) ALL' | sudo tee /etc/sudoers.d/admin_group
sudo chmod 440 /etc/sudoers.d/admin_group
sudo visudo -cf /etc/sudoers.d/admin_group
```

The validation command should report that the file parsed successfully.

### Step 15 — Set each learner account password to `Learner123`

Run each command and enter `Learner123` twice when prompted:

```bash
sudo passwd frontend1
sudo passwd frontend2
sudo passwd backend1
sudo passwd backend2
sudo passwd admin1
```

### Step 16 — Switch to `frontend1`

```bash
su - frontend1
```

Enter:

```text
Learner123
```

### Step 17 — Create a file in the frontend directory as `frontend1`

```bash
touch /srv/lab_navigating-and-managing-amazon-linux/Frontend/test.txt
```

### Step 18 — Return to `ec2-user`

```bash
exit
```

### Step 19 — Switch to `backend1`

```bash
su - backend1
```

Enter:

```text
Learner123
```

### Step 20 — Attempt to create a file in `Frontend` as `backend1`

Use a different filename so the result is not affected by the existing `test.txt` file:

```bash
touch /srv/lab_navigating-and-managing-amazon-linux/Frontend/permission_test.txt
```

Expected result:

```text
Permission denied
```

### Step 21 — Return to `ec2-user`

```bash
exit
```

### Step 22 — Switch to `admin1`

```bash
su - admin1
```

Enter:

```text
Learner123
```

### Step 23 — Verify sudo access

```bash
sudo whoami
```

Enter `Learner123` when prompted.

Expected output:

```text
root
```

### Step 24 — Create a file in `Frontend` as `admin1`

```bash
touch /srv/lab_navigating-and-managing-amazon-linux/Frontend/admin.txt
```

### Step 25 — Return to `ec2-user`

```bash
exit
```

---

# Implement and audit file permissions using special permission bits

Begin from the project directory:

```bash
cd /srv/lab_navigating-and-managing-amazon-linux
```

### Step 1 — Enable setgid on `Frontend`

```bash
sudo chmod g+s Frontend
```

New files and subdirectories created inside `Frontend` will inherit `frontend_group`.

### Step 2 — Enable the sticky bit on `Frontend`

```bash
sudo chmod +t Frontend
```

### Step 3 — Verify the special permission bits

```bash
ls -ld Frontend
```

The group execute position should contain `s`. The final execute position should contain `T` because others do not have execute permission under mode `770`.

### Step 4 — Switch to `frontend1`

```bash
su - frontend1
```

Enter:

```text
Learner123
```

### Step 5 — Create `app.js` in the correct `Frontend` directory

```bash
touch /srv/lab_navigating-and-managing-amazon-linux/Frontend/app.js
```

### Step 6 — Verify inherited group ownership

```bash
ls -l /srv/lab_navigating-and-managing-amazon-linux/Frontend/app.js
```

The group owner should be:

```text
frontend_group
```

### Step 7 — Create `style.css`

```bash
touch /srv/lab_navigating-and-managing-amazon-linux/Frontend/style.css
```

### Step 8 — Return to `ec2-user`

```bash
exit
```

### Step 9 — Switch to `frontend2`

```bash
su - frontend2
```

Enter:

```text
Learner123
```

### Step 10 — Attempt to remove `frontend1`'s file

```bash
rm /srv/lab_navigating-and-managing-amazon-linux/Frontend/style.css
```

If prompted, type:

```text
yes
```

Expected result:

```text
Operation not permitted
```

The sticky bit prevents `frontend2` from deleting a file owned by `frontend1`.

### Step 11 — Return to `ec2-user`

```bash
exit
```

### Step 12 — Return to the project directory

```bash
cd /srv/lab_navigating-and-managing-amazon-linux
```

### Step 13 — Find world-writable directories

```bash
find . -type d -perm -002
```

Expected result includes:

```text
./Backend
```

Permission-denied messages are not expected when running this command from the project directory as `ec2-user`.

### Step 14 — Inspect `Backend` permissions

```bash
ls -ld Backend
```

The permissions should show that everyone currently has write access.

### Step 15 — Remove world access from `Backend`

```bash
sudo chmod -R 770 Backend
```

### Step 16 — Verify the corrected permissions

```bash
ls -ld Backend
```

Only the owner and group should have read, write, and execute permissions.

### Step 17 — Repeat the world-writable directory audit

```bash
find . -type d -perm -002
```

The command should produce no output for `Frontend` or `Backend`.
