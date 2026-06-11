# ☁️ Project 02 — AWS IAM Access Control Lab

## Overview

Built a multi-user IAM environment with RBAC policies and least-privilege permissions, then **simulated privilege misuse scenarios** and monitored them via CloudTrail logs.

## Objective

Simulate a realistic enterprise AWS environment to practice identity-based threat detection — directly applicable to cloud SOC roles.

## Tools Used

| Tool | Purpose |
|------|---------|
| AWS IAM | User creation, RBAC policy assignment |
| AWS CloudTrail | API activity logging |
| AWS CloudWatch | Alert triggers on policy violations |

## Architecture

```
IAM Users Created:
├── admin-user     → AdministratorAccess (restricted)
├── dev-user       → S3 + EC2 read-only
├── auditor-user   → SecurityAudit (read-only)
└── attacker-sim   → Simulated privilege escalation
```

## Attack Scenarios Simulated

| Scenario | Action | Detection Method |
|----------|--------|-----------------|
| Privilege escalation | dev-user attempted admin API call | CloudTrail → AccessDenied event |
| Unauthorized S3 access | Cross-account bucket access attempt | CloudTrail → GetObject denied |
| Credential stuffing sim | Multiple failed console logins | CloudWatch alarm on ConsoleLoginFailures |

## Key Findings

- All unauthorized API calls captured in CloudTrail within seconds
- CloudWatch metric filters successfully triggered SNS alerts on 3/3 simulated attacks
- Least-privilege policy blocked all privilege escalation attempts

## Files

| File | Description |
|------|-------------|
| `lab-setup.md` | Step-by-step IAM environment setup |
| `attack-scenarios.md` | Simulated attack documentation |
| `cloudtrail-findings.md` | Log analysis and alert review |
| `screenshots/` | CloudTrail events, CloudWatch alarms |

## Key Takeaways

- CloudTrail is a powerful SIEM data source for AWS environments
- Least-privilege is a detection enabler — violations stand out immediately
- AccessDenied events in CloudTrail are high-value SOC signals
