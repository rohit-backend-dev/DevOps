## 📂 Changing Directories with `cd` and `..`

* `..` → refers to the **parent directory** (one level up).
* `../..` → refers to the **grandparent directory** (two levels up).
* `cd ../../folder` → go two levels up, then into `folder`.

### Examples

1. **Move up one level**

```bash
pwd
# /home/user/projects/myapp
cd ..
pwd
# /home/user/projects
```

2. **Move up two levels**

```bash
cd ../..
pwd
# /home/user
```

3. **Move up two levels and enter a folder**

```bash
cd ../../downloads
pwd
# /home/user/downloads
```

---

### ✅ Tips

* Use `cd -` to go **back to the previous directory**.
* Use `cd ~` or just `cd` to go **directly to your home directory**.
* Tab-completion (`Tab` key) helps avoid typos in folder names.

---

## 🗂️ **1. File & Directory Management**

### 1️⃣ `ls`

* **Purpose:** List directory contents
* **Common flags:**

  * `-l` → long listing
  * `-a` → include hidden files
  * `-t` → sort by modification time
  * `-r` → reverse order
* **Example:**

  ```bash
  ls -ltrh
  ```

  * Lists all files, including hidden, detailed info, oldest → newest, human-readable sizes.
* **Tips / Mistakes:**

  * Forgetting `-a` → hidden files won’t show
  * `-h` only works with `-l`

---

### 2️⃣ `cd`

* **Purpose:** Change directory
* **Example:**

  ```bash
  cd /home/user/Documents
  cd ..        # go up one directory
  cd ../..     # go up two directories
  cd ~         # go to home
  ```
* **Tips / Mistakes:**

  * `cd` without a path → goes to home
  * Using relative vs absolute paths incorrectly

---

### 3️⃣ `pwd`

* **Purpose:** Print current working directory
* **Example:**

  ```bash
  pwd
  ```
* **Tips / Mistakes:**

  * Only prints **absolute path**, not relative

---

### 4️⃣ `mkdir`

* **Purpose:** Create a new directory
* **Example:**

  ```bash
  mkdir new_folder
  mkdir -p /tmp/a/b/c   # create nested dirs
  ```
* **Tips / Mistakes:**

  * Forget `-p` → fails if parent doesn’t exist
  * Permissions may restrict creation in some directories

---

### 5️⃣ `rmdir`

* **Purpose:** Remove **empty** directory
* **Example:**

  ```bash
  rmdir old_folder
  ```
* **Tips / Mistakes:**

  * Fails if directory is not empty → use `rm -rf` instead

---

### 6️⃣ `rm`

* **Purpose:** Remove files/directories
* **Flags:**

  * `-r` → recursive (delete directories)
  * `-f` → force (ignore prompts)
* **Example:**

  ```bash
  rm file.txt
  rm -rf folder_to_delete
  ```
* **Tips / Mistakes:**

  * Dangerous! `rm -rf /` can **wipe your system**
  * Always double-check path before `-rf`

---

### 7️⃣ `cp`

* **Purpose:** Copy files/directories
* **Flags:**

  * `-r` → recursive (copy directories)
  * `-i` → interactive (ask before overwrite)
* **Example:**

  ```bash
  cp file.txt /backup/
  cp -r folder1/ folder2/
  ```
* **Tips / Mistakes:**

  * Forget `-r` → directories won’t copy
  * Overwriting without `-i` may silently lose data

---

### 8️⃣ `mv`

* **Purpose:** Move or rename files/directories
* **Example:**

  ```bash
  mv old.txt new.txt   # rename
  mv file.txt /tmp/    # move
  ```
* **Tips / Mistakes:**

  * Moving to existing file overwrites silently → use `-i`

---

### 9️⃣ `touch`

* **Purpose:** Create empty file / update timestamp
* **Example:**

  ```bash
  touch newfile.txt
  touch -c existing.txt  # only update timestamp if exists
  ```
* **Tips / Mistakes:**

  * Creates empty file if doesn’t exist
  * Use `-c` to avoid creating new file accidentally

---

### 🔟 `cat`

* **Purpose:** View file content
* **Example:**

  ```bash
  cat file.txt
  cat file1.txt file2.txt > merged.txt
  ```
