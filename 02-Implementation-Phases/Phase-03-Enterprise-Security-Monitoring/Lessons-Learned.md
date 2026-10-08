# Lessons Learned

## Phase 03 — Enterprise Security Monitoring

**Project:** Menarol Enterprise Infrastructure
**Environment:** Pre-Production Proof of Concept

This document records technical findings, troubleshooting lessons, and engineering improvements identified during the implementation of Windows Event Forwarding and Wazuh security monitoring.

---

## Lesson 001 — Validate the Entire Event Forwarding Chain

### Observation

Windows Event Forwarding depends on several components working together:

- Windows Event Collector.
- Event subscription configuration.
- Group Policy delivery.
- Windows Remote Management.
- Windows Firewall.
- Source authorization.
- Event log permissions.

An empty `ForwardedEvents` log does not identify which component failed.

### Lesson

Each layer must be validated independently rather than assuming the problem is with the collector or subscription.

### Future Application

Use a structured troubleshooting process that verifies workstation policy, service configuration, connectivity, authorization, event generation, and collection.

---

## Lesson 002 — Security Log Forwarding Has Additional Permission Requirements

### Observation

Forwarding Windows Security events required appropriate access to the source Security log.

In the original validated configuration, adding `NT AUTHORITY\NETWORK SERVICE` to the workstation's local `Event Log Readers` group established the necessary access.

### Lesson

A functioning WinRM connection and subscription do not automatically guarantee that the forwarding service can read every selected event channel.

### Future Application

Verify event channel permissions when troubleshooting missing Security events.

Evaluate permission changes for security impact before applying them across enterprise endpoints.

---

## Lesson 003 — Manual Validation Is Not the Same as Enterprise Deployment

### Observation

A manual permission change established that the Windows Event Forwarding architecture worked.

However, the configuration had not been converted into a centrally managed, repeatable deployment.

### Lesson

Technical functionality and enterprise deployment readiness are separate acceptance criteria.

### Future Application

Follow this sequence:

1. Validate the technology.
2. Identify manual prerequisites.
3. Research a supported centralized deployment method.
4. Test the proposed method.
5. Confirm repeatability.
6. Document and approve the standard.

---

## Lesson 004 — Do Not Standardize an Unverified Group Policy Method

### Observation

Restricted Groups was evaluated for managing local group membership.

During implementation, the Group Policy editor could not resolve `NT AUTHORITY\NETWORK SERVICE` through the Active Directory object picker.

The proposed configuration was not successfully validated.

### Lesson

A configuration method should not become an enterprise standard merely because it appears in technical guidance.

### Future Application

Test proposed Group Policy configurations in the target environment before adopting them.

Document unsuccessful approaches so they are not repeatedly introduced without new evidence.

---

## Lesson 005 — Avoid Changing Architecture During Configuration

### Observation

The original WEF implementation became unnecessarily confusing when recommendations changed between Restricted Groups and Group Policy Preferences before the technical research was resolved.

### Lesson

Implementation should follow an agreed technical approach unless validation produces evidence that requires reconsideration.

### Future Application

Use a controlled sequence:

1. Research.
2. Evaluate alternatives.
3. Record the decision.
4. Implement.
5. Validate.
6. Document the outcome.

Changes in approach should be supported by a clear technical reason.

---

## Lesson 006 — Functional Progress and Engineering Debt Can Be Tracked Separately

### Observation

Windows Event Forwarding was functionally validated while the zero-touch deployment of the Security log permission remained unresolved.

### Lesson

An outstanding standardization improvement does not necessarily invalidate a successful functional test.

However, the limitation must remain visible and must not be represented as completed.

### Future Application

Maintain separate statuses for:

- Functional validation.
- Deployment automation.
- Operational readiness.
- Production approval.

---

## Lesson 007 — Reuse Validated Infrastructure Before Adding New Components

### Observation

The Windows Event Collector was already receiving selected workstation security events before Wazuh was introduced.

Instead of immediately deploying a Wazuh agent to every workstation, the existing collector was integrated with Wazuh.

### Lesson

A validated infrastructure component can sometimes be extended to support additional capabilities without redesigning the entire architecture.

### Future Application

Evaluate existing collection mechanisms before introducing new agents, services, or dependencies.

Document the trade-offs of centralized collection, including collector availability, event coverage, and potential collection bottlenecks.

---

## Lesson 008 — Distinguish the Collection Agent from the Original Event Source

### Observation

The Wazuh Windows agent was installed on `ServerM1`, while the observed Security event originated from `COMPUTER01`.

The Wazuh record identified the collection agent as `ServerM1` and retained the original computer name in the Windows event data.

### Lesson

The system forwarding or ingesting an event is not necessarily the system where the activity occurred.

### Future Application

During investigations, examine both:

- The Wazuh agent identity.
- The original Windows event computer field.

