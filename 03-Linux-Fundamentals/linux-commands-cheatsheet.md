# Linux Commands Cheat Sheet for SOC

## File & Directory Operations

```bash
ls -la                        # List all files with permissions
ls -lt                        # Sort by modification time (newest first)
pwd                           # Print current directory
cd /var/log                   # Change directory
find / -name "*.log" 2>/dev/null  # Find all .log files
find / -mtime -1 -type f      # Files modified in last 24 hours
find / -perm -4000 -type f 2>/dev/null  # SUID files (privesc check)
locate malware.exe            # Quick file search (uses database)
```

## Text Processing (Essential for Log Analysis)

```bash
cat /var/log/auth.log                    # Print file content
head -50 /var/log/syslog                 # First 50 lines
tail -100 /var/log/syslog                # Last 100 lines
tail -f /var/log/auth.log                # Follow live log updates
grep "Failed password" /var/log/auth.log # Search for pattern
grep -i "error" /var/log/syslog          # Case-insensitive search
grep -r "192.168.1.100" /var/log/        # Recursive search in dir
grep -v "^#" config.conf                 # Exclude comment lines

# AWK — column extraction
awk '{print $1, $3}' access.log          # Print columns 1 and 3
awk -F: '{print $1}' /etc/passwd         # Use : as delimiter

# SED — stream editor
sed 's/ERROR/CRITICAL/g' logfile.txt     # Replace text
sed -n '100,200p' large.log              # Print lines 100-200

# CUT — field extraction
cut -d' ' -f1 access.log                 # Get first field (IP in Apache log)
cut -d: -f1 /etc/passwd                  # Get usernames

# SORT and UNIQ — frequency analysis
sort file.txt | uniq -c | sort -rn       # Count occurrences, sort by frequency
```

## SOC Investigation Commands

```bash
# Count failed SSH logins per IP
grep "Failed password" /var/log/auth.log \
  | awk '{print $11}' \
  | sort | uniq -c | sort -rn | head -20

# Find successful logins after failures (brute force success)
grep "Accepted password" /var/log/auth.log

# Check who is logged in right now
who
w
last | head -20                           # Recent logins

# Network connections
ss -tulnp                                # All listening ports + process
netstat -an | grep ESTABLISHED           # Active connections
ss -an | grep :4444                      # Check for suspicious port

# Processes
ps aux                                   # All running processes
ps aux | grep [malicious_name]           # Find specific process
top                                      # Real-time process view
lsof -i :443                             # What's using port 443
lsof -p 1234                             # Files opened by PID 1234

# System info
uname -a                                 # Kernel version
id                                       # Current user + groups
whoami                                   # Current user
hostname                                 # System hostname
uptime                                   # System uptime and load

# File integrity
md5sum suspicious.file                   # Get MD5 hash
sha256sum suspicious.file               # Get SHA256 hash
file malware.bin                         # Identify file type
strings malware.bin | head -50           # Extract readable strings
```

## User & Account Investigation

```bash
cat /etc/passwd                          # All users
cat /etc/shadow                          # Password hashes (root only)
id username                             # User's groups
sudo -l                                  # What can current user sudo
lastlog                                  # Last login for all users
faillog -a                               # Failed login attempts
aureport --login                         # Audit report of logins
```

## Persistence Mechanism Checks

```bash
# Cron jobs (scheduled tasks)
crontab -l                               # Current user's cron
cat /etc/crontab                         # System cron
ls /etc/cron.*                           # All cron directories

# Startup scripts
ls /etc/init.d/                          # Init scripts
systemctl list-units --type=service      # All services
cat /etc/rc.local                        # Startup commands

# SSH authorized keys (backdoor check)
cat ~/.ssh/authorized_keys
cat /root/.ssh/authorized_keys

# SUID binaries (potential privesc)
find / -perm -4000 -user root -type f 2>/dev/null
```
