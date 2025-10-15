
# 🎓 Linux Mastery Learning Guide 

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

## 🗂️ 1. File & Directory Management

| Command    | 🧠 Concept                                                                   | 💡 Example                    | ⚠️ Common Mistake                                   |
| ---------- | ---------------------------------------------------------------------------- | ----------------------------- | --------------------------------------------------- |
| **ls**     | Lists directory contents. `-l` gives detailed info, `-a` shows hidden files. | `ls -la`                      | Forgetting `-a` hides dotfiles like `.gitignore`.   |
| **pwd**    | Prints the full path of your current directory.                              | `pwd`                         | Works only for your shell session; not permanent.   |
| **cd**     | Changes working directory. Use `cd ..` to go up one level.                   | `cd /var/log`                 | Using `cd` alone jumps to home dir; not an error.   |
| **mkdir**  | Creates new directories. Add `-p` for nested folders.                        | `mkdir -p /tmp/test/app`      | Fails without `-p` if parent folders missing.       |
| **rmdir**  | Deletes *empty* directories.                                                 | `rmdir old_dir`               | Fails if directory isn’t empty — use `rm -r`.       |
| **rm**     | Deletes files or directories. Add `-r` for recursive delete.                 | `rm -rf build/`               | ⚠️ Be careful — no undo! Never `rm -rf /`.          |
| **cp**     | Copies files/folders. Add `-r` for recursive copy.                           | `cp -r src/ backup/`          | Forgetting `-r` gives “omitting directory” error.   |
| **mv**     | Moves or renames files/directories.                                          | `mv old.txt new.txt`          | Can overwrite files silently — use `-i` to confirm. |
| **touch**  | Creates an empty file or updates its timestamp.                              | `touch app.log`               | Doesn’t open or edit the file.                      |
| **cat**    | Displays file content or concatenates files.                                 | `cat notes.txt`               | Avoid on large files — use `less` instead.          |
| **less**   | Views file contents page by page.                                            | `less /var/log/syslog`        | Use `q` to quit; don’t try to edit here.            |
| **head**   | Shows first lines of a file (`-n` sets count).                               | `head -n 20 data.txt`         | Default is 10 lines.                                |
| **tail**   | Shows last lines; `-f` follows live logs.                                    | `tail -f app.log`             | Forgetting `-f` won’t auto-refresh.                 |
| **find**   | Searches files by name, type, size, etc.                                     | `find /home -name "*.sh"`     | Forgetting quotes causes shell expansion issues.    |
| **locate** | Finds files via index (faster than `find`).                                  | `locate passwd`               | Must run `updatedb` first for latest results.       |
| **tree**   | Displays directory hierarchy graphically.                                    | `tree /etc`                   | May not be pre-installed.                           |
| **du**     | Shows directory size (`-h` = human-readable).                                | `du -sh /home`                | Without `-h`, shows bytes only.                     |
| **df**     | Displays disk space usage of file systems.                                   | `df -h`                       | Doesn’t show unmounted devices.                     |
| **ln**     | Creates links (hard/symbolic).                                               | `ln -s /etc/passwd pass_link` | Missing `-s` makes hard link instead of symlink.    |

---

## ⚙️ 2. System Information & Process Management

