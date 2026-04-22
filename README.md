# Detection Rules

A collection of custom detection rules written in Sigma, mapped to the MITRE ATT&CK framework.

## Philosophy
Each rule is built around correlation-based detection logic — alerting on patterns of behavior rather than isolated events. The goal is high fidelity detection with a controllable false positive surface.

## Structure
Rules are organized by tactic and include documentation covering:
- Behavior being detected
- Relevant log sources
- ATT&CK tactic and technique mapping
- Known false positive considerations

## Rules Index
| Rule | Tactic | Severity |
|------|--------|----------|
| [Suspicious LSASS Access](rules/credential-access/suspicious-lsass-access.yml) | Credential Access | Medium |
| [After-Hours Brute Force with Scheduled Task](rules/correlated/brute_force_success_with_scheduled_task/brute_force_success_with_scheduled_task.yml) | Credential Access, Persistence, Defense Evasion | High |
| [Pass the Ticket](rules/lateral-movement/pass_the_ticket.yml) | Lateral Movement | High |
| [LSASS to Pass the Ticket](rules/correlated/lsass_to_pass_the_ticket/lsass_to_pass_the_ticket.yml) | Credential Access, Lateral Movement | Critical |
## Status
This is a living repository, updated as new detection use cases are developed.

## Log Sources
- Firewall — port scans, traffic from blocked countries, access to critical ports, overly permissive rules
- IPS/IDS — abnormal traffic patterns, known vulnerability exploits, malware downloads
- WAF — SQL injection, XSS, CSRF, bot traffic
- Linux — privilege escalation, unauthorized root access, SSH anomalies, changes to /etc/passwd or /etc/shadow
- Windows — log deletion, Domain Admin group changes, RDP attempts, unauthorized account creation
- Linux — privilege escalation, unauthorized root access, SSH anomalies, changes to /etc/passwd or /etc/shadow
- Network devices — insecure protocols like Telnet, policy violations, critical ports going down
- Endpoint — antivirus quarantine events, EDR threat detections, EPP blocks
- VPN — after-hours access, impossible travel, unauthorized software in VPN traffic
- VM Platform — privilege changes, VM creation/deletion, missed backups
- Vulnerability Management — critical vulns detected, scan failures

---
*Mapped to [MITRE ATT&CK](https://attack.mitre.org/)*
