# Web Server Log Analysis

## Apache/Nginx Log Format

```
Apache Combined Log:
IP  ident  user  [timestamp]  "method path version"  status  size  "referer"  "user-agent"

Example:
192.168.1.100 - - [15/Jan/2024:10:30:00 +0000] "GET /login.php HTTP/1.1" 200 1234 "-" "Mozilla/5.0"
45.33.32.156  - - [15/Jan/2024:10:30:01 +0000] "GET /admin.php HTTP/1.1" 403 512  "-" "sqlmap/1.7"
```

## Attack Patterns in Web Logs

### SQL Injection
```
GET /login.php?id=1' OR '1'='1 HTTP/1.1
GET /products.php?id=1 UNION SELECT 1,2,3-- HTTP/1.1
GET /search.php?q=1'; DROP TABLE users;-- HTTP/1.1

Indicators:
- Single quotes: %27 or '
- SQL keywords: UNION, SELECT, INSERT, DROP
- Comment sequences: --, #, /*
- Boolean: OR 1=1, AND 1=1
```

### XSS Attempts
```
GET /search.php?q=<script>alert(1)</script> HTTP/1.1
GET /page.php?name=<img src=x onerror=alert(1)> HTTP/1.1

Indicators: <script>, javascript:, onerror=, onload=
```

### Directory Traversal
```
GET /download.php?file=../../etc/passwd HTTP/1.1
GET /view.php?page=../../../windows/win.ini HTTP/1.1

Indicators: ../, %2e%2e%2f, %252e%252e%252f
```

### Brute Force (Web Login)
```
POST /login.php HTTP/1.1 → 200 (check for many POSTs from same IP)
POST /login.php HTTP/1.1 → 401 (many failures)
POST /login.php HTTP/1.1 → 302 (success after failures = compromise)

Detection: High POST volume to login endpoint from single IP
```

### Scanning/Enumeration
```
Many 404 errors from same IP = directory brute force
GET /wp-admin/ → 404
GET /phpmyadmin/ → 404
GET /admin/ → 403  ← found!
GET /.env → 200  ← sensitive file exposed!

Tool signatures in User-Agent:
"sqlmap" "nikto" "dirbuster" "gobuster" "nmap" "masscan"
```

## Log Analysis Commands

```bash
# Top source IPs
awk '{print $1}' access.log | sort | uniq -c | sort -rn | head 20

# Top requested URLs
awk '{print $7}' access.log | sort | uniq -c | sort -rn | head 20

# Failed requests (4xx errors)
awk '$9 ~ /^4/' access.log | awk '{print $1, $7, $9}' | head 50

# 500 errors (possible successful injection)
grep '" 500 ' access.log

# SQL injection attempts
grep -i "union\|select\|insert\|drop\|%27\|--" access.log

# Suspicious user agents
grep -iE "sqlmap|nikto|nmap|masscan|dirbuster|gobuster|burp" access.log

# Requests with shell commands (command injection)
grep -E "(%7C|%60|\||;|%3B).*(cat|wget|curl|bash|sh)" access.log
```
