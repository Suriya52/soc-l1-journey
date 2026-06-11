# Nmap Cheat Sheet

## Basic Scans

```bash
# Single host
nmap 192.168.1.100

# Network range
nmap 192.168.1.0/24

# Multiple targets
nmap 192.168.1.1 192.168.1.2 192.168.1.3

# From file
nmap -iL targets.txt
```

## Scan Types

```bash
nmap -sS 192.168.1.100      # SYN scan (stealth, requires root)
nmap -sT 192.168.1.100      # TCP connect scan (no root needed)
nmap -sU 192.168.1.100      # UDP scan (slow)
nmap -sn 192.168.1.0/24     # Ping sweep (host discovery only)
nmap -Pn 192.168.1.100      # Skip host discovery, scan anyway
```

## Port Specification

```bash
nmap -p 80 192.168.1.100           # Single port
nmap -p 80,443,8080 192.168.1.100  # Multiple ports
nmap -p 1-1024 192.168.1.100       # Port range
nmap -p- 192.168.1.100             # All 65535 ports
nmap --top-ports 100 192.168.1.100 # Top 100 common ports
```

## Service & OS Detection

```bash
nmap -sV 192.168.1.100      # Service version detection
nmap -O 192.168.1.100       # OS detection
nmap -A 192.168.1.100       # Aggressive: OS + version + scripts + traceroute
nmap -sC 192.168.1.100      # Default scripts
```

## Output

```bash
nmap -oN output.txt 192.168.1.100    # Normal text
nmap -oX output.xml 192.168.1.100    # XML
nmap -oG output.gnmap 192.168.1.100  # Grepable
nmap -oA all_formats 192.168.1.100   # All three formats
```

## SOC Context: Recognizing Nmap in Logs

```
Signs of nmap scanning in logs:
- Many SYN packets to sequential ports in short timeframe
- TCP RST responses from closed ports
- Unusual user agents in web logs: "nmap scripting engine"
- Event ID 5156 (Windows Filtering Platform): many connection attempts
- Nmap default scripts hit: /robots.txt, various paths

Nmap timing templates (T0=slowest, T5=fastest):
nmap -T4 → aggressive timing (common in real attacks)
nmap -T1 → slow, stealthy (may evade rate-based detection)
```
