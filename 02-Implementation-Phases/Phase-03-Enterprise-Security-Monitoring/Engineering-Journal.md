# Engineering Journal

## Phase 03 — Enterprise Security Monitoring

**Project:** Menarol Enterprise Infrastructure
**Environment:** Pre-Production Proof of Concept
**Status:** Active

This journal records infrastructure implementation activities, troubleshooting, validation results, and outstanding engineering work.

Historical implementation details are preserved separately from the current operational baseline.

---

## Milestone 01 — Windows Event Collector Deployment

**Status:** Completed in original implementation

### Objective

Establish a centralized Windows Event Collector to receive security events from domain workstations.

### Implementation

- Initialized the Windows Event Collector service.
- Confirmed service availability.
- Prepared the server for Windows Event Forwarding subscriptions.
- Verified that the `ForwardedEvents` channel was available in Event Viewer.

### Historical Environment

The original implementation was documented on `MENAROL-SRV01`.

### Validation

- Collector initialization completed.
- The collector service was available.
- Event Viewer displayed the forwarded event channel.

### Outcome

The Windows Event Collector foundation was established for subsequent source-initiated event forwarding.

---

## Milestone 02 — Windows Event Forwarding

**Status:** Functionally validated; deployment standardization outstanding

### Objective

Configure source-initiated Windows Event Forwarding for domain workstations using centrally managed Group Policy settings.

### Original Implementation

- Created a source-initiated event subscription.
- Configured the workstation Subscription Manager through Group Policy.
- Configured the required WinRM and firewall settings.
- Applied workstation Group Policy.
- Investigated an initially empty forwarded event log.
- Validated collector, subscription, policy, and connectivity prerequisites.
- Identified the Security log access requirement.
- Added `NT AUTHORITY\NETWORK SERVICE` to the local `Event Log Readers` group for functional validation.
- Confirmed that the forwarding architecture functioned with the required access.
- Evaluated a Restricted Groups approach for centralized deployment.

### Troubleshooting Finding

The Restricted Groups object picker could not resolve the well-known `NETWORK SERVICE` principal through the Active Directory selection process.

The attempted approach was not adopted as an enterprise configuration standard.

### Historical Validation

Windows Event Forwarding was functionally validated on `MENAROL-WKS01`.

### Outstanding Work

A centrally managed method for configuring the required Security log access must be selected and validated.

The original plan to repeat clean deployment testing on `MENAROL-WKS02` was not completed in the supplied historical record.

### Engineering Outcome

The forwarding architecture was validated independently of the remaining deployment automation issue.

This distinction allows further monitoring integration while retaining the unresolved standardization requirement.

---

## Milestone 03 — Virtual Infrastructure Recovery and Baseline Reconciliation

**Status:** Current operational baseline established

### Context

During relocation of the virtualized environment, some implementation progress was lost and earlier configurations reappeared.

The recovered systems did not retain all names and configurations described in the original implementation records.

### Current Verified Environment

| Component               | Current Configuration |
| ----------------------- | --------------------- |
| Active Directory domain | `Menarol.local`       |
| Domain Controller       | `ServerM1`            |
| Windows Event Collector | `ServerM1`            |
| Domain workstation      | `COMPUTER01`          |
| Wazuh server            | `MENAROL-WAZUH01`     |

### Engineering Decision

The functioning infrastructure will not be renamed solely to match historical documentation.

Historical names remain in the original implementation records, while current operational documentation reflects the verified environment.

### Outstanding Work

- Revalidate historical endpoint policies where required.
- Document configuration differences.
- Establish recovery and configuration preservation requirements for future infrastructure relocation.

---

## Milestone 04 — Current Windows Event Forwarding Validation

**Status:** Validated

### Objective

Verify that the recovered domain workstation forwards selected Windows Security events to the current collector.

### Current Configuration

**Collector:** `ServerM1`
**Workstation:** `COMPUTER01`
**Subscription:** `Menarol Security Events`
**Group Policy:** `Menarol - Windows Event Forwarding`
**Collection Channel:** `ForwardedEvents`