* **Tips / Mistakes:**

  * Big files → `cat` scrolls too fast, use `less`
  * `>` overwrites destination

---

### 1️⃣1️⃣ `less`

* **Purpose:** View file **page by page**
* **Example:**

  ```bash
  less syslog
  ```
* **Tips / Mistakes:**

  * Navigation: `q` to quit, `space` for next page, `/` to search
  * Doesn’t edit files, only view

---

### 1️⃣2️⃣ `head` / `tail`

* **Purpose:** View first or last lines
* **Example:**

  ```bash
  head -n 10 file.txt
  tail -f /var/log/syslog   # live updates
  ```
* **Tips / Mistakes:**

  * `-f` keeps file open for real-time logging
  * `tail` and `head` default to 10 lines

---

### 1️⃣3️⃣ `tree`

* **Purpose:** Display directory tree
* **Example:**

  ```bash
  tree /home/user
  tree -L 2  # depth 2
  ```
* **Tips / Mistakes:**

  * Install via `sudo apt install tree` if missing
  * Large directories → long output

---

### 1️⃣4️⃣ `ln`

* **Purpose:** Create links
* **Flags:**

  * `-s` → symbolic link
* **Example:**

  ```bash
  ln file.txt file_link    # hard link
  ln -s /path/file shortcut  # symlink
  ```
* **Tips / Mistakes:**

  * Hard links cannot span filesystems
  * Symbolic links break if target deleted

---

### 1️⃣5️⃣ `du`

* **Purpose:** Show directory/file size
* **Flags:**

  * `-h` → human-readable
  * `-s` → summary
* **Example:**

  ```bash
  du -sh /var/log
  ```
* **Tips / Mistakes:**

  * Without `-h`, sizes are in bytes
  * Recursive by default → huge output

---

### 1️⃣6️⃣ `df`

* **Purpose:** Disk space usage
* **Flags:**

  * `-h` → human-readable
* **Example:**

  ```bash
  df -h
  df -Th   # show filesystem types
  ```
* **Tips / Mistakes:**

  * Shows **mounted filesystems**, not all disks

---

### 1️⃣7️⃣ `find`

* **Purpose:** Search files/directories
* **Example:**

  ```bash
  find / -name "*.conf"
  find ~/ -type f -size +1M
  ```
* **Tips / Mistakes:**

  * Starts from specified path → `/` for whole system
  * Can be **slow**, use `locate` for faster searches

---

### 1️⃣8️⃣ `locate`

* **Purpose:** Quickly find files
* **Example:**

  ```bash
  locate passwd
  ```
* **Tips / Mistakes:**

  * Uses database → update with `sudo updatedb`
  * Might not find very new files immediately

---

## ⚙️ **2. System Information & Management**

### 1️⃣ `uname`

* **Purpose:** Display system information
* **Flags:**

  * `-a` → all info
  * `-r` → kernel release
  * `-m` → machine hardware
* **Example:**

  ```bash
  uname -a
  uname -r
  uname -m
  ```
* **Tips / Mistakes:**

  * Only shows OS/kernel info, not distribution details
  * For distro info, use `cat /etc/os-release`

---

### 2️⃣ `whoami`

* **Purpose:** Show current user
* **Example:**

  ```bash
  whoami
  ```
* **Tips / Mistakes:**

  * Equivalent to `id -un`
  * Does **not** show user privileges

---

### 3️⃣ `hostname`

* **Purpose:** Display or set system hostname
* **Example:**

  ```bash
  hostname
  hostnamectl set-hostname myserver
  hostname -I  # show IP addresses
  ```
* **Tips / Mistakes:**

  * Changing hostname may require restart for some services
  * `-I` shows all network IPs

---

### 4️⃣ `uptime`

* **Purpose:** Show system uptime & load
* **Example:**

  ```bash
  uptime
  ```
* **Tips / Mistakes:**

  * Load averages indicate CPU load over 1, 5, 15 mins
  * Misinterpreting load average → >1 per core indicates heavy load

---

### 5️⃣ `top`

* **Purpose:** Real-time process view
* **Example:**

  ```bash
  top
  ```