| Command        | 🧠 Concept                                  | 💡 Example                            | ⚠️ Common Mistake                          |                                                  |
| -------------- | ------------------------------------------- | ------------------------------------- | ------------------------------------------ | ------------------------------------------------ |
| **uname**      | Prints system and kernel info.              | `uname -a`                            | Without `-a`, shows limited info.          |                                                  |
| **hostname**   | Displays or sets the system name.           | `hostnamectl set-hostname dev-server` | Needs `sudo` for changes.                  |                                                  |
| **whoami**     | Prints the currently logged-in user.        | `whoami`                              | Doesn’t show groups.                       |                                                  |
| **uptime**     | Shows how long the system has been running. | `uptime`                              | None.                                      |                                                  |
| **top**        | Real-time view of processes, CPU & memory.  | `top`                                 | Press `q` to quit.                         |                                                  |
| **htop**       | Interactive, color version of `top`.        | `htop`                                | May need `sudo apt install htop`.          |                                                  |
| **ps**         | Lists processes (use `aux` for all).        | `ps aux                               | grep java`                                 | Without flags shows only your shell’s processes. |
| **kill**       | Terminates process by PID.                  | `kill 1234`                           | Use `kill -9` only if normal kill fails.   |                                                  |
| **killall**    | Kills all processes by name.                | `killall firefox`                     | Case-sensitive — kills all matching names. |                                                  |
| **free**       | Displays memory usage (`-h` for readable).  | `free -h`                             | Values update only at command time.        |                                                  |
| **vmstat**     | Shows CPU, memory, swap, I/O stats.         | `vmstat 2`                            | Doesn’t show process names.                |                                                  |
| **lscpu**      | Lists CPU details.                          | `lscpu`                               | Informational only.                        |                                                  |
| **lsblk**      | Lists block devices (drives/partitions).    | `lsblk`                               | Add `-f` to view file systems.             |                                                  |
| **dmesg**      | Prints kernel and hardware messages.        | `dmesg                                | less`                                      | Long output — always pipe to `less`.             |
| **systemctl**  | Controls systemd services.                  | `systemctl restart nginx`             | Requires `sudo` for most actions.          |                                                  |
| **journalctl** | Reads logs managed by systemd.              | `journalctl -u ssh -xe`               | Use filters to avoid flooding output.      |                                                  |
| **date**       | Displays or sets date/time.                 | `date "+%F %T"`                       | Changing time requires root.               |                                                  |
| **cal**        | Prints a calendar.                          | `cal 2025`                            | Handy but purely informational.            |                                                  |

---

## 🌐 3. Networking Commands

| Command        | 🧠 Concept                              | 💡 Example                 | ⚠️ Common Mistake                             |
| -------------- | --------------------------------------- | -------------------------- | --------------------------------------------- |
| **ping**       | Checks connectivity to a host.          | `ping -c 4 google.com`     | Without `-c`, it keeps running — use Ctrl +C. |
| **ip**         | Manages network interfaces & routes.    | `ip addr show`             | Replaces old `ifconfig`.                      |
| **ifconfig**   | Displays interface info (legacy).       | `ifconfig eth0`            | Not installed by default on newer systems.    |
| **ss**         | Shows active sockets/connections.       | `ss -tulpn`                | Use `sudo` to see all ports.                  |
| **netstat**    | Lists network connections (deprecated). | `netstat -tuln`            | Use `ss` instead for accuracy.                |
| **traceroute** | Shows route packets take to host.       | `traceroute github.com`    | May require installation.                     |
| **nslookup**   | Queries DNS records.                    | `nslookup openai.com`      | Gives basic info only.                        |
| **dig**        | Advanced DNS diagnostic.                | `dig example.com`          | Use `+short` for cleaner output.              |
| **curl**       | Transfers data (HTTP, FTP, etc.).       | `curl -O file.zip`         | Without `-O`, outputs binary to screen.       |
| **wget**       | Downloads files via HTTP/FTP.           | `wget https://file.zip`    | Some servers block default user agent.        |
| **scp**        | Securely copies files over SSH.         | `scp file user@host:/path` | Ensure SSH access first.                      |
| **rsync**      | Syncs files efficiently (backups).      | `rsync -avz /src /dest`    | Forgetting `/` changes behavior.              |
| **ssh**        | Connects to remote machines.            | `ssh user@192.168.1.10`    | Wrong port or key causes denial.              |
| **ufw**        | Simple firewall utility.                | `ufw allow 22`             | Enable it first with `ufw enable`.            |
| **iptables**   | Low-level firewall control.             | `iptables -L`              | Rules reset unless saved.                     |

---

## 🔒 4. User & Permission Management

| Command     | 🧠 Concept                                   | 💡 Example                  | ⚠️ Common Mistake                                       |
| ----------- | -------------------------------------------- | --------------------------- | ------------------------------------------------------- |
| **who**     | Lists logged-in users.                       | `who`                       | None.                                                   |
| **id**      | Shows user ID and groups.                    | `id rohit`                  | Case-sensitive usernames.                               |
| **useradd** | Adds new user to system.                     | `sudo useradd john`         | Doesn’t set password automatically.                     |
| **passwd**  | Sets or changes passwords.                   | `passwd john`               | Use `sudo` for other users.                             |
| **usermod** | Modifies user properties.                    | `usermod -aG sudo john`     | Missing `-a` removes existing groups!                   |
| **userdel** | Deletes a user.                              | `userdel -r john`           | `-r` removes home folder too.                           |
| **groups**  | Lists groups current user belongs to.        | `groups`                    | None.                                                   |
| **chown**   | Changes file owner/group.                    | `chown user:group file.txt` | Fails on system files without `sudo`.                   |
| **chmod**   | Changes permissions (rwx = read/write/exec). | `chmod 755 script.sh`       | Commonly misordered — use numeric or symbolic properly. |
| **sudo**    | Executes command as root.                    | `sudo apt update`           | Don’t use for unsafe scripts.                           |
| **su**      | Switches to another user.                    | `su - root`                 | Use `exit` to return.                                   |

