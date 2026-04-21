# Suspicious LSASS Access
`rules/credential-access/suspicious_lsass_access.yml`

## What it detects
This rule detects non-whitelisted processes opening a handle to `lsass.exe` with memory read permissions. LSASS (Local Security Authority Subsystem Service) is the Windows process responsible for handling authentication — it stores credential material in memory including password hashes and Kerberos tickets, making it a high value target for attackers.

## Why handle-based detection matters
Before any credential dumping can occur, the attacking tool must first request a handle to `lsass.exe` from the operating system, declaring its intended permissions. This handle request happens before the dump completes, making it an early-stage detection opportunity. This rule targets that moment of intent — catching the setup rather than waiting for the payload.

## Mimikatz and similar tools
The most common credential dumping tool, Mimikatz, requests specific memory read permission flags when accessing LSASS — `0x1010` and `0x1410`. These flags represent read virtual memory and query information permissions. By filtering on these specific values combined with an unexpected source process, this rule achieves high fidelity detection with a controllable false positive surface.

## Log source
Sysmon Event ID 10 (Process Access). Standard Windows logs do not capture process handle requests at this level — Sysmon must be deployed and configured to generate the telemetry this rule depends on.

## False positives
Legitimate LSASS access occurs from a well-defined set of processes including EDR agents, backup software, and Windows system processes. These are accounted for in the filter condition. Any process outside this whitelist requesting memory read access to `lsass.exe` should be treated as suspicious.

## ATT&CK mapping
| Field | Value |
|-------|-------|
| Tactic | Credential Access |
| Technique | T1003.001 — OS Credential Dumping: LSASS Memory |