## Step 1
**Task:** Run the following command to connect to your EC2 instance.
**Command(s):**
```bash
ssh ec2-user@<public-IP>
```

## Step 2
**Task:** Type `y` and press `Enter` if prompted to confirm the authenticity of the host.

## Step 3
**Task:** Copy and paste the instance **Password** from the **Lab Credentials** panel, then press `Enter`.

## Step 4
**Task:** Run the following command to generate an SSH key pair.
**Command(s):**
```bash
ssh-keygen -t ed25519 -C "lab-key"
```

## Step 5
**Task:** Press `Enter` to accept the default file location. When prompted for a passphrase, press `Enter` to leave it empty, then press `Enter` again to confirm.

## Step 9
**Task:** Run the following command to add the public key to the list of authorized keys.
**Command(s):**
```bash
cat ~/.ssh/id_ed25519.pub >> ~/.ssh/authorized_keys
```

## Step 10
**Task:** Run the following commands to set the required permissions.
**Command(s):**
```bash
chmod 700 ~/.ssh
```
```bash
chmod 600 ~/.ssh/authorized_keys
```

## Step 11
**Task:** Run the following command to display your private key.
**Command(s):**
```bash
cat ~/.ssh/id_ed25519
```

## Step 13
**Task:** Type `exit` and press `Enter` to disconnect from the EC2 instance.

## Step 14
**Task:** Run the following command to create the `.ssh` directory if it does not already exist.
**Command(s):**
```bash
mkdir -p ~/.ssh
```

## Step 14
**Task:** From the terminal, run the command:
**Command(s):**
```bash
add_key
```

## Step 15
**Task:** Press `i` to enter insert mode.

## Step 16
**Task:** Paste in the private key you retrieve in earlier steps at the top of this editor.

## Step 17
**Task:** Press `Esc`.

## Step 18
**Task:** Use the command `:wq` and press `Enter` to save the key and exit.

## Step 19
**Task:** Run the command:
**Command(s):**
```bash
ssh -i /home/cloud_user/.ssh/id_dropbear ec2-user@<public-IP>
```

## Step 20
**Task:** Type `y` and press `Enter` if prompted to confirm the authenticity of the host.

## Step 21
**Task:** Run the following command to update the installed packages on the EC2 instance.
**Command(s):**
```bash
sudo dnf update -y
```

## Step 22
**Task:** Run the following command to install git on the system.
**Command(s):**
```bash
sudo dnf install git -y
```

## Step 23
**Task:** Run the following command to change to the `/srv` directory.
**Command(s):**
```bash
cd /srv
```

## Step 24
**Task:** Run the following command to clone the sample web application repository into the `/srv` directory.
**Command(s):**
```bash
sudo git clone https://github.com/ps-interactive/lab_navigating-and-managing-amazon-linux.git
```

## Step 25
**Task:** Run the following command to display your current working directory.
**Command(s):**
```bash
pwd
```

## Step 26
**Task:** Run the following command to list the contents of the current directory.
**Command(s):**
```bash
ls
```

## Step 27
**Task:** Run the following command to change to the cloned repository.
**Command(s):**
```bash
cd lab_navigating-and-managing-amazon-linux/
```

## Step 28
**Task:** Run the following command to change to the `Frontend` directory.
**Command(s):**
```bash
cd Frontend/
```

## Step 29
**Task:** Suppose you need to locate the application's `health.html` file but don't know which subdirectory contains it. First, run the following command to list the contents of the current directory.
**Command(s):**
```bash
ls
```

## Step 30
**Task:** To locate the file, run the following command.
**Command(s):**
```bash
find . -name "health.html"
```

## Step 31
**Task:** Change to the `public` directory.
**Command(s):**
```bash
cd public/
```

## Step 32
**Task:** Then, run the following command to list the contents of the current directory.
**Command(s):**
```bash
ls
```

## Step 33
**Task:** Move back to your previous directory by running:
**Command(s):**
```bash
cd ..
```

## Step 34
**Task:** Display your current working directory.
**Command(s):**
```bash
pwd
```

## Step 35
**Task:** Run the following command to search for the `DB_NAME` configuration setting.
**Command(s):**
```bash
grep -R "DB_NAME"
```

## Step 36
**Task:** Run the following command to change to the `config` directory.
**Command(s):**
```bash
cd config/
```

## Step 37
**Task:** Run the following command to view the contents of the configuration file.
**Command(s):**
```bash
cat database.conf
```

## Step 38
**Task:** Run the command:
**Command(s):**
```bash
cd /home/ec2-user/
```

## Step 39
**Task:** Then, check your current working directory.
**Command(s):**
```bash
pwd
```

## Step 1
**Task:** First, return to the project directory by running the following command.
**Command(s):**
```bash
cd /srv/lab_navigating-and-managing-amazon-linux/
```

## Step 41
**Task:** Run the following command to create the `Backend` directory.
**Command(s):**
```bash
sudo mkdir Backend
```

## Step 42
**Task:** Change to the new directory.
**Command(s):**
```bash
cd Backend/
```

## Step 43
**Task:** Run the following command to create a new file named `server.js`.
**Command(s):**
```bash
sudo touch server.js
```