* **Tips / Mistakes:**

  * Press `q` to quit
  * Sort columns with `M` (memory) or `P` (CPU)
  * For better interactive view, use `htop`

---

### 6️⃣ `htop`

* **Purpose:** Interactive process viewer
* **Example:**

  ```bash
  htop
  ```
* **Tips / Mistakes:**

  * Requires installation: `sudo apt install htop`
  * Use arrows to navigate, `F9` to kill process

---

### 7️⃣ `ps`

* **Purpose:** Show running processes
* **Flags:**

  * `aux` → show all processes for all users with details
* **Example:**

  ```bash
  ps aux
  ps -ef  # alternative format
  ```
* **Tips / Mistakes:**

  * Snapshot view, not real-time (use `top` for live monitoring)
  * Can pipe with `grep` to filter specific process

---

### 8️⃣ `kill`

* **Purpose:** Terminate process by PID
* **Flags:**

  * `-9` → force kill
* **Example:**

  ```bash
  kill 1234
  kill -9 1234
  ```
* **Tips / Mistakes:**

  * `kill` without `-9` allows graceful termination
  * Must have permission to kill others’ processes

---

### 9️⃣ `killall`

* **Purpose:** Kill process by name
* **Example:**

  ```bash
  killall firefox
  killall -9 apache2
  ```
* **Tips / Mistakes:**

  * Kills all processes with that name
  * Dangerous if multiple instances running → use carefully

---

### 🔟 `free`

* **Purpose:** Show memory usage
* **Flags:**

  * `-h` → human-readable
  * `-m` → show in MB
* **Example:**

  ```bash
  free -h
  ```
* **Tips / Mistakes:**

  * Pay attention to `available` vs `used` memory
  * Cached memory is reusable

---

### 1️⃣1️⃣ `vmstat`

* **Purpose:** Virtual memory statistics
* **Example:**

  ```bash
  vmstat 2 5
  ```

  * Shows CPU, memory, I/O every 2 seconds for 5 iterations.
* **Tips / Mistakes:**

  * Useful for performance monitoring
  * Misreading swap vs free memory can lead to wrong conclusions

---

### 1️⃣2️⃣ `lscpu`

* **Purpose:** Show CPU architecture info
* **Example:**

  ```bash
  lscpu
  ```
* **Tips / Mistakes:**

  * Shows cores, threads, architecture
  * Doesn’t show real-time CPU usage

---

### 1️⃣3️⃣ `lsblk`

* **Purpose:** List block devices
* **Example:**

  ```bash
  lsblk
  lsblk -f   # show filesystem info
  ```
* **Tips / Mistakes:**

  * Doesn’t show mounted filesystems’ usage (use `df -h`)
  * Use with `sudo` for complete info

---

### 1️⃣4️⃣ `lspci`

* **Purpose:** Show PCI devices
* **Example:**

  ```bash
  lspci
  lspci -v   # verbose
  ```
* **Tips / Mistakes:**

  * Useful for hardware troubleshooting
  * Requires root for full info

---

### 1️⃣5️⃣ `lsusb`

* **Purpose:** Show USB devices
* **Example:**

  ```bash
  lsusb
  ```
* **Tips / Mistakes:**

  * Helps detect connected USB peripherals
  * Verbose: `lsusb -v`

---

### 1️⃣6️⃣ `dmesg`

* **Purpose:** View kernel/system messages
* **Example:**

  ```bash
  dmesg | less
  dmesg | grep usb
  ```
* **Tips / Mistakes:**

  * Logs boot and hardware messages
  * Use `sudo` to see all messages

---

### 1️⃣7️⃣ `systemctl`

* **Purpose:** Manage systemd services
* **Examples:**

  ```bash
  systemctl status ssh
  systemctl start nginx
  systemctl enable nginx
  systemctl stop nginx
  ```
* **Tips / Mistakes:**

  * Use `enable` for autostart on boot
  * Some older distros use `service` instead

---

### 1️⃣8️⃣ `journalctl`

* **Purpose:** View system logs
* **Examples:**

  ```bash
  journalctl -xe
  journalctl -u nginx
  journalctl --since "1 hour ago"
  ```