---

## 📦 5. Package Management

*(Examples below assume Debian/Ubuntu — replace with `yum`, `dnf`, or `zypper` on other distros.)*

| Command              | 🧠 Concept                                | 💡 Example                         | ⚠️ Common Mistake                             |
| -------------------- | ----------------------------------------- | ---------------------------------- | --------------------------------------------- |
| **apt update**       | Refreshes package lists.                  | `sudo apt update`                  | Doesn’t install anything yet.                 |
| **apt upgrade**      | Installs latest versions of all packages. | `sudo apt upgrade -y`              | Combine with `update` regularly.              |
| **apt install**      | Installs a specific package.              | `sudo apt install nginx`           | Forgetting `sudo` fails silently.             |
| **apt remove**       | Uninstalls a package.                     | `sudo apt remove nginx`            | Leaves configs — use `purge` to remove fully. |
| **apt purge**        | Removes package + config files.           | `sudo apt purge nginx`             | Double-check before using.                    |
| **dpkg -i**          | Installs `.deb` manually.                 | `sudo dpkg -i package.deb`         | Dependencies not resolved automatically.      |
| **snap**             | Manages Snap packages (sandboxed).        | `sudo snap install code --classic` | Some distros lack Snap by default.            |
| **yum install**      | RHEL/CentOS package install command.      | `sudo yum install git`             | Deprecated on new versions — use `dnf`.       |
| **dnf update**       | Modern Fedora/RHEL package update.        | `sudo dnf update`                  | Equivalent to `yum update`.                   |
| **apt-cache search** | Searches package by keyword.              | `apt-cache search java`            | Not for Snap or Flatpak packages.             |

Perfect 💪 — here’s the **final and full continuation (Part 2)** of your

> 🎓 **Linux Mastery Learning Guide (with Concepts + Examples + Common Mistakes)**

This section covers everything from text processing to disk, archiving, shell utilities, and admin tools — completing your **100+ Linux command deep-learning guide**.

---

## 🧮 **6. Text Processing & File Content Manipulation**

| Command   | 🧠 Concept                                                                             | 💡 Example                        | ⚠️ Common Mistake                               |                                                  |
| --------- | -------------------------------------------------------------------------------------- | --------------------------------- | ----------------------------------------------- | ------------------------------------------------ |
| **grep**  | Searches for patterns inside files. Use `-i` for case-insensitive, `-r` for recursive. | `grep -i "error" /var/log/syslog` | Forgetting quotes breaks pattern search.        |                                                  |
| **egrep** | Extended version of grep supporting regex.                                             | `egrep "(warn                     | error)" app.log`                                | Deprecated on some systems — use `grep -E`.      |
| **fgrep** | Fixed-string grep (no regex).                                                          | `fgrep "INFO" log.txt`            | Use only for literal searches.                  |                                                  |
| **awk**   | Powerful text processor for structured data.                                           | `awk '{print $1, $3}' data.txt`   | Syntax-sensitive — spaces matter.               |                                                  |
| **sed**   | Stream editor for find/replace in text.                                                | `sed 's/foo/bar/g' file.txt`      | Forgetting `'g'` replaces only first match.     |                                                  |
| **cut**   | Cuts specific fields by delimiter.                                                     | `cut -d':' -f1 /etc/passwd`       | Wrong delimiter gives empty output.             |                                                  |
| **sort**  | Sorts lines alphabetically/numerically.                                                | `sort -n marks.txt`               | Doesn’t remove duplicates; combine with `uniq`. |                                                  |
| **uniq**  | Removes duplicate lines (adjacent only).                                               | `sort file.txt                    | uniq`                                           | Needs sorted input to work properly.             |
| **wc**    | Counts words, lines, and characters.                                                   | `wc -l notes.txt`                 | Without flag, prints all counts together.       |                                                  |
| **paste** | Merges files line by line horizontally.                                                | `paste file1 file2`               | Mismatched line counts create gaps.             |                                                  |
| **join**  | Joins lines of two sorted files on a common field.                                     | `join f1.txt f2.txt`              | Files must be sorted on join field.             |                                                  |
| **tr**    | Translates or deletes characters.                                                      | `tr a-z A-Z < file.txt`           | Doesn’t edit file — redirects required.         |                                                  |
| **diff**  | Shows line differences between files.                                                  | `diff file1 file2`                | Outputs patch-style data — not a merge.         |                                                  |
| **cmp**   | Compares files byte by byte.                                                           | `cmp file1.bin file2.bin`         | Only useful for binary or exact match.          |                                                  |
| **comm**  | Compares sorted files and shows differences.                                           | `comm f1.txt f2.txt`              | Input must be sorted.                           |                                                  |
| **tee**   | Redirects output to file *and* screen.                                                 | `ls                               | tee list.txt`                                   | Overwrites file by default — use `-a` to append. |