## Step 44
**Task:** List the contents of the current directory and verify that the `server.js` file appears in the output.
**Command(s):**
```bash
ls
```


# Create and configure users, groups, and sudo access for a multi-team application environment

## Step 1
**Task:** Run the command:
**Command(s):**
```bash
sudo groupadd frontend_group
```

## Step 2
**Task:** Create a `backend_group` to manage members of the backend development team.
**Command(s):**
```bash
sudo groupadd backend_group
```

## Step 3
**Task:** Create an `admin_group` to manage administrative users.
**Command(s):**
```bash
sudo groupadd admin_group
```

## Step 4
**Task:** Run the command:
**Command(s):**
```bash
sudo useradd -m frontend1
```

## Step 5
**Task:** Create four more users:`frontend2`, `backend1`, `backend2` and `admin1`.

## Step 6
**Task:** Run the following command.
**Command(s):**
```bash
sudo usermod -aG frontend_group frontend1
```

## Step 7
**Task:** Add `frontend2`, `backend1`, `backend2` and `admin1` to their respective groups.
**Command(s):**
```bash
groups frontend1
```

## Step 8
**Task:** Run the command:
**Command(s):**
```bash
cd ..
```

## Step 9
**Task:** Run the following command.
**Command(s):**
```bash
sudo chown -R root:frontend_group Frontend
```

## Step 10
**Task:** Change the group ownership of the `Backend` directory to `backend_group`.
**Command(s):**
```bash
ls -ld Frontend Backend
```
```bash
ls -ld Frontend Backend
```

## Step 11
**Task:** Run the command:
**Command(s):**
```bash
sudo chmod -R 770 Frontend
```

## Step 12
**Task:** Run the command:
**Command(s):**
```bash
sudo chmod -R 777 Backend
```

## Step 13
**Task:** Now add your `admin1` user to both the frontend_group and backend_group. You can see what groups you’re in using `groups admin1`. Now you're going to give the admin user sudo permissions.

## Step 14
**Task:** Run the command:
**Command(s):**
```bash
sudo visudo
```

## Step 15
**Task:** Add this to the file: `%admin_group ALL=(ALL) ALL`. This makes it so everyone in the admin_group has permissions to use sudo.

## Step 16
**Task:** Save the file with `Control+X`, `SHIFT+Y` and pressing enter. Now that your users and groups have the correct permissions you're going to give each user account a password so you can login to them and test their permissions.

## Step 17
**Task:** Run the following commands and give each user a password of Learner123.
**Command(s):**
```bash
sudo passwd frontend1
    sudo passwd frontend2
    sudo passwd backend1
    sudo passwd admin1
```

## Step 18
**Task:** Run the command:
**Command(s):**
```bash
su - frontend1
```

## Step 19
**Task:** Run the command:
**Command(s):**
```bash
touch /srv/lab_navigating-and-managing-amazon-linux/Frontend/test.txt
```

## Step 20
**Task:** Now switch to the backend1 user.

## Step 21
**Task:** Run the command:
**Command(s):**
```bash
touch /srv/lab_navigating-and-managing-amazon-linux/Frontend/test.txt
```

## Step 22
**Task:** Now switch to the admin1 user.

## Step 23
**Task:** Run the command:
**Command(s):**
```bash
sudo whoami
```

## Step 24
**Task:** Run the command:
**Command(s):**
```bash
touch /srv/lab_navigating-and-managing-amazon-linux/Frontend/admin.txt
```

## Step 25
**Task:** Run the command
**Command(s):**
```bash
exit
```


# Implement and audit file permissions using special permission bits to meet security requirements

## Step 1
**Task:** Run the command:
**Command(s):**
```bash
sudo chmod g+s Frontend
```

## Step 2
**Task:** Run the command:
**Command(s):**
```bash
sudo chmod +t Frontend
```

## Step 3
**Task:** Run the command:
**Command(s):**
```bash
ls -ld Frontend
```

## Step 4
**Task:** Swtich to the frontend1 user.

## Step 5
**Task:** Run the command:
**Command(s):**
```bash
touch /srv/Frontend/app.js
```

## Step 6
**Task:** Run the command:
**Command(s):**
```bash
ls -l /srv/Frontend/app.js
```

## Step 7
**Task:** Create a file called `style.css` in the same directory you just made app.js.

## Step 8
**Task:** Run the command
**Command(s):**
```bash
exit
```

## Step 9
**Task:** Switch to the frontend2 user.

## Step 10
**Task:** Run the command:
**Command(s):**
```bash
rm /srv/Frontend/style.css
```

## Step 11
**Task:** Type `yes` and press enter. You should get an access denied error.

## Step 12
**Task:** Run the command
**Command(s):**
```bash
exit
```

## Step 13
**Task:** Run the command:
**Command(s):**
```bash
find . -type d -perm -002
```

## Step 14
**Task:** Run this command to see the exact permissions of the Backend folder:
**Command(s):**
```bash
ls -ld Backend
```

## Step 15
**Task:** Run the command:
**Command(s):**
```bash
sudo chmod 770 Backend
```

## Step 16
**Task:** Run the command:
**Command(s):**
```bash
ls -ld Backend
```

## Step 17
**Task:** Run the command:
**Command(s):**
```bash
find . -type d -perm -002
```