* **Tips / Mistakes:**

  * `-u` filters by service
  * Can produce huge output → use `less`

---

### 1️⃣9️⃣ `date`

* **Purpose:** Show or set system date/time
* **Examples:**

  ```bash
  date
  date "+%Y-%m-%d %H:%M:%S"
  sudo date -s "2025-10-12 15:30:00"
  ```
* **Tips / Mistakes:**

  * Changing date requires `sudo`
  * Use `timedatectl` for persistent changes

---

### 2️⃣0️⃣ `cal`

* **Purpose:** Show calendar
* **Examples:**

  ```bash
  cal
  cal 2025
  cal 10 2025   # October 2025
  ```
* **Tips / Mistakes:**

  * Only shows **visual calendar**, cannot schedule events
  * Use `ncal` for alternative layout

---

## 🌐 **3. Networking Commands**

### 1️⃣ `ping`

* **Purpose:** Test network connectivity to a host
* **Flags:**

  * `-c <count>` → number of packets
  * `-i <interval>` → interval between packets
* **Example:**

  ```bash
  ping -c 4 google.com
  ping -i 2 8.8.8.8
  ```
* **Tips / Mistakes:**

  * Use `Ctrl+C` to stop continuous ping
  * Failure may indicate DNS or firewall issues, not always host down

---

### 2️⃣ `ip`

* **Purpose:** Manage network interfaces and routes
* **Flags:**

  * `addr show` → show IPs
  * `link show` → show interfaces
  * `route` → show routing table
* **Example:**

  ```bash
  ip addr show
  ip link show
  ip route
  ```
* **Tips / Mistakes:**

  * Modern replacement for `ifconfig`
  * Use `sudo ip addr add <IP>/<mask> dev <interface>` to add IP

---

### 3️⃣ `ifconfig`

* **Purpose:** Show or configure network interfaces (legacy)
* **Example:**

  ```bash
  ifconfig
  ifconfig eth0 192.168.1.10 netmask 255.255.255.0 up
  ```
* **Tips / Mistakes:**

  * Deprecated on many modern Linux distros
  * Prefer `ip` command for scripts and automation

---

### 4️⃣ `netstat`

* **Purpose:** Show network connections, routing, and stats
* **Flags:**

  * `-tuln` → TCP/UDP listening ports without resolving names
  * `-p` → show PID of process
* **Example:**

  ```bash
  netstat -tuln
  netstat -tulpn
  ```
* **Tips / Mistakes:**

  * Can be replaced by `ss` for faster results
  * Must use `sudo` for full info

---

### 5️⃣ `ss`

* **Purpose:** Show socket statistics (faster than `netstat`)
* **Flags:**

  * `-t` → TCP
  * `-u` → UDP
  * `-l` → listening
  * `-p` → show process info
* **Example:**

  ```bash
  ss -tulpn
  ss -s  # summary
  ```
* **Tips / Mistakes:**

  * Preferred modern command for connection inspection
  * Output can be verbose → pipe with `grep`

---

### 6️⃣ `traceroute`

* **Purpose:** Trace route packets take to a host
* **Example:**

  ```bash
  traceroute google.com
  traceroute -m 10 github.com  # max 10 hops
  ```
* **Tips / Mistakes:**

  * May require `sudo` on some distros
  * Firewalls may block ICMP → incomplete paths

---

### 7️⃣ `nslookup`

* **Purpose:** Query DNS records of a domain
* **Example:**

  ```bash
  nslookup openai.com
  nslookup -type=MX gmail.com
  ```
* **Tips / Mistakes:**

  * Shows which DNS server was used
  * Use `dig` for more advanced queries

---

### 8️⃣ `dig`

* **Purpose:** DNS lookup and troubleshooting
* **Example:**

  ```bash
  dig github.com
  dig github.com A
  dig github.com MX +short
  ```
* **Tips / Mistakes:**

  * Very versatile for DNS analysis
  * `+short` simplifies output

---

### 9️⃣ `curl`

* **Purpose:** Transfer data from/to a URL
* **Flags:**

  * `-O` → save file with original name
  * `-I` → fetch headers only
  * `-L` → follow redirects