### Implementation and Verification

- Confirmed the source-initiated event subscription.
- Confirmed the workstation received its forwarding configuration.
- Verified selected Windows Security events were collected on `ServerM1`.
- Confirmed forwarded events originated from `COMPUTER01`.

### Outcome

The current Windows Event Forwarding pipeline was operational and suitable for subsequent Wazuh integration.

### Limitation

The centrally managed Security log access prerequisite remains an open standardization item.

---

## Milestone 05 — Wazuh Server Deployment

**Status:** Operational in PoC

### Objective

Deploy a centralized security monitoring platform capable of receiving and investigating forwarded Windows events.

### Server Configuration

| Component        | Configuration             |
| ---------------- | ------------------------- |
| Hostname         | `MENAROL-WAZUH01`         |
| Operating system | Ubuntu Server 24.04.5 LTS |
| Wazuh version    | 4.14.8                    |
| Deployment model | All-in-one                |
| Virtualization   | VMware Workstation        |

### Components

- Wazuh Manager.
- Wazuh Indexer.
- Wazuh Dashboard.

### Validation

The Wazuh platform was accessible, and its monitoring interface was used to investigate Windows security events.

### Outcome

A functioning Wazuh monitoring platform was established within the PoC.

### Outstanding Work

Production capacity, retention, backup, recovery, and maintenance requirements have not yet been established.

---

## Milestone 06 — Wazuh Windows Agent Integration

**Status:** Validated

### Objective

Integrate the Windows Event Collector with Wazuh without changing the existing workstation forwarding architecture.

### Agent Configuration

**Agent Host:** `ServerM1`
**Agent ID:** `001`
**Agent Version:** `4.14.8-1`
**Windows Service:** `WazuhSvc`

### Implementation

- Installed the Wazuh Windows agent.
- Enrolled the agent with the Wazuh Manager.
- Verified the agent service was running.
- Configured ingestion of the Windows `ForwardedEvents` channel.

### Agent Configuration

The following configuration was added to the Wazuh agent configuration file:

```xml
<localfile>
  <location>ForwardedEvents</location>
  <log_format>eventchannel</log_format>
</localfile>
```

### Validation

The Wazuh agent log confirmed analysis of the `ForwardedEvents` event channel.

### Outcome

The collector was integrated with Wazuh, enabling the existing Windows Event Forwarding architecture to provide security events to the SIEM.

---

## Milestone 07 — End-to-End Security Event Validation

**Status:** Passed

### Objective

Verify the complete event collection and ingestion path from the Windows workstation to Wazuh.

### Event Path

`COMPUTER01` → `ServerM1` → `MENAROL-WAZUH01`

### Investigation Method

Used Wazuh Threat Hunting to review security events collected by the Windows agent.

Example investigation filters:

```text
agent.id: 001
```

```text
data.win.system.computer: "Computer01.Menarol.local"
```

### Observed Evidence

| Field                 | Observed Value             |
| --------------------- | -------------------------- |
| Wazuh agent           | `ServerM1`                 |
| Agent ID              | `001`                      |
| Original computer     | `Computer01.Menarol.local` |
| Windows event channel | `Security`                 |
| Event ID              | `4634`                     |
| Logon type            | `3`                        |
| Account observed      | `COMPUTER01$`              |

### Analysis

The Wazuh agent identified `ServerM1` as the collection host.

The forwarded Windows event retained the original computer information, identifying `COMPUTER01` as the source.

The original Windows channel appeared as `Security`, even though the event was ingested from the collector's `ForwardedEvents` channel.

This distinction is important when investigating events from multiple workstations through a centralized collector.

### Result

**Passed:** A selected Windows Security event was successfully collected through Windows Event Forwarding, ingested by Wazuh, and identified through Threat Hunting.

### Limitation

This test establishes event ingestion and source attribution.

It does not establish complete detection coverage, production readiness, or successful validation of every selected Windows Security Event ID.

---

## Milestone 08 — Controlled Authentication Monitoring

**Status:** Planned — Not Yet Executed

### Objective