---

## 🧰 **7. Compression, Archiving & Backup Tools**

| Command     | 🧠 Concept                                                        | 💡 Example                           | ⚠️ Common Mistake                                    |
| ----------- | ----------------------------------------------------------------- | ------------------------------------ | ---------------------------------------------------- |
| **tar**     | Archives multiple files. Combine with gzip/bzip2 for compression. | `tar -czvf backup.tar.gz /home/user` | Missing `-f` means no output file created.           |
| **gzip**    | Compresses individual files (replaces original).                  | `gzip log.txt`                       | Original is deleted after compression.               |
| **gunzip**  | Decompresses `.gz` files.                                         | `gunzip log.txt.gz`                  | Cannot decompress `.tar.gz` directly — use tar.      |
| **zip**     | Creates `.zip` archives (cross-platform).                         | `zip -r project.zip src/`            | Forgetting `-r` skips folders.                       |
| **unzip**   | Extracts `.zip` archives.                                         | `unzip archive.zip`                  | Doesn’t overwrite unless confirmed.                  |
| **bzip2**   | High-ratio compression (better than gzip).                        | `bzip2 data.csv`                     | Slower; only compresses one file.                    |
| **bunzip2** | Decompress `.bz2` files.                                          | `bunzip2 data.csv.bz2`               | Not for `.tar.bz2` (needs `tar -xjf`).               |
| **xz**      | Extreme compression ratio.                                        | `xz file.txt`                        | CPU intensive; one file only.                        |
| **unxz**    | Decompress `.xz` archives.                                        | `unxz file.txt.xz`                   | Use `tar -xJf` for `.tar.xz`.                        |
| **rsync**   | Syncs directories for backup.                                     | `rsync -avz /data /backup`           | Trailing `/` changes behavior — `/data/` vs `/data`. |

---

## 💾 **8. Disk, Mounting & Storage Management**

| Command    | 🧠 Concept                                   | 💡 Example                      | ⚠️ Common Mistake                                 |
| ---------- | -------------------------------------------- | ------------------------------- | ------------------------------------------------- |
| **mount**  | Attaches a filesystem/device to a directory. | `mount /dev/sdb1 /mnt`          | Directory must exist beforehand.                  |
| **umount** | Unmounts a mounted device.                   | `umount /mnt`                   | Fails if files are in use — close them first.     |
| **fdisk**  | Disk partition management tool.              | `fdisk -l`                      | Use carefully — changes are permanent.            |
| **parted** | Modern alternative to fdisk for GPT disks.   | `parted /dev/sda print`         | Requires `sudo`.                                  |
| **mkfs**   | Creates new filesystem on a partition.       | `mkfs.ext4 /dev/sdb1`           | ⚠️ Erases all data on the drive!                  |
| **blkid**  | Lists device UUIDs and types.                | `blkid`                         | Read-only tool — safe to use.                     |
| **lsblk**  | Shows mounted/unmounted block devices.       | `lsblk -f`                      | Doesn’t show usage stats.                         |
| **df**     | Shows disk space usage.                      | `df -h`                         | Displays filesystem view, not folder size.        |
| **du**     | Shows directory usage.                       | `du -sh /home/user`             | Without `-h`, output is in bytes.                 |
| **dd**     | Low-level copy and imaging tool.             | `dd if=/dev/sda of=/backup.img` | ⚠️ Dangerous if `if`/`of` reversed. Double-check! |
| **fsck**   | Checks and repairs filesystem errors.        | `fsck /dev/sda1`                | Run only on unmounted volumes.                    |