* **Example:**

  ```bash
  curl -O https://example.com/file.zip
  curl -I https://example.com
  curl -L https://tinyurl.com/example
  ```
* **Tips / Mistakes:**

  * Use for testing APIs, not just downloads
  * Avoid using `sudo` unnecessarily

---

### 🔟 `wget`

* **Purpose:** Download files from the web
* **Flags:**

  * `-c` → resume download
  * `-r` → recursive download
  * `-P <dir>` → download to directory
* **Example:**

  ```bash
  wget https://example.com/file.zip
  wget -c https://example.com/largefile.iso
  wget -r -np -k https://example.com
  ```
* **Tips / Mistakes:**

  * Useful for offline site mirroring
  * Be careful with recursive downloads → may fetch unwanted files

---

### 1️⃣1️⃣ `scp`

* **Purpose:** Secure copy over SSH
* **Flags:**

  * `-r` → recursive (directories)
  * `-P <port>` → specify SSH port
* **Example:**

  ```bash
  scp file.txt user@remote:/path/
  scp -r mydir user@host:/backup/
  scp -P 2222 file.txt user@host:/path/
  ```
* **Tips / Mistakes:**

  * Requires SSH access
  * Use `rsync` for better efficiency on large directories

---

### 1️⃣2️⃣ `rsync`

* **Purpose:** Sync files/directories efficiently
* **Flags:**

  * `-a` → archive mode
  * `-v` → verbose
  * `-z` → compress
* **Example:**

  ```bash
  rsync -avz /src/ user@host:/dest/
  rsync -av --delete /src/ /backup/
  ```
* **Tips / Mistakes:**

  * Preserves permissions, symbolic links, timestamps
  * Missing trailing slash changes behavior (`/src/` vs `/src`)

---

### 1️⃣3️⃣ `ssh`

* **Purpose:** Secure shell login to remote system
* **Flags:**

  * `-p <port>` → specify port
  * `-i <key>` → identity file (private key)
* **Example:**

  ```bash
  ssh user@host
  ssh -p 2222 user@host
  ssh -i ~/.ssh/id_rsa user@host
  ```
* **Tips / Mistakes:**

  * Passwordless login via SSH key is best practice
  * Avoid root login directly for security

---

### 1️⃣4️⃣ `telnet`

* **Purpose:** Connect to remote host via TCP
* **Example:**

  ```bash
  telnet smtp.gmail.com 25
  telnet 192.168.1.10 22
  ```
* **Tips / Mistakes:**

  * Not encrypted → use only for testing
  * Useful to check open ports

---

### 1️⃣5️⃣ `nmcli`

* **Purpose:** Manage NetworkManager connections
* **Example:**

  ```bash
  nmcli device status
  nmcli con show
  nmcli con up id "WiFiNetwork"
  ```
* **Tips / Mistakes:**

  * CLI replacement for GUI network tools
  * Ensure NetworkManager service is running

---

### 1️⃣6️⃣ `ufw`

* **Purpose:** Simple firewall configuration
* **Flags:**

  * `enable`, `disable`, `status`, `allow`, `deny`
* **Example:**

  ```bash
  sudo ufw enable
  sudo ufw allow 22/tcp
  sudo ufw status
  ```
* **Tips / Mistakes:**

  * UFW must be enabled for rules to apply
  * Avoid locking yourself out → allow SSH first

---

### 1️⃣7️⃣ `iptables`

* **Purpose:** Advanced firewall rules
* **Flags:**

  * `-L` → list rules
  * `-A` → append rule
  * `-D` → delete rule
* **Example:**

  ```bash
  sudo iptables -L
  sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
  sudo iptables -D INPUT -p tcp --dport 22 -j ACCEPT
  ```
* **Tips / Mistakes:**

  * Very powerful but dangerous → can lock out network
  * Backup rules: `sudo iptables-save > rules.backup`

---

## 🔒 **4. User & Permission Management**

### 1️⃣ `who`

* **Purpose:** Show logged-in users on the system
* **Flags:**

  * `-H` → add header
  * `-u` → show idle time
* **Example:**

  ```bash
  who
  who -H
  who -u
  ```