Validate the collection and investigation of failed Windows authentication activity.

### Planned Test

1. Verify the relevant Windows audit configuration.
2. Select an authorized test account.
3. Generate controlled failed authentication attempts.
4. Confirm Event ID `4625` at the appropriate Windows event source.
5. Verify collection through Windows Event Forwarding.
6. Confirm visibility in Wazuh.
7. Review event details and detection behavior.
8. Capture sanitized validation evidence.
9. Record findings and any required configuration changes.

Account lockout monitoring using Event ID `4740` will be evaluated separately.

### Acceptance Criteria

- Expected authentication events are generated.
- Events reach the configured collector.
- Wazuh ingests the events.
- The originating system can be identified.
- Detection behavior and limitations are documented.

---

## Open Engineering Items

| Item                                           | Status         |
| ---------------------------------------------- | -------------- |
| Centralized Security log permission deployment | Open           |
| Revalidation of historical endpoint policies   | Pending        |
| Controlled failed-authentication detection     | Validated 2026-10-09 |
| Account lockout monitoring                     | Planned        |
| Privileged group change monitoring             | Planned        |
| PowerShell logging                             | Planned        |
| Sysmon evaluation                              | Planned        |
| Custom Wazuh detection rules                   | Planned        |
| Monitoring retention and backup requirements   | Pending        |
| Production migration assessment                | Pending        |

---

## Current Engineering Status

The current environment has demonstrated successful centralized Windows security event collection and Wazuh ingestion.

Controlled failed-authentication monitoring and local ServerM1 hardening/FIM tests are now recorded in the dated entry below. Account-lockout testing, assessment reliability investigation, and additional detection engineering remain open.

Future journal entries will record the date, configuration changes, validation evidence, observed results, troubleshooting findings, and outstanding actions for each activity.

---

## 2026-10-09 — Focused Security Monitoring and Hardening Validation

**Status:** Four focused exercises validated in the PoC; operational follow-up remains open.

The supplied [validation record](Validation-2026-10-09.md) records COMPUTER01 → WEF → ServerM1/WEC → Wazuh agent 001 → MENAROL-WAZUH01, with original-source attribution in Menarol.local. It supersedes the earlier planned status of Milestone 08 for failed-logon testing only.

- Two authorised 4625 records triggered built-in Wazuh rule 60122, severity 5. This was controlled testing, not a real attack or validated brute-force correlation rule.
- WEF delivery timeout changed from 900000 to 30000 milliseconds; precise end-to-end latency improvement was not measured.
- Minimum password length changed from 7 to 14, verified in Active Directory and local ServerM1 SCA check 27003.
- Initial baseline: 95 passed / 264 failed, 26%. Pre-hardening reassessment: 98 passed / 261 failed, 27%; three existing-policy checks corrected without configuration changes. Final hardening retest: 99 passed / 260 failed, 27%; one additional check passed after minimum password length changed from 7 to 14.
- SCA results were inconsistent after reboot. Reassessment passed following an agent restart, but the root cause remains unresolved.
- Local ServerM1 FIM verified added/modified/deleted events under rules 554/550/553. SCA and FIM were not tested on COMPUTER01.

Temporary secplus.test account cleanup and GPO backup confirmation remain unverified. Account-lockout testing, custom rules, advanced logging, WEF permission automation, and production readiness remain pending. Integration of this evidence changed repository documentation only; no running infrastructure was changed during the repository work.

---

## 2026-10-09 — Cleanup Verification Clarification

User-supplied verification confirms `secplus.test` is disabled (`Enabled=False`) and `C:\Menarol-FIM-Test\monitoring-test.txt` is absent (`Test-Path=False`). The empty demonstration folder and its FIM configuration remain intentionally retained.

This clarification supersedes the pending account/file cleanup status in the earlier 9 October entry, which is retained as history. See the [updated validation record](Validation-2026-10-09.md). GPO backup confirmation remains unverified. SCA inconsistency after reboot, account-lockout testing, custom rules, advanced logging, WEF permission automation, and production readiness remain unresolved or pending.
