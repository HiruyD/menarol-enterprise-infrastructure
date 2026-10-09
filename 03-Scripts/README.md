# Read-only Verification Runbook

These read-only checks are grouped by machine. The [validation record](../02-Implementation-Phases/Phase-03-Enterprise-Security-Monitoring/Validation-2026-10-09.md) contains the observed results; rerun and review the checks before treating them as current system health.

## Verification status and scope

| Label | Meaning |
| --- | --- |
| Recorded manual verification | The command or dashboard filter is preserved in the documentation or supplied cleanup evidence, with an observed result. |
| Reconstructed inspection example | The check is documented, but its exact command line was not retained. The example command has not been run against the lab. |
| Automation | No automation has been validated here; WEF permission deployment automation is still pending. |

Run Windows commands locally in PowerShell with permission to read the logs and policy. AD queries require the ActiveDirectory module on ServerM1. Record the host, timestamps, timezone, and dashboard window. If no events are returned, check the time window and log retention before assuming collection has failed.

## COMPUTER01 — Windows event source

**Reconstructed inspection examples:** auditing and source 4625 records were manually inspected in the validation exercise; these exact command forms were not preserved.

```powershell
auditpol /get /subcategory:"Logon"
Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4625} -MaxEvents 10 |
    Select-Object TimeCreated, MachineName, Id, Message
```

The recorded Logon audit setting was Success and Failure. The authorised `secplus.test` test generated 4625 records, logon type 2, status `0xC000006D`, and substatus `0xC000006A`. Review the account and event fields before attributing a record to the exercise. The account is now disabled; these inspection steps do not generate new logons or test account lockout.

## ServerM1 — WEC, domain policy, and agent 001

### Recorded manual verification — password policy and cleanup

The AD policy command is recorded in the validation notes. The cleanup commands came from the supplied package; their results were subsequently confirmed.

```powershell
Get-ADDefaultDomainPasswordPolicy
Get-ADUser secplus.test | Select-Object SamAccountName, Enabled
Test-Path 'C:\Menarol-FIM-Test\monitoring-test.txt'
```

Recorded results: `MinPasswordLength` 14, test account `Enabled=False`, and test file `Test-Path=False`. The empty `C:\Menarol-FIM-Test` demonstration folder and its FIM configuration remain intentionally retained. The default domain lockout threshold was 0 in the exercise; account-lockout testing remains pending. GPO backup confirmation is separate and remains unverified.

### Reconstructed inspection examples — collector and service

Subscription status, delivery configuration, forwarded events, and the running agent service were manually checked, but their exact inspection commands were not retained.

```powershell
wecutil gr "Menarol Security Events"
wecutil gs "Menarol Security Events"
Get-WinEvent -FilterHashtable @{LogName='ForwardedEvents'; Id=4625} -MaxEvents 10 |
    Select-Object TimeCreated, MachineName, Id, Message
Get-Service -Name WazuhSvc
```

The recorded subscription was Active, LastError 0, with source `Computer01.Menarol.local`. Configuration inspection showed the delivery timeout changed from 900000 to 30000 milliseconds. That value is a delivery setting; precise end-to-end latency improvement was not measured. Agent 001 on ServerM1 ingests `ForwardedEvents`; the original Windows computer identifies COMPUTER01. Inspect the agent's configured `ossec.conf` and `ossec.log` locally through its actual installation directory if further investigation is needed; the records do not preserve an absolute installation path.

SCA and FIM run locally on ServerM1. The documented real-time directory entry is retained under the existing syscheck configuration; the scheduled scan interval remained 43200 seconds. Do not infer COMPUTER01 SCA or FIM coverage from forwarded workstation events.

## MENAROL-WAZUH01 — dashboard investigation

Use the existing Wazuh Dashboard served by MENAROL-WAZUH01. No Linux host verification command was preserved for these four exercises, so none is represented here as manually tested.

### Recorded manual verification — Threat Hunting filters

Apply these documented filters to distinguish agent 001 from the original Windows source:

```text
agent.id: 001
```

```text
data.win.system.computer: "Computer01.Menarol.local"
```

The authentication screenshot preserves this combined filter:

```text
agent.id: "001" AND data.win.system.eventID: "4625" AND data.win.eventdata.targetUserName: "secplus.test"
```

Use a time window that includes the recorded test. Two authorised records matched built-in rule 60122, severity 5. This was not a real attack or a validated brute-force correlation rule.

### Recorded manual verification — SCA and FIM views

Select ServerM1 / agent 001 in the dashboard and review the [assessment](../02-Implementation-Phases/Phase-03-Enterprise-Security-Monitoring/Validation-2026-10-09.md#3-finding-remediation-and-retest) and [integrity results](../02-Implementation-Phases/Phase-03-Enterprise-Security-Monitoring/Validation-2026-10-09.md#4-real-time-file-integrity-monitoring).

| View | Recorded result |
| --- | --- |
| Configuration assessment | Check 27003 passed after minimum password length changed from 7 to 14. Initial baseline: 95 passed / 264 failed, 26%. Pre-hardening reassessment: 98 passed / 261 failed, 27%. Final hardening retest: 99 passed / 260 failed, 27%; one additional check passed after the minimum-length change. |
| File integrity events | Local test file added, modified, and deleted under rules 554/550/553, severities 5/7/7. |

Three existing-policy SCA checks corrected on the pre-hardening reassessment without configuration changes, not additional remediation. Results became inconsistent after reboot; reassessment passed, but the root cause remains unresolved. Viewing a saved result does not run a new scan.

## Follow-up and related records

For pending tests and operational work, see the [validation record](../02-Implementation-Phases/Phase-03-Enterprise-Security-Monitoring/Validation-2026-10-09.md#remaining-work-and-limits). These commands inspect existing state; they do not apply policy changes or generate new test activity.

- [Architecture and monitoring scope](../04-Network-Diagrams/README.md)
- [Portfolio overview](../05-GitHub-Portfolio/README.md)
- [Phase 03 decisions](../02-Implementation-Phases/Phase-03-Enterprise-Security-Monitoring/Decisions.md)
- [Phase 03 lessons](../02-Implementation-Phases/Phase-03-Enterprise-Security-Monitoring/Lessons-Learned.md)