* **Tips / Mistakes:**

  * Useful to see multiple sessions for a user
  * Mistake: confusing with `w`, which shows more info including processes

---

### 2️⃣ `id`

* **Purpose:** Show user ID, group ID, and groups
* **Example:**

  ```bash
  id
  id rohit
  ```
* **Tips / Mistakes:**

  * Shows numeric UID/GID by default
  * Use `id -n` for names instead of numbers

---

### 3️⃣ `useradd`

* **Purpose:** Create a new user account
* **Flags:**

  * `-m` → create home directory
  * `-s` → specify shell
  * `-G` → add to supplementary groups
* **Example:**

  ```bash
  sudo useradd -m -s /bin/bash john
  sudo useradd -m -G sudo developers jane
  ```
* **Tips / Mistakes:**

  * After `useradd`, always set password using `passwd`
  * Common mistake: forgetting `-m` → no home directory created

---

### 4️⃣ `passwd`

* **Purpose:** Change password for a user
* **Flags:**

  * `-l` → lock account
  * `-u` → unlock account
* **Example:**

  ```bash
  passwd john
  sudo passwd -l john
  sudo passwd -u john
  ```
* **Tips / Mistakes:**

  * Strong passwords prevent brute force attacks
  * Mistake: `passwd` without sudo cannot change another user's password

---

### 5️⃣ `usermod`

* **Purpose:** Modify user properties
* **Flags:**

  * `-aG` → add to groups
  * `-d` → change home directory
  * `-s` → change shell
* **Example:**

  ```bash
  sudo usermod -aG sudo john
  sudo usermod -s /bin/zsh jane
  sudo usermod -d /home/newhome john
  ```
* **Tips / Mistakes:**

  * Always use `-a` with `-G` to avoid removing existing groups
  * Mistake: forgetting `sudo` → permission denied

---

### 6️⃣ `userdel`

* **Purpose:** Delete a user account
* **Flags:**

  * `-r` → remove home directory and files
* **Example:**

  ```bash
  sudo userdel john
  sudo userdel -r john
  ```
* **Tips / Mistakes:**

  * `-r` is critical to clean up files
  * Mistake: deleting active user without logging out may cause issues

---

### 7️⃣ `groupadd`

* **Purpose:** Create a new group
* **Flags:**

  * `-g <GID>` → specify group ID
* **Example:**

  ```bash
  sudo groupadd developers
  sudo groupadd -g 1500 designers
  ```
* **Tips / Mistakes:**

  * Check `/etc/group` to confirm creation
  * Mistake: duplicate GID → will fail

---

### 8️⃣ `groups`

* **Purpose:** Show groups a user belongs to
* **Example:**

  ```bash
  groups
  groups john
  ```
* **Tips / Mistakes:**

  * Useful to verify `usermod -aG` changes
  * Mistake: using `groups` after login, not showing new groups until re-login

---

### 9️⃣ `chown`

* **Purpose:** Change file ownership
* **Flags:**

  * `-R` → recursive
* **Example:**

  ```bash
  sudo chown john file.txt
  sudo chown john:developers /var/www/html -R
  ```
* **Tips / Mistakes:**

  * Critical for web server permissions
  * Mistake: using `-R` carelessly → can break system ownership

---

### 🔟 `chmod`

* **Purpose:** Change file or directory permissions
* **Modes:**

  * Numeric: `755` → owner=rwx, group=rx, others=rx
  * Symbolic: `u+x`, `g-w`
* **Example:**

  ```bash
  chmod 644 file.txt
  chmod u+x script.sh
  chmod -R 755 /var/www/html
  ```
* **Tips / Mistakes:**

  * `chmod 777` is insecure → avoid on production
  * Use `-R` carefully to avoid changing unintended files

---

### 1️⃣1️⃣ `sudo`

* **Purpose:** Run command with superuser privileges
* **Example:**

  ```bash
  sudo apt update
  sudo systemctl restart nginx
  ```
* **Tips / Mistakes:**

  * Avoid logging in as root → use `sudo`
  * Mistake: forgetting to configure user in `sudoers`

---

### 1️⃣2️⃣ `su`

* **Purpose:** Switch user or become root
* **Flags:**

  * `-` → start login shell
