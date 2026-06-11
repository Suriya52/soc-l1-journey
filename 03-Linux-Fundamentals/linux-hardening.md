# Linux Hardening Checklist

> For SOC analysts: understand what a hardened system looks like so you can spot deviations.

## User Management
- [ ] Disable root SSH login (`PermitRootLogin no` in sshd_config)
- [ ] Use SSH key authentication only (`PasswordAuthentication no`)
- [ ] Remove unnecessary user accounts
- [ ] Set password policy (min length, complexity, expiry)
- [ ] Restrict sudo to specific users and commands
- [ ] Lock accounts after failed attempts (fail2ban)

## File System
- [ ] Set correct permissions on sensitive files
  ```bash
  chmod 600 /etc/shadow      # Only root reads
  chmod 644 /etc/passwd      # World readable
  chmod 700 /root            # Root home dir
  ```
- [ ] Find and investigate SUID/SGID binaries
- [ ] Disable USB storage if not needed
- [ ] Enable filesystem auditing with auditd

## Network
- [ ] Firewall enabled (ufw or iptables)
- [ ] Only required ports open
- [ ] Disable IPv6 if not used
- [ ] Enable TCP SYN cookies (SYN flood protection)

## Services
- [ ] Disable Telnet, FTP, rsh (use SSH/SFTP instead)
- [ ] Remove or disable unused services
- [ ] Keep all packages updated
- [ ] Enable automatic security updates

## Logging & Monitoring
- [ ] auditd installed and configured
- [ ] Logs forwarded to central SIEM
- [ ] Log rotation configured
- [ ] Fail2ban installed for brute force protection

## SOC Relevance
When investigating a Linux system, deviations from a hardened baseline are red flags:
- SSH running with password auth → potential brute force vector
- New SUID binaries → possible privilege escalation tool
- New cron entries → possible persistence
- Unusual listening ports → possible backdoor
