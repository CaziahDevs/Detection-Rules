# After-Hours Brute Force with Scheduled Task Creation
`rules/correlated/after_hours_brute_force_scheduled_task.yml`

## What it detects
This rule detects a pattern of multi-tactic adversarial behavior occurring during off-hours. Specifically, it correlates three conditions within a 30-minute window: repeated failed login attempts followed by a successful authentication, and the creation of a scheduled task shortly after. Activity is flagged between 10:00pm and 6:00am to surface behavior that may be intentionally timed to blend into low-traffic periods or evade analyst attention. Together these signals suggest a brute force credential access attempt followed by a persistence mechanism being established under the cover of off-hours activity.

## Log source
Windows Security Event Log.
| Event ID | Description |
|----------|-------------|
| 4625 | Failed login attempt |
| 4624 | Successful login |
| 4698 | Scheduled task created |

## Correlation logic
All three conditions must occur within a 30-minute window from the same source user or host to trigger this alert.

## False positives
- Legitimate administrative maintenance windows
- Known overnight batch processes
- Employees operating across international time zones

## ATT&CK mapping
| Field | Value |
|-------|-------|
| Tactic | Credential Access |
| Technique | T1110 — Brute Force |
| Tactic | Persistence |
| Technique | T1053.005 — Scheduled Task |
| Tactic | Defense Evasion |
| Technique | T1562 — Impair Defenses |