# Active Directory Basics for SOC Analysts

## What is Active Directory?

Active Directory (AD) is Microsoft's directory service that manages users, computers, and resources in an enterprise network. Most corporate environments run on AD — understanding it is essential for SOC work.

## Core AD Components

```
Forest
  └── Domain (company.com)
        ├── Organizational Units (OUs)
        │     ├── Users/
        │     ├── Computers/
        │     └── Groups/
        └── Domain Controllers (DCs)
              └── NTDS.dit (the AD database — treasure for attackers)
```

| Component | Description | Security Relevance |
|-----------|-------------|-------------------|
| **Domain Controller (DC)** | Server managing the domain | Compromise = game over |
| **NTDS.dit** | AD database with all hashes | Primary attacker target |
| **LDAP** | Protocol to query AD | LDAP enumeration by attackers |
| **Kerberos** | AD authentication protocol | Pass-the-ticket, Kerberoasting |
| **NTLM** | Legacy auth protocol | Pass-the-hash attacks |
| **GPO** | Group Policy Object | Attackers abuse for persistence |
| **krbtgt** | Kerberos ticket-granting account | Golden Ticket attack target |

## AD Attack Techniques (What to Detect)

| Attack | Description | Detection |
|--------|-------------|-----------|
| **Pass the Hash (PTH)** | Use NTLM hash instead of password | Event 4624 Type 3 from unusual source |
| **Pass the Ticket (PTT)** | Use stolen Kerberos ticket | Unusual Kerberos ticket usage |
| **Kerberoasting** | Request service tickets to crack offline | High volume Event 4769 |
| **AS-REP Roasting** | Attack accounts with no pre-auth | Event 4768 failures |
| **Golden Ticket** | Forge Kerberos tickets using krbtgt hash | Abnormal ticket lifetimes |
| **DCSync** | Replicate AD data to extract hashes | Event 4662 on DC |
| **BloodHound** | Map AD attack paths | Heavy LDAP queries |

## Privileged Groups to Monitor

| Group | Privileges | Why Monitor |
|-------|-----------|-------------|
| Domain Admins | Full domain control | Any addition = critical alert |
| Enterprise Admins | Full forest control | Any addition = critical alert |
| Schema Admins | Modify AD schema | Should be empty normally |
| Backup Operators | Backup files including NTDS.dit | Can extract creds |
| Account Operators | Manage user accounts | Can create backdoor accounts |
| Remote Desktop Users | RDP access | Lateral movement vector |

## Key Event IDs for AD Monitoring

```
4728/4732/4756  → User added to privileged group
4662            → Object operation on AD (DCSync)
4769            → Kerberos service ticket request (Kerberoasting)
4771            → Kerberos pre-auth failed (brute force)
4648            → Explicit credential logon (lateral movement)
5136            → AD object modified
```
