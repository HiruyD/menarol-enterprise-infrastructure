# Phase 03 — Enterprise Security Monitoring

**Project:** Menarol Enterprise Infrastructure
**Environment:** Pre-Production Proof of Concept
**Status:** In Progress
**Current Milestone:** Wazuh Integration Validated — Detection Testing Next

---

## 1. Overview

Phase 03 introduces centralized security event collection, auditing, and monitoring into the Menarol Enterprise Infrastructure.

Following the Active Directory foundation established in Phase 01 and the endpoint integration work performed in Phase 02, this phase focuses on improving visibility into Windows security activity.

The monitoring architecture combines native Microsoft event collection technologies with Wazuh SIEM.

The implementation follows a controlled engineering process: configure, validate, investigate, document, and improve.

The objective is to establish a repeatable security monitoring foundation that can be evaluated for future production deployment.

---

## 2. Objectives

- Centralize Windows security event collection.
- Configure Windows Event Forwarding through Group Policy.
- Validate security event transmission from domain workstations.
- Deploy a centralized security monitoring platform.
- Integrate forwarded Windows events with Wazuh.
- Investigate authentication and account management activity.
- Expand endpoint auditing and PowerShell visibility.
- Develop and validate security detections.
- Document configurations, testing results, and unresolved limitations.

---

## 3. Current Infrastructure

The following inventory reflects the most recently verified operational environment.

| System            | Operating System          | Role                                                                          |
| ----------------- | ------------------------- | ----------------------------------------------------------------------------- |
| `ServerM1`        | Windows Server 2022       | Active Directory Domain Controller, DNS, Windows Event Collector, Wazuh Agent |
| `COMPUTER01`      | Windows client            | Domain workstation and event forwarding source                                |
| `MENAROL-WAZUH01` | Ubuntu Server 24.04.5 LTS | Wazuh Manager, Indexer, and Dashboard                                         |

**Active Directory Domain:** `Menarol.local`
**Virtualization Platform:** VMware Workstation
**Wazuh Version:** 4.14.8

### Historical Configuration Note

Earlier implementation records reference `MENAROL-SRV01`, `MENAROL-WKS01`, `MENAROL-WKS02`, and the domain `menarol.com`.

Following relocation and recovery of the virtualized environment, older configurations reappeared and some implementation progress was lost.

The current inventory represents the environment subsequently verified during the monitoring integration.

Historical system names are retained in earlier engineering records to preserve implementation history.

---

## 4. Security Monitoring Architecture

The current architecture uses Windows Event Forwarding to collect workstation events and Wazuh to centralize their monitoring and investigation.

```text
                  Active Directory / Group Policy
                             ServerM1
                                |
                                v
                           COMPUTER01
                       Windows Security Log
                                |
                                | Windows Event Forwarding
                                v
                            ServerM1
                      Windows Event Collector
                         ForwardedEvents
                                |
                                | Wazuh Windows Agent
                                v
                        MENAROL-WAZUH01
                          Wazuh Manager
                          Wazuh Indexer
                          Wazuh Dashboard
                                |
                                v
                      Security Event Analysis
```

### Event Collection Flow

1. Windows generates security events on `COMPUTER01`.
2. Group Policy configures the workstation for source-initiated Windows Event Forwarding.
3. The Windows Event Collector on `ServerM1` receives selected events.
4. The forwarded events are stored in the `ForwardedEvents` Windows event channel.
5. The Wazuh agent on `ServerM1` reads the forwarded event channel.
6. Wazuh processes the ingested events and makes relevant security records available for investigation.

The Wazuh agent identifies the collection host, while the original Windows event data identifies the system that generated the event.

---

## 5. Milestone 3.1 — Windows Event Collector

**Status: Completed and Functionally Validated**

### Objectives

- Initialize Windows Event Collector.
- Confirm collector service functionality.
- Prepare centralized event subscriptions.
- Verify availability of the forwarded event log.

### Completed Work

- Initialized Windows Event Collector.
- Confirmed collector service availability.
- Verified the `ForwardedEvents` channel in Event Viewer.
- Prepared the collector for source-initiated subscriptions.

### Validation

The event collector successfully received security events originating from the domain workstation.

---

## 6. Milestone 3.2 — Windows Event Forwarding

