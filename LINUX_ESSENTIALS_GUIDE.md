# A Comprehensive Guide to Essential Linux Commands, Filesystem Navigation, and System Diagnostics

This guide is designed for cybersecurity students and professionals to quickly learn and apply essential Linux concepts, with a focus on **command-line usage, filesystem navigation, permissions, diagnostics, and security use cases**.

---

## 1. Introduction to Linux Terminal

### Opening a Terminal in Kali Linux

**Shortcut:**
- **Linux:** `Ctrl + Alt + T`
- **Mac (SSH):** `Ctrl + Option + T`

By default, the terminal opens in the user’s home directory.

```bash
pwd   # Print working directory
Default Directory:

User home directory (e.g., /home/kali for user kali).

Verify with pwd.

2. Linux Filesystem Hierarchy Standard (FHS)
Linux follows the FHS (Filesystem Hierarchy Standard), which defines standard directory structures.

Directory	Purpose	What’s Stored Here	Analogy
/	Root directory	Top of the filesystem	Foundation of a house
/bin	User binaries	Essential commands (ls, cp)	Toolbox
/boot	Boot loader files	Boot files, kernel	Car engine
/dev	Devices	Hardware device files	Control panel
/etc	Config files	System configs, user lists	Instruction manual
/home	User home dirs	Personal files	Bedrooms
/lib	Shared libraries	Libraries for /bin & /sbin	Spare parts
/lost+found	Recovered files	Recovery after crash	Lost & found box
/media	Removable media	Auto-mounted USB/DVD	Guest parking
/mnt	Temp mount point	Manual mount	Temporary parking
/opt	Optional apps	Large 3rd party apps	Shed
/proc	Process info	Virtual system info	Live dashboard
/root	Root home	Superuser home	Admin’s office
/run	Runtime data	Temporary runtime data	Whiteboard
/sbin	System binaries	Admin commands	Maintenance tools
/srv	Service data	Server data (web, ftp)	Service desk
/sys	System files	Kernel/hardware info	Electrical panel
/tmp	Temp files	Temporary storage	Scrap bin
/usr	User apps/resources	Installed software	Library
/var	Variable data	Logs, mail, cache	Filing cabinet

3. Connecting via SSH
Steps to connect from Mac → Linux:

Start SSH service:

bash
Copy code
sudo service ssh start
Connect:

bash
Copy code
ssh username@linux_ip
# Example:
ssh kali@192.18.64.18
Verify host key → type yes.

4. Navigation & File Management
Navigation Commands
bash
Copy code
ls        # List files
ls -l     # Long list
ls -a     # Show hidden
ls -lah   # Long list + hidden + human readable

cd /      # Go to root
cd ~      # Go to home
cd ..     # Move up one directory
cd -      # Go to previous directory

pwd       # Print current directory
File Management
bash
Copy code
mkdir new_folder         # Create dir
rmdir old_dir            # Remove empty dir
rm file.txt              # Delete file
rm -rf dir/              # Force delete directory

cp file.txt backup/      # Copy file
cp -r dir/ backup/       # Copy directory

mv old.txt new.txt       # Rename
mv file.txt ~/Downloads/ # Move file

touch new_file.txt       # Create empty file
5. Search Tools
bash
Copy code
find /home -name "*.log"        # Search for log files
grep "error" /var/log/syslog    # Search text in files
locate config.ini               # Fast file search
6. System Information
bash
Copy code
df -h     # Disk space usage
du -sh ~/Downloads   # Dir size
free -h   # Memory usage
7. Process & Service Management
Processes
bash
Copy code
ps aux | grep firefox   # List processes
top                     # Live process monitor
kill -9 1234            # Kill PID 1234
Services (systemd)
bash
Copy code
sudo systemctl start nginx      # Start
sudo systemctl stop apache2     # Stop
sudo systemctl restart ssh      # Restart
systemctl status mysql          # Status
8. User & Group Management
User Commands
bash
Copy code
sudo useradd kishore        # Add user
sudo passwd kishore         # Set password
sudo userdel -r kishore     # Delete user
sudo usermod -s /bin/zsh kishore   # Change shell
Group Commands
bash
Copy code
sudo groupadd developers
sudo usermod -aG developers kishore
sudo gpasswd -d kishore developers
Account Info
bash
Copy code
id kishore
groups kishore
getent passwd kishore
9. File Permissions
Basic Permissions
Symbol	Value	Meaning
r	4	Read
w	2	Write
x	1	Execute

bash
Copy code
chmod 755 script.sh   # rwxr-xr-x
chmod 644 config.txt  # rw-r--r--
chmod 700 private/    # rwx------
Special Permissions
SetUID: chmod 4755 /usr/bin/passwd

SetGID: chmod 2755 /shared/

Sticky Bit: chmod 1777 /tmp

10. Storage & Filesystem Diagnostics
Command	Purpose	Example	Cybersecurity Use Case
df -h	Disk usage	df -h /home	Detect log poisoning filling disk
du -sh /dir	Directory size	du -sh /var/log	Spot abnormal growth
find / -type f -size +1G	Large files	find /home -size +500M	Detect exfiltration/malware
iostat -x 2	IO performance	iostat	Detect crypto-mining
lsblk -f	Block devices	lsblk	Check unauthorized devices
blkid	Show UUIDs	blkid /dev/sda1	Verify device integrity
mount / umount	Mount filesystems	mount /dev/sdb1 /mnt/test	Evidence collection
cat /proc/mdstat	RAID status	—	Check RAID tampering
lvs / vgs / pvs	LVM info	lvs --all	Audit volume groups

11. Key Notes
Flags matter:

-r recursive

-f force

-h human-readable

Admin rights: use sudo where needed.

Wildcards:

* match multiple

? match single

Shortcuts:

Ctrl+C = Kill process

Ctrl+Z = Suspend

!! = Repeat last command

📌 Cybersecurity Relevance
Filesystem & logs: Detect tampering, log wiping, or poisoning.

Permissions: Identify privilege misconfigurations.

Processes & services: Spot malware persistence.

Storage checks: Find exfiltrated data or hidden payloads.

📂 Repository Info
Author: Purna Kishore Kondapaneni

Focus: Linux Essentials for Cybersecurity
