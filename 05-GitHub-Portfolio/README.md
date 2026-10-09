# Security Monitoring Portfolio

I used the existing Menarol lab to trace Windows events, test failed-logon alerts, harden one password-policy setting, and check file integrity monitoring. The [9 October 2026 validation record](../02-Implementation-Phases/Phase-03-Enterprise-Security-Monitoring/Validation-2026-10-09.md) is the authoritative source for the procedures, results, and limitations.

## Four validated exercises

| Exercise | Verified outcome | Evidence |
| --- | --- | --- |
| [Centralised Windows monitoring](../02-Implementation-Phases/Phase-03-Enterprise-Security-Monitoring/Validation-2026-10-09.md#1-centralised-windows-monitoring) | COMPUTER01 events reached Wazuh through ServerM1/WEC and agent 001, preserving original-source attribution. | [Monitoring overview](../02-Implementation-Phases/Phase-03-Enterprise-Security-Monitoring/evidence/2026-10-09/01-monitoring-overview.png) |
| [Controlled authentication detection](../02-Implementation-Phases/Phase-03-Enterprise-Security-Monitoring/Validation-2026-10-09.md#2-controlled-authentication-detection) | Two authorised 4625 records triggered built-in rule 60122, severity 5. No real attack or brute-force correlation is claimed. | [Authentication alerts](../02-Implementation-Phases/Phase-03-Enterprise-Security-Monitoring/evidence/2026-10-09/02-authentication-alerts.png) |
| [Password-policy hardening and retest](../02-Implementation-Phases/Phase-03-Enterprise-Security-Monitoring/Validation-2026-10-09.md#3-finding-remediation-and-retest) | Minimum length changed from 7 to 14, verified in AD and local ServerM1 SCA check 27003. One additional check passed; the pre-hardening reassessment and final hardening retest both displayed 27%. | [Hardening result](../02-Implementation-Phases/Phase-03-Enterprise-Security-Monitoring/evidence/2026-10-09/03-password-hardening-result.png) |
| [Local file integrity monitoring](../02-Implementation-Phases/Phase-03-Enterprise-Security-Monitoring/Validation-2026-10-09.md#4-real-time-file-integrity-monitoring) | ServerM1 added/modified/deleted events matched rules 554/550/553 for one harmless test file. | [Integrity events](../02-Implementation-Phases/Phase-03-Enterprise-Security-Monitoring/evidence/2026-10-09/04-file-integrity-events.png) |

## Engineering lessons

The [lessons](../02-Implementation-Phases/Phase-03-Enterprise-Security-Monitoring/Lessons-Learned.md) and [decisions](../02-Implementation-Phases/Phase-03-Enterprise-Security-Monitoring/Decisions.md) record the troubleshooting findings:

- Distinguish the original workstation from the collector agent, and inspect each stage of the event path.
- Compare assessment findings with system evidence before remediation. Initial baseline: 95 passed / 264 failed, 26%. Three existing-policy checks corrected without configuration changes on the pre-hardening reassessment: 98 passed / 261 failed, 27%. Final hardening retest: 99 passed / 260 failed, 27%; one additional check passed after minimum password length changed from 7 to 14.
- Treat a passing retest separately from root-cause resolution. SCA inconsistency after reboot remains unresolved.
- A delivery timeout change from 900000 to 30000 milliseconds is not a measured end-to-end latency improvement. A monitored file change is evidence of activity, not proof of compromise.

## Current boundaries

SCA and FIM were tested locally on ServerM1. The test account is disabled and the test file is absent; the empty folder and FIM configuration are retained for demonstrations. [Cleanup checks](../02-Implementation-Phases/Phase-03-Enterprise-Security-Monitoring/Validation-2026-10-09.md#cleanup-verification--9-october-2026) are recorded separately.

GPO backup confirmation, account-lockout testing, custom rules, advanced logging, WEF permission automation, and production readiness remain pending. The tests cover specific lab scenarios, not CIS compliance or complete detection coverage.

[Architecture diagram](../04-Network-Diagrams/README.md) · [Read-only verification runbook](../03-Scripts/README.md) · [Roadmap](../ROADMAP.md) · [Root overview](../README.md)