---

## ⚡ **9. Shell Utilities & Shortcuts**

| Command     | 🧠 Concept                          | 💡 Example                   | ⚠️ Common Mistake                              |                                                |
| ----------- | ----------------------------------- | ---------------------------- | ---------------------------------------------- | ---------------------------------------------- |
| **alias**   | Creates shortcuts for commands.     | `alias ll='ls -la'`          | Use quotes around alias command.               |                                                |
| **unalias** | Removes alias.                      | `unalias ll`                 | Use `-a` to remove all aliases.                |                                                |
| **history** | Shows previous commands.            | `history                     | grep apt`                                      | Doesn’t include commands from closed sessions. |
| **clear**   | Clears terminal screen.             | `clear`                      | Cosmetic — doesn’t clear scrollback buffer.    |                                                |
| **echo**    | Prints text or variables.           | `echo $HOME`                 | Double quotes preserve spaces.                 |                                                |
| **sleep**   | Pauses execution for seconds.       | `sleep 5`                    | Only pauses; doesn’t schedule.                 |                                                |
| **time**    | Measures execution time.            | `time ls -l`                 | Built-in for Bash — syntax differs for others. |                                                |
| **watch**   | Repeats command periodically.       | `watch -n 2 date`            | Quits with `Ctrl+C`.                           |                                                |
| **exit**    | Closes the current shell session.   | `exit`                       | Ends SSH if inside remote session.             |                                                |
| **source**  | Executes a script in current shell. | `source ~/.bashrc`           | `./script.sh` runs in *new* shell — not same.  |                                                |
| **export**  | Sets environment variables.         | `export PATH=$PATH:/opt/bin` | Temporary — resets on reboot.                  |                                                |

---

## 🧠 **10. System Administration & Maintenance Commands**

| Command                   | 🧠 Concept                                 | 💡 Example               | ⚠️ Common Mistake                                      |                                |
| ------------------------- | ------------------------------------------ | ------------------------ | ------------------------------------------------------ | ------------------------------ |
| **reboot**                | Restarts the system immediately.           | `sudo reboot`            | Must save work first!                                  |                                |
| **shutdown**              | Powers off or reboots the system.          | `sudo shutdown -h now`   | Without time argument, defaults to 1 minute delay.     |                                |
| **service**               | Manages SysVinit services (older systems). | `service ssh restart`    | Use `systemctl` on modern distros.                     |                                |
| **systemctl**             | Manages systemd services & targets.        | `systemctl status nginx` | Needs `sudo` for most operations.                      |                                |
| **crontab**               | Schedules recurring tasks.                 | `crontab -e`             | Commands must use full paths (e.g. `/usr/bin/python`). |                                |
| **at**                    | Schedules one-time tasks.                  | `echo "ls /home"         | at now + 1 minute`                                     | `atd` service must be running. |
| **df -Th**                | Shows filesystem type with usage.          | `df -Th`                 | Doesn’t show per-folder usage.                         |                                |
| **uptime**                | Displays load average and uptime.          | `uptime`                 | Informational — not editable.                          |                                |
| **last**                  | Shows login history.                       | `last`                   | Log may rotate; older entries disappear.               |                                |
| **journalctl -xe**        | Displays recent system logs with errors.   | `sudo journalctl -xe`    | Can be long — use filters with `-u service`.           |                                |
| **alias gs='git status'** | Quick Git alias example.                   | `alias gs='git status'`  | Not permanent unless added to `.bashrc`.               |                                |

---

# 🧩 Bonus: Power Combinations

| Task                                   | Commands Used                                 |                     |         |           |
| -------------------------------------- | --------------------------------------------- | ------------------- | ------- | --------- |
| Monitor live logs for “error” keyword  | `tail -f app.log                              | grep --color error` |         |           |
| Count unique IPs from access log       | `awk '{print $1}' access.log                  | sort                | uniq -c | sort -nr` |
| Backup `/var/www` daily with timestamp | `tar -czf backup_$(date +%F).tar.gz /var/www` |                     |         |           |
| Find large files (>500MB)              | `find / -type f -size +500M`                  |                     |         |           |
| Show top 5 memory-consuming processes  | `ps aux --sort=-%mem                          | head -n 6`          |         |           |

---
