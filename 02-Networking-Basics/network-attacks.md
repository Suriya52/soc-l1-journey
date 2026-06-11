# Common Network Attacks

## Reconnaissance

| Attack | Description | Detection |
|--------|-------------|-----------|
| **Port Scan** | Attacker probes ports to find open services | Many SYN packets, few ACKs, multiple ports in short window |
| **Ping Sweep** | ICMP echo to find live hosts | Many ICMP requests across subnet |
| **OS Fingerprinting** | Identify OS via packet analysis | Nmap -O scan patterns |
| **Banner Grabbing** | Connect to service to read version info | Multiple connections to different ports |

## Man-in-the-Middle (MITM)

| Attack | Description | Detection |
|--------|-------------|-----------|
| **ARP Poisoning** | Fake ARP replies redirect traffic through attacker | Duplicate IP-MAC mappings in ARP table |
| **DNS Spoofing** | Return false DNS response | DNS answers don't match trusted resolver |
| **SSL Stripping** | Downgrade HTTPS to HTTP | HTTPS redirects to HTTP |

## Denial of Service

| Attack | Description | Detection |
|--------|-------------|-----------|
| **SYN Flood** | Overwhelm server with SYN packets | Huge volume of SYN, no ACK |
| **UDP Flood** | Flood with UDP packets | Massive UDP traffic |
| **DNS Amplification** | Use DNS to amplify attack traffic | Large DNS responses to victim |
| **ICMP Flood (Ping flood)** | Overwhelm with ICMP | High ICMP volume |

## Exfiltration Techniques

| Technique | How | Detection |
|-----------|-----|-----------|
| **DNS Tunneling** | Encode data in DNS queries | Long DNS names, high DNS query volume |
| **HTTP/S C2** | C2 traffic blends with web traffic | Beaconing pattern, unusual user agents |
| **ICMP Tunneling** | Hide data in ICMP payload | Unusually large ICMP packets |
| **FTP Exfil** | Upload files to attacker FTP | Large FTP PUT to unknown server |
