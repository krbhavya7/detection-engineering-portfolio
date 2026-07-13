# Project: Detection Coverage Map

## Objective
Map current detection coverage for the Credential Access tactic (MITRE ATT&CK) before
building any new detections, to prioritize effort based on real gaps rather than guesswork.

## Method
Rated each technique None / Partial / Strong, assuming standard Windows Security logs +
Sysmon flowing into a SIEM with basic correlation rules. Full reasoning is in the Navigator
layer (`navigator-layer.json`) as per-technique comments.

## Results

![Coverage heatmap](./coverage-heatmap.png)

| Technique | Rating | Reasoning |
|---|---|---|
| Brute Force | Partial | 4625 threshold rule catches classic brute force; password spray likely evades it. |
| Credentials from Password Stores | Partial | Process access to vault/browser files is logged; no tuned rule yet. |
| OS Credential Dumping | Strong | Sysmon Event ID 10 on lsass.exe is a mature, widely-used detection pattern. |
| Steal or Forge Kerberos Tickets | None | 4769 logged, but no rule for Kerberoasting or anomalous TGT lifetimes. |
| Steal Web Session Cookie | None | No telemetry targets browser cookie DB access; needs EDR-level monitoring. |
| Input Capture | None | Keylogging evades standard logs; needs EDR behavioral monitoring. |
| Unsecured Credentials | Partial | Command-line credential exposure visible via Sysmon; no active file/script scan. |
| Network Sniffing | None | Passive sniffing generates no host logs; needs network-level monitoring. |
| Modify Authentication Process | None | Auth package registry changes aren't monitored; needs a purpose-built rule. |
| Multi-Factor Authentication Interception | None | Not visible in host logs; needs identity provider (e.g., Entra ID) sign-in logs. |

**Summary:** 1 Strong, 3 Partial, 6 None out of 10 techniques assessed.
An ATT&CK Navigator heatmap showing current detection coverage for a chosen tactic,
with reasoning for each rating.


## Next steps
These gaps directly inform which detections to prioritize building next.# Project 1: Detection Coverage Map

Status: Complete

