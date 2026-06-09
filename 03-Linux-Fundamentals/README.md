# 🐧 03 — Linux Fundamentals

> Linux runs most of the internet — and most SIEM/security tooling.

## Purpose
A SOC analyst spends significant time on Linux systems — investigating logs, running queries, and managing security tools. This section builds comfort with the CLI and security-relevant Linux knowledge.

## Topics Covered

- [ ] Linux file system hierarchy
- [ ] Essential commands (ls, grep, find, awk, sed, cut)
- [ ] File permissions and ownership
- [ ] User and group management
- [ ] Process management (ps, top, netstat, ss)
- [ ] Log files and their locations
- [ ] Systemd and service management
- [ ] Bash scripting for security tasks
- [ ] Linux hardening concepts
- [ ] Cron jobs and persistence mechanisms

## Files in This Folder

| File | Description |
|------|-------------|
| `linux-commands-cheatsheet.md` | Essential commands for SOC work |
| `log-locations.md` | Where to find critical log files |
| `bash-scripts/` | Useful security scripts |
| `linux-hardening.md` | Security hardening checklist |
| `common-ioc-hunting.md` | Finding IOCs on a Linux system |

## Critical Log Locations

```bash
/var/log/auth.log          # Authentication events (Debian/Ubuntu)
/var/log/secure            # Authentication events (RHEL/CentOS)
/var/log/syslog            # General system messages
/var/log/kern.log          # Kernel messages
/var/log/apache2/access.log  # Apache web server access
/var/log/apache2/error.log   # Apache errors
/var/log/nginx/access.log    # Nginx access log
/var/log/fail2ban.log        # Fail2ban actions
/var/log/audit/audit.log     # Linux audit daemon
```

## SOC-Useful Commands

```bash
# Find recently modified files
find / -mtime -1 -type f 2>/dev/null

# Check for SUID binaries (privilege escalation)
find / -perm -4000 -type f 2>/dev/null

# Active network connections
ss -tulnp

# Check running processes
ps aux | grep [suspicious_name]

# Search logs for failed logins
grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c | sort -rn

# Find cron jobs for all users
for user in $(cut -d: -f1 /etc/passwd); do echo "=== $user ==="; crontab -l -u $user 2>/dev/null; done
```