* **Example:**

  ```bash
  su -
  su john
  ```
* **Tips / Mistakes:**

  * `su -` is safer → loads root environment
  * Mistake: switching to root without `-` → may have wrong PATH

---

### 1️⃣3️⃣ `visudo`

* **Purpose:** Safely edit the sudoers file
* **Example:**

  ```bash
  sudo visudo
  ```
* **Tips / Mistakes:**

  * Always use `visudo` to avoid syntax errors
  * Mistake: editing `/etc/sudoers` directly → can lock out sudo access

---

## 📦 **5. Package Management**

### 1️⃣ `apt update`

* **Purpose:** Refresh package index on Debian/Ubuntu systems
* **Example:**

  ```bash
  sudo apt update
  ```
* **Tips / Mistakes:**

  * Always run before installing packages
  * Mistake: skipping update → may install outdated software

---

### 2️⃣ `apt upgrade`

* **Purpose:** Upgrade installed packages to latest versions
* **Example:**

  ```bash
  sudo apt upgrade
  sudo apt upgrade -y
  ```
* **Tips / Mistakes:**

  * Use `-y` to auto-confirm prompts
  * Mistake: skipping upgrade → may miss security patches

---

### 3️⃣ `apt install`

* **Purpose:** Install packages
* **Flags:**

  * `-y` → auto-confirm
* **Example:**

  ```bash
  sudo apt install vim
  sudo apt install git -y
  ```
* **Tips / Mistakes:**

  * Can install multiple packages at once: `apt install pkg1 pkg2`
  * Mistake: typo in package name → “Unable to locate package”

---

### 4️⃣ `apt remove`

* **Purpose:** Remove installed packages
* **Example:**

  ```bash
  sudo apt remove nginx
  sudo apt remove nginx -y
  ```
* **Tips / Mistakes:**

  * Removes package but keeps config files
  * Use `purge` if you want config files removed: `sudo apt purge nginx`

---

### 5️⃣ `apt autoremove`

* **Purpose:** Remove unused dependencies
* **Example:**

  ```bash
  sudo apt autoremove
  ```
* **Tips / Mistakes:**

  * Clean system automatically after removing packages
  * Mistake: not checking → may remove packages you actually need

---

### 6️⃣ `dpkg`

* **Purpose:** Manage .deb packages directly
* **Flags:**

  * `-i` → install package
  * `-r` → remove package
* **Example:**

  ```bash
  sudo dpkg -i package.deb
  sudo dpkg -r package_name
  ```
* **Tips / Mistakes:**

  * Useful for offline installs
  * Mistake: dependency issues → resolve with `sudo apt -f install`

---

### 7️⃣ `snap`

* **Purpose:** Install and manage Snap packages
* **Example:**

  ```bash
  snap install code --classic
  snap list
  snap remove code
  ```
* **Tips / Mistakes:**

  * `--classic` required for dev tools
  * Mistake: using Snap for apps that require old libraries → may break

---

### 8️⃣ `yum` (RedHat/CentOS)

* **Purpose:** Manage RPM packages
* **Example:**

  ```bash
  sudo yum install git
  sudo yum update
  sudo yum remove nano
  ```
* **Tips / Mistakes:**

  * For CentOS/RedHat, similar to `apt`
  * Mistake: running `yum install` without sudo → permission denied

---

### 9️⃣ `dnf` (Fedora)

* **Purpose:** Modern package manager for Fedora/RHEL
* **Example:**

  ```bash
  sudo dnf install git
  sudo dnf update
  sudo dnf remove nano
  ```
* **Tips / Mistakes:**

  * Replacement for `yum` in newer Fedora
  * Mistake: forgetting `sudo` → fails

---

### 🔟 `rpm`

* **Purpose:** Directly manage RPM packages
* **Flags:**

  * `-i` → install
  * `-U` → upgrade
  * `-e` → erase/remove
* **Example:**

  ```bash
  sudo rpm -i package.rpm
  sudo rpm -U package.rpm
  sudo rpm -e package_name
  ```
* **Tips / Mistakes:**

  * Use for offline installs
  * Mistake: dependency issues → resolve manually or use `dnf`

