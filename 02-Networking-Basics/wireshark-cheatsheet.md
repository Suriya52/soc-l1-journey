# Wireshark Cheat Sheet

## Essential Display Filters

```wireshark
# Filter by IP address (any direction)
ip.addr == 192.168.1.100

# Filter by source IP
ip.src == 192.168.1.100

# Filter by destination IP
ip.dst == 10.0.0.1

# Filter by subnet
ip.addr == 192.168.1.0/24

# Filter by port
tcp.port == 443
udp.port == 53

# Show only DNS
dns

# Show only HTTP
http

# Show only HTTPS
tls

# Show only ARP
arp

# TCP SYN packets only (connection attempts / port scan)
tcp.flags.syn == 1 && tcp.flags.ack == 0

# Failed TCP connections (RST)
tcp.flags.reset == 1

# Find large packets (possible exfiltration)
frame.len > 1400

# HTTP POST requests (form submissions, possible data theft)
http.request.method == "POST"

# DNS queries only (not responses)
dns.flags.response == 0

# Packets containing a string
frame contains "password"
frame contains "cmd.exe"
```

## Analysis Workflow

```
1. Statistics → Protocol Hierarchy   (see what protocols are present)
2. Statistics → Conversations        (see top talkers)
3. Statistics → IO Graph             (visualize traffic over time)
4. Follow TCP Stream                 (read full conversation)
5. Export Objects → HTTP             (extract files transferred)
```

## IOC Hunting in PCAPs

```wireshark
# Suspicious user agents
http.user_agent contains "python"
http.user_agent contains "curl"
http.user_agent contains "nmap"

# PowerShell download
http.request.uri contains ".ps1"

# Executable downloads
http.request.uri contains ".exe"
http.request.uri contains ".dll"

# Base64 in URI (possible encoded payload)
http.request.uri contains "=="

# Long DNS queries (possible tunneling)
dns.qry.name.len > 50
```