This distinction becomes increasingly important when a collector receives events from multiple workstations.

---

## Lesson 009 — Understand the Difference Between ForwardedEvents and the Original Event Channel

### Observation

The Wazuh agent was configured to read the collector's `ForwardedEvents` channel.

However, an ingested event identified its original Windows event channel as `Security`.

### Lesson

The collection channel and the event's original source channel represent different parts of the logging process.

### Future Application

When filtering events in Wazuh, verify which fields describe the collection mechanism and which describe the original Windows event.

Avoid assuming that every event collected through `ForwardedEvents` will report that channel as its original source.

---

## Lesson 010 — Validate the Entire SIEM Ingestion Path

### Observation

Successful event forwarding into Windows Event Collector did not, by itself, prove that Wazuh was receiving those events.

Additional validation was performed after installing the Wazuh agent and configuring it to read `ForwardedEvents`.

An event originating from `COMPUTER01` was subsequently identified through Wazuh Threat Hunting.

### Lesson

Event collection and SIEM ingestion are separate technical stages.

Each stage requires its own validation.

### Future Application

Verify the complete sequence:

1. Event generated on the source.
2. Event received by the collector.
3. Collection agent reads the event.
4. SIEM receives and processes the event.
5. Event is accessible for investigation.
6. Original source information remains identifiable.

---

## Lesson 011 — Event Visibility Does Not Establish Detection Coverage

### Observation

Wazuh successfully displayed a forwarded Windows Security event with Event ID `4634`.

This confirmed that the event ingestion path was functioning.

It did not demonstrate that failed authentication, account lockout, privilege changes, or other security scenarios had been successfully detected.

### Lesson

Collecting security telemetry is not the same as validating detection logic.

### Future Application

Develop controlled test cases for each monitoring objective.

Record the expected event, actual event, Wazuh behavior, and investigation outcome.

Do not report a detection as validated until the corresponding scenario has been tested.

---

## Lesson 012 — Virtual Machine Recovery Requires Configuration Revalidation

### Observation

During relocation of the virtualized environment, some implementation progress was lost and earlier system configurations reappeared.

The recovered infrastructure had different names and domain settings from the original documentation.

### Lesson

A virtual machine that boots successfully after relocation or recovery is not necessarily at the same configuration baseline as before the move.

### Future Application

After infrastructure recovery:

- Verify system identity and domain membership.
- Confirm required services.
- Validate Group Policy and security settings.
- Test critical integrations.
- Compare the recovered environment against documented baselines.
- Record differences and unresolved changes.

Avoid making unnecessary infrastructure changes simply to match historical documentation.

---

## Lesson 013 — Recovery Checkpoints and Documentation Serve Different Purposes

### Observation

The project uses VMware snapshots and engineering documentation to support implementation and recovery.

The relocation experience demonstrated the importance of knowing which configuration state is actually available after a recovery operation.

### Lesson

Snapshots can support short-term rollback, but they do not replace independent backups or configuration documentation.

### Future Application

Establish a recovery approach that includes:

- Documented configuration baselines.
- Appropriate VM recovery checkpoints.
- Independent backup requirements.
- Verified restore procedures.
- Clear identification of recovery points.

For domain controllers, recovery procedures must account for Active Directory consistency and supported restoration methods.

---

## Lesson 014 — Keep Engineering Documentation Aligned with Verified Infrastructure

### Observation

Earlier project records referenced `MENAROL-SRV01`, `MENAROL-WKS01`, and `menarol.com`, while the current verified monitoring environment uses `ServerM1`, `COMPUTER01`, and `Menarol.local`.

### Lesson

Historical implementation records and current infrastructure inventories serve different purposes.

Rewriting historical records to match current names can obscure what actually occurred.

### Future Application

Preserve original engineering history while maintaining a separate, current operational baseline.

Document infrastructure changes, recovery events, and configuration differences explicitly.

---

## Lesson 015 — Treat Production Readiness as a Separate Engineering Decision

### Observation

The WEF-to-Wazuh monitoring pipeline has been validated within the VMware PoC.

However, production hosting, backup, retention, licensing, capacity, and operational requirements remain under evaluation.

### Lesson

A successful proof of concept demonstrates technical feasibility under tested conditions, not complete production readiness.

### Future Application

Evaluate production deployment through documented requirements, cost comparisons, risk assessment, and operational acceptance criteria.

Avoid selecting a production migration method before those requirements have been reviewed.

---

## Summary

Phase 03 has demonstrated the importance of separating infrastructure functionality, security monitoring visibility, detection validation, and production readiness.

The next engineering priority is to perform controlled failed-authentication testing and verify whether the existing Windows Event Forwarding and Wazuh integration provides the expected monitoring evidence.

Future lessons will be added as additional detection scenarios, endpoint logging capabilities, and operational requirements are tested.
