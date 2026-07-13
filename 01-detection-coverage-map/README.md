# Project: Detection Coverage Map

**Status:** Complete
**Tactic assessed:** Credential Access (TA0006)
**Framework:** MITRE ATT&CK Enterprise, v15

## Objective
Map current detection coverage for the Credential Access tactic (MITRE ATT&CK) before
building any new detections, to prioritize effort based on real gaps rather than guesswork.

## Method
Rated each technique None / Partial / Strong, assuming standard Windows Security logs +
Sysmon flowing into a SIEM with basic correlation rules. Full reasoning is in the Navigator
layer (`navigator-layer.json`) as per-technique comments.

## Rating criteria
Each technique was assessed against one question: *"With standard Windows Security logs and
Sysmon flowing into a SIEM with basic correlation rules, would this technique realistically
be detected?"*

| Rating | Meaning |
|---|---|
| **Strong** | A mature, commonly-available detection pattern exists (often built into SIEM content packs). |
| **Partial** | Relevant telemetry is logged, but no tuned rule exists, or the rule has a known evasion path. |
| **None** | No telemetry source or rule covers this technique with standard logging. |

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

## Limitations
- This is a desk assessment based on typical enterprise telemetry, not a measured result from
  a live environment; Project 2 builds the actual lab to validate or correct these ratings.
- Only top-level techniques were scored; sub-techniques (e.g., specific Kerberoasting variants)
  may have different individual coverage.
- Ratings reflect detection *capability*, not alerting maturity (e.g., whether an analyst would
  actually see and act on the alert in time).

## References
- [MITRE ATT&CK: Credential Access (TA0006)](https://attack.mitre.org/tactics/TA0006/)
- [ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator/)

## Next steps
These gaps directly inform which detections to prioritize building in later projects,
Starting with the SOC lab (Project 2) to generate real telemetry for validation.

