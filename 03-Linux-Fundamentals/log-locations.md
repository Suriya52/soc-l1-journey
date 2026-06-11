# Linux Log File Locations

## Critical Log Files for SOC

| Log File | Contains | Key Patterns to Hunt |
|----------|----------|---------------------|
| `/var/log/auth.log` | SSH, sudo, su, PAM auth | Failed password, Accepted, sudo, su |
| `/var/log/secure` | Same as auth.log (RHEL/CentOS) | Same patterns |
| `/var/log/syslog` | General system messages | Errors, service starts/stops |
| `/var/log/messages` | Same as syslog (RHEL/CentOS) | Same patterns |
| `/var/log/kern.log` | Kernel messages | Hardware issues, kernel exploits |
| `/var/log/boot.log` | Boot process | Boot failures |
| `/var/log/dmesg` | Hardware/driver messages | USB insertions, hardware changes |
| `/var/log/cron` | Cron job executions | Suspicious scheduled tasks |
| `/var/log/wtmp` | All login/logout records | Use `last` command to read |
| `/var/log/btmp` | Failed login attempts | Use `lastb` command to read |
| `/var/log/lastlog` | Last login per user | Use `lastlog` to read |
| `/var/log/faillog` | Failed login counts | Use `faillog` to read |
| `/var/log/audit/audit.log` | Linux audit daemon | System calls, file access |

## Web Server Logs

```
/var/log/apache2/access.log    # Apache — every HTTP request
/var/log/apache2/error.log     # Apache — errors
/var/log/nginx/access.log      # Nginx access
/var/log/nginx/error.log       # Nginx errors
```

## Apache/Nginx Log Format

```
Apache Combined Log Format:
192.168.1.100 - alice [15/Jan/2024:10:30:00 +0000] "GET /login.php HTTP/1.1" 200 1234 "-" "Mozilla/5.0"
│             │ │    │ │                          │  │                      │   │     │    │
IP addr       │ user │ timestamp                  │  request                status size │   user-agent
              │      │                            │                                     │
              ident  │                            method                                referer
                     │
                     auth user
```

## Auth Log Patterns

```bash
# Successful SSH login
Jan 15 10:30:00 server sshd[12345]: Accepted password for alice from 192.168.1.100 port 55123 ssh2

# Failed SSH login
Jan 15 10:30:01 server sshd[12345]: Failed password for admin from 45.33.32.156 port 45678 ssh2

# Invalid user attempt
Jan 15 10:30:02 server sshd[12345]: Invalid user tomcat from 45.33.32.156 port 45679

# Sudo usage
Jan 15 10:30:10 server sudo: alice : TTY=pts/0 ; PWD=/home/alice ; USER=root ; COMMAND=/bin/bash

# User added to sudo group
Jan 15 11:00:00 server groupadd[13000]: add 'attacker' to group 'sudo'
```

## Audit Log Analysis

```bash
# Install auditd if not present
apt install auditd

# Search audit log for specific user
ausearch -ua alice

# Search for file access
ausearch -f /etc/passwd

# Search for executed commands
ausearch -sc execve

# Generate report
aureport --summary
aureport --login --failed
```