**Status: Functionally Validated — One Standardization Item Open**

### Objectives

- Configure a source-initiated event subscription.
- Deploy forwarding settings through Group Policy.
- Configure required WinRM and firewall settings.
- Collect selected Windows Security events.
- Validate centralized collection.
- Reduce manual workstation-side configuration.

### Implemented Configuration

**Collector:** `ServerM1`
**Event Source:** `COMPUTER01`
**Subscription:** `Menarol Security Events`
**Group Policy Object:** `Menarol - Windows Event Forwarding`
**Collector Channel:** `ForwardedEvents`

The forwarding configuration is applied through the workstation's domain policy.

### Security Event Selection

The configured monitoring scope includes the following Windows Security Event IDs.

| Event ID | Description                                        |
| -------- | -------------------------------------------------- |
| 4624     | Successful account logon                           |
| 4625     | Failed account logon                               |
| 4634     | Account logoff                                     |
| 4648     | Logon attempted using explicit credentials         |
| 4672     | Special privileges assigned to a new logon         |
| 4720     | User account created                               |
| 4722     | User account enabled                               |
| 4723     | Password change attempted                          |
| 4724     | Password reset attempted                           |
| 4725     | User account disabled                              |
| 4726     | User account deleted                               |
| 4732     | Member added to a security-enabled local group     |
| 4733     | Member removed from a security-enabled local group |
| 4740     | User account locked out                            |

Event selection does not guarantee that every event type will be generated. The relevant Windows audit policies and test conditions must also be satisfied.

### Validation Results

- The workstation received its event forwarding configuration.
- The collector accepted forwarded events.
- Security events originating from `COMPUTER01` appeared on `ServerM1`.
- Forwarded event ingestion was subsequently validated through Wazuh.

### Open Engineering Improvement

The original WEF implementation identified a Security log access prerequisite involving `NT AUTHORITY\NETWORK SERVICE` and membership in the local `Event Log Readers` group.

A manual configuration was used during the original functional validation.

An attempted Restricted Groups approach was not adopted because the Group Policy object picker could not resolve the local well-known principal through Active Directory.

A supported, centrally managed deployment method has not yet been validated and documented.

The manual method must not be represented as the final enterprise deployment standard.

### Standardization Acceptance Criteria

- Deploy the required Security log access configuration centrally.
- Confirm the configuration applies to a newly domain-joined workstation.
- Verify forwarding after Group Policy refresh without manual intervention.
- Repeat validation across multiple workstations.
- Document the final configuration and recovery procedure.

---

## 7. Milestone 3.3 — Wazuh SIEM Deployment

**Status: Operational in the PoC**

### Objectives

- Deploy a centralized security monitoring server.
- Install Wazuh components.
- Enroll the Windows Event Collector as an agent.
- Ingest forwarded Windows events.
- Validate event visibility and source attribution.

### Wazuh Server

**Hostname:** `MENAROL-WAZUH01`
**Operating System:** Ubuntu Server 24.04.5 LTS
**Wazuh Version:** 4.14.8

The deployment includes:

- Wazuh Manager.
- Wazuh Indexer.
- Wazuh Dashboard.

The platform is deployed as an all-in-one installation within the VMware PoC environment.

### Windows Agent

**Agent Host:** `ServerM1`
**Agent ID:** `001`
**Agent Version:** `4.14.8-1`

The Wazuh Windows agent was installed, enrolled, and verified as operational.

### Forwarded Event Ingestion

The Wazuh agent configuration includes:

```xml
<localfile>
  <location>ForwardedEvents</location>
  <log_format>eventchannel</log_format>
</localfile>
```

This configuration instructs the agent to monitor the Windows `ForwardedEvents` event channel.

Agent logging confirmed that the channel was being analyzed.

---

## 8. End-to-End Monitoring Validation

**Status: Successfully Validated**

### Test Objective

Confirm that a security event generated on the domain workstation can be collected through Windows Event Forwarding and observed through the Wazuh monitoring platform.

### Verified Event Path

`COMPUTER01` → `ServerM1` → `MENAROL-WAZUH01`

### Validation Method

Wazuh Threat Hunting was used to inspect ingested Windows events.

The investigation included filtering for the collection agent and original event source.

Example filters:

```text
agent.id: 001
```

