# **💻 Linux Top 30 Commands – Interview Quick Sheet**

## **1️⃣ File & Directory**

| Command  | Purpose           | Example                 |
| -------- | ----------------- | ----------------------- |
| `ls -la` | List all files    | `ls -la`                |
| `cd`     | Change directory  | `cd /home/user`         |
| `pwd`    | Current directory | `pwd`                   |
| `mkdir`  | Make directory    | `mkdir new_folder`      |
| `rm -rf` | Remove file/dir   | `rm -rf folder`         |
| `cp -r`  | Copy file/dir     | `cp -r folder1 folder2` |
| `mv`     | Move/Rename       | `mv file.txt /tmp/`     |
| `touch`  | Create file       | `touch file.txt`        |
| `cat`    | View file         | `cat file.txt`          |
| `less`   | Page-wise view    | `less file.txt`         |
| `find`   | Search files      | `find / -name "*.conf"` |

---

## **2️⃣ System & Process**

| Command         | Purpose             | Example           |
| --------------- | ------------------- | ----------------- |
| `uname -a`      | System info         | `uname -a`        |
| `whoami`        | Current user        | `whoami`          |
| `uptime`        | System uptime       | `uptime`          |
| `top`           | Live process view   | `top`             |
| `htop`          | Interactive process | `htop`            |
| `ps aux`        | Running processes   | `ps aux`          |
| `kill -9 PID`   | Kill process        | `kill -9 1234`    |
| `free -h`       | Memory usage        | `free -h`         |
| `df -h`         | Disk usage          | `df -h`           |
| `du -sh folder` | Folder size         | `du -sh /var/log` |

---

## **3️⃣ Networking**

| Command                     | Purpose           | Example                        |
| --------------------------- | ----------------- | ------------------------------ |
| `ping`                      | Test connectivity | `ping -c 4 google.com`         |
| `ip addr show`              | IP info           | `ip addr show`                 |
| `netstat -tuln`             | Network stats     | `netstat -tuln`                |
| `ss -tulpn`                 | Socket info       | `ss -tulpn`                    |
| `ssh user@host`             | Remote login      | `ssh john@192.168.1.5`         |
| `scp file user@host:/path/` | Copy over SSH     | `scp file.txt john@host:/tmp/` |
| `curl -I url`               | Fetch headers     | `curl -I https://google.com`   |
| `wget url`                  | Download file     | `wget https://file.zip`        |

---

## **4️⃣ Users & Permissions**

| Command             | Purpose            | Example                      |
| ------------------- | ------------------ | ---------------------------- |
| `id`                | User info          | `id john`                    |
| `useradd -m`        | Add user           | `sudo useradd -m john`       |
| `passwd`            | Change password    | `sudo passwd john`           |
| `usermod -aG group` | Add to group       | `sudo usermod -aG sudo john` |
| `userdel -r`        | Delete user        | `sudo userdel -r john`       |
| `chown`             | Change owner       | `sudo chown john file.txt`   |
| `chmod`             | Change permissions | `chmod 755 file.txt`         |
| `sudo`              | Run as root        | `sudo apt update`            |

---

## **5️⃣ Package Management (Debian/Ubuntu)**

| Command                      | Purpose          | Example                       |
| ---------------------------- | ---------------- | ----------------------------- |
| `apt update`                 | Refresh repo     | `sudo apt update`             |
| `apt upgrade -y`             | Upgrade packages | `sudo apt upgrade -y`         |
| `apt install pkg -y`         | Install package  | `sudo apt install git -y`     |
| `apt remove pkg`             | Remove package   | `sudo apt remove nginx`       |
| `apt autoremove`             | Cleanup deps     | `sudo apt autoremove`         |
| `dpkg -i pkg.deb`            | Install .deb     | `sudo dpkg -i file.deb`       |
| `snap install pkg --classic` | Snap package     | `snap install code --classic` |

---

✅ **Tips for interviews:**

* Know `ls`, `cd`, `pwd`, `chmod`, `chown`, `top`, `ps`, `kill`, `scp`, `ssh` by heart.
* Always mention **flags** like `-r`, `-f`, `-a`, `-h` in answers.
* Be ready to explain **difference between `kill` & `killall`**, `find` & `locate`, `apt` & `dpkg`.

---
