# Burp Suite Cheat Sheet

> Suriya already has proficiency here from 50+ PortSwigger labs.

## Core Modules

| Module | Purpose |
|--------|---------|
| **Proxy** | Intercept and modify HTTP/S requests |
| **Repeater** | Manually send and modify requests |
| **Intruder** | Automated payload injection (brute force, fuzzing) |
| **Scanner** | Automated vulnerability scanning (Pro only) |
| **Decoder** | Encode/decode URL, Base64, HTML, etc. |
| **Comparer** | Diff two requests or responses |
| **Logger** | Full request/response history |

## SOC Use Cases (Defender Perspective)

```
Understanding attack payloads seen in web logs:
- Reproduce the request to understand what the attacker was doing
- Identify the vulnerability class
- Determine if the attack was successful (response analysis)

IOC extraction:
- Identify exact payloads for SIEM rule tuning
- Extract attacker's IP, user agent, request patterns
```

## Common Burp Filters for SOC Analysis

```
In Proxy → HTTP History:
Filter by: Status code = 500 (possible successful injection)
Filter by: Response size (large responses may indicate data leakage)
Filter by: Request method = POST (form submissions)

Useful search in HTTP history:
Search: "error in your SQL syntax" → confirmed SQLi
Search: "root:" → possible /etc/passwd disclosure
Search: "exception" → application error (recon info)
```

## Attack Signatures (Payloads Seen in SOC Logs)

```sql
-- SQL Injection payloads to recognize:
' OR '1'='1
1; DROP TABLE users--
1 UNION SELECT null,null,null--
1' AND SLEEP(5)--
%27%20OR%201%3D1--

-- XSS payloads:
<script>alert(document.cookie)</script>
"><img src=x onerror=alert(1)>
javascript:alert(1)

-- Path Traversal:
../../../etc/passwd
..%2F..%2F..%2Fetc%2Fshadow
```