```text
data.win.system.computer: "Computer01.Menarol.local"
```

### Observed Results

The validated event record contained the following attributes:

| Field                          | Observed Value             |
| ------------------------------ | -------------------------- |
| Wazuh agent                    | `ServerM1`                 |
| Agent ID                       | `001`                      |
| Original Windows computer      | `Computer01.Menarol.local` |
| Original Windows event channel | `Security`                 |
| Observed Event ID              | `4634`                     |
| Logon type                     | `3`                        |

The event originated from the domain workstation and was collected through the Windows Event Collector.

The Wazuh event retained the original Windows computer information, allowing the source workstation to be identified even though the Wazuh agent was installed on the collector.

### Validation Outcome

**Passed:** The selected Windows Security event was successfully forwarded, ingested, and made available for investigation through Wazuh.

### Scope Limitation

This test validates the event collection and ingestion pipeline.

It does not establish that every selected Security Event ID has been tested, that all security activity is detected, or that alerting and incident response procedures are production-ready.

---

## 9. Next Milestone — Authentication Detection Testing

**Status: Planned**

### Objective

Validate the monitoring pipeline using controlled failed-authentication events.

### Planned Procedure

1. Establish the expected Windows audit configuration.
2. Select an authorized test account and workstation.
3. Generate a limited number of controlled failed logon attempts.
4. Confirm Security Event ID `4625` on the source or relevant authentication system.
5. Verify collection through Windows Event Forwarding.
6. Identify the corresponding record in Wazuh.
7. Review event fields, rule classification, and alert behavior.
8. Capture sanitized evidence.
9. Document findings and limitations.

Account lockout Event ID `4740` will be evaluated separately where appropriate.

Testing must avoid production credentials and unintended account lockouts.

### Acceptance Criteria

- The expected event is generated.
- The event reaches the configured collection point.
- The original event source can be identified.
- The event is visible through Wazuh.
- Detection behavior and limitations are documented.

---

## 10. Future Monitoring Milestones

### Advanced Windows Auditing

- Review Advanced Audit Policy settings.
- Validate authentication and account management events.
- Evaluate privilege use and object access auditing.
- Confirm event generation and forwarding requirements.

### PowerShell Logging

- Configure Script Block Logging.
- Evaluate Module Logging.
- Evaluate PowerShell transcription.
- Validate event generation and collection.

### Sysmon Deployment

- Evaluate Sysmon requirements.
- Select and review a suitable configuration.
- Deploy Sysmon in the test environment.
- Validate event generation and collection.

### Detection Engineering

- Develop custom Wazuh rules.
- Validate rules using controlled activity.
- Investigate false positives.
- Document detection logic and test evidence.

### Monitoring Operations

- Evaluate log retention and storage.
- Document platform maintenance requirements.
- Define initial security investigation procedures.
- Evaluate monitoring coverage and escalation requirements.

---

## 11. Evidence and Documentation

Engineering evidence will be organized to demonstrate implementation and validation without exposing credentials or unnecessary sensitive information.

Planned evidence includes:

- Windows Event Forwarding subscription configuration.
- Group Policy configuration and application.
- Forwarded events in Windows Event Viewer.
- Wazuh agent enrollment and operational status.
- Wazuh event ingestion and original source attribution.
- Controlled authentication detection results.

Supporting records are maintained in the Phase 03 engineering documentation:

- `Decisions.md` — Engineering decisions and rationale.
- `Engineering-Journal.md` — Implementation history and validation records (existing filename; pending correction).
- `Lessons-Learned.md` — Troubleshooting findings and improvements.

---

## 12. Current Status

**Windows Event Collector:** Validated
**Windows Event Forwarding:** Functionally validated
**Wazuh Deployment:** Operational in PoC
**Wazuh Event Ingestion:** Validated
**Authentication Detection Testing:** Next milestone
**Advanced Audit Policy:** Further validation planned
**PowerShell Monitoring:** Planned
**Sysmon:** Planned
**Custom Wazuh Rules:** Planned
**Production Readiness:** Not established

### Next Engineering Activity

Conduct a controlled Windows authentication failure test and trace the resulting event through the Windows Event Forwarding and Wazuh monitoring pipeline.

Record the test procedure, observed results, detection behavior, and supporting evidence before proceeding to additional monitoring scenarios.
