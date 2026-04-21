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
| [Suspicious LSASS Access](rules/credential-access/suspicious_lsass_access.yml) | Credential Access | Medium |
| [After-Hours Brute Force with Scheduled Task](rules/correlated/after_hours_brute_force_scheduled_task.yml) | Credential Access, Persistence, Defense Evasion | High |

## Status
This is a living repository, updated as new detection use cases are developed.

---
*Mapped to [MITRE ATT&CK](https://attack.mitre.org/)*
