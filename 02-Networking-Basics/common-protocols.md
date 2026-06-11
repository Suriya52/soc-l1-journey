# Common Protocols Reference

## Must-Know Protocols for SOC

| Protocol | Port | Transport | Purpose | Security Notes |
|----------|------|-----------|---------|----------------|
| HTTP | 80 | TCP | Web traffic | Unencrypted — never for sensitive data |
| HTTPS | 443 | TCP | Encrypted web | SSL/TLS — check cert validity |
| DNS | 53 | UDP/TCP | Name resolution | DNS tunneling, poisoning vector |
| SMTP | 25 | TCP | Email sending | Spam relay, phishing source |
| SMTPS | 465/587 | TCP | Encrypted email | Preferred for auth |
| FTP | 21 | TCP | File transfer | Cleartext credentials — flag it |
| FTPS | 990 | TCP | Encrypted FTP | Acceptable |
| SSH | 22 | TCP | Secure shell | Brute force target |
| Telnet | 23 | TCP | Unencrypted shell | NEVER use — always alert |
| RDP | 3389 | TCP | Remote desktop | Major brute force/lateral movement target |
| SMB | 445 | TCP | File sharing | EternalBlue, ransomware propagation |
| LDAP | 389 | TCP | Directory services | AD queries, credential exposure |
| LDAPS | 636 | TCP | Encrypted LDAP | Preferred |
| Kerberos | 88 | TCP/UDP | AD authentication | Pass-the-ticket, Kerberoasting |
| SNMP | 161 | UDP | Network management | Community string exposure |
| NTP | 123 | UDP | Time sync | NTP amplification DDoS |
| ICMP | — | — | Ping, traceroute | Covert C2 channel, network recon |

## DNS Deep Dive (Critical for SOC)

DNS is abused constantly. Watch for:

```
DNS Tunneling    → Unusually long DNS queries, high query volume
                   Tool: iodine, dnscat2

DNS Poisoning    → Incorrect IP returned for a domain
                   (MITM between client and DNS server)

Fast Flux DNS    → Malware C2 domains that change IPs rapidly
                   Indicator: Many A records, very low TTL

DGA Domains      → Randomly generated domains used by malware C2
                   Indicator: Nonsense domain names, NX responses
```

## HTTP Response Codes (SOC Relevant)

| Code | Meaning | SOC Relevance |
|------|---------|---------------|
| 200 | OK | Normal |
| 301/302 | Redirect | Watch for redirect chains to malicious sites |
| 400 | Bad Request | Could indicate injection attempt |
| 401 | Unauthorized | Auth failure |
| 403 | Forbidden | Access control working |
| 404 | Not Found | Directory brute force generates many 404s |
| 500 | Server Error | Could indicate successful injection |
| 503 | Service Unavailable | Could indicate DDoS |
