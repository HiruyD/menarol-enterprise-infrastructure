# Changelog — Menarol Enterprise Infrastructure

This changelog records significant infrastructure milestones, validated capabilities, and documentation changes associated with the Menarol Enterprise Infrastructure proof of concept.

The project follows a phased engineering implementation model. Entries describe infrastructure progress rather than commercial software releases.

Dates are included only when supported by engineering records.

---

## Unreleased — Repository Publication Preparation

**Status:** In Progress

### Documentation

- Repositioned the repository as an enterprise infrastructure pre-production proof of concept supporting Menarol's business operations.
- Updated the root README to explain business objectives, implementation scope, current infrastructure, and validation status.
- Established a project roadmap covering infrastructure implementation, security monitoring, detection engineering, and production readiness.
- Identified repository navigation and file naming improvements.
- Identified the need to reconcile historical infrastructure records with the currently verified environment.

### Engineering Decisions

- Retain the operational infrastructure configuration rather than renaming systems solely to match historical documentation.
- Preserve historical implementation records following VM relocation and recovery.
- Keep production migration and hosting decisions open pending cost and feasibility assessment.
- Distinguish completed PoC validation from production deployment readiness.

### Outstanding

- Standardize Phase 03 documentation.
- Add sanitized monitoring evidence.
- Review and correct internal documentation links.
- Complete repository publication review.

---

## Phase 03 — Enterprise Security Monitoring

**Status:** In Progress

### Windows Event Collection

- Configured Windows Event Collector.
- Implemented source-initiated Windows Event Forwarding.
- Configured workstation event forwarding through Group Policy.
- Validated centralized collection of selected Windows Security events.
- Documented the remaining Security log permission automation limitation.

### Wazuh SIEM Integration

- Deployed Ubuntu Server 24.04 LTS for centralized security monitoring.
- Installed Wazuh Manager, Indexer, and Dashboard.
- Installed and enrolled the Wazuh Windows agent on the event collector.
- Configured the agent to ingest the Windows `ForwardedEvents` channel.
- Validated event ingestion into Wazuh.
- Confirmed that events originating from `COMPUTER01` can be identified and investigated through the Wazuh dashboard.

### Pending

- Controlled failed-authentication detection validation.
- Account-lockout event monitoring.
- Privileged group membership monitoring.
- PowerShell activity monitoring.
- Custom detection rules and alert tuning.
- Monitoring retention and operational readiness assessment.

---

## Phase 02 — Enterprise Endpoint Integration

**Status:** Original implementation milestones completed

### Infrastructure

- Created a Windows 11 Enterprise golden image.
- Deployed a domain workstation.
- Established enterprise Group Policy management.
- Expanded enterprise identity organization.

### Endpoint Security

- Implemented workstation configuration baselines.
- Configured Windows Defender security policies.
- Configured Microsoft Defender SmartScreen.
- Implemented endpoint restrictions and hardening settings.

### Engineering Note

Some historical endpoint configurations require revalidation following relocation and recovery of the virtualized environment.

Earlier completion records are retained as implementation history and do not automatically establish that every configuration remains active.

---

## Phase 01 — Enterprise Infrastructure Foundation

**Status:** Original implementation milestones completed

### Infrastructure

- Deployed Windows Server 2022.
- Installed and configured Active Directory Domain Services.
- Configured DNS.
- Established enterprise organizational units.
- Created initial user and administrative identities.
- Established security groups and authorization foundations.
- Documented implementation milestones and VMware recovery checkpoints.

### Engineering Note

Earlier records reference different hostnames and domain settings from the current operational environment.

These records remain part of the engineering history. The current infrastructure inventory is maintained separately to avoid presenting historical configurations as active.

---

## Infrastructure Recovery and Configuration Reconciliation

**Date:** Not recorded

### Context

During relocation of the virtualized environment, some implementation progress was lost and earlier configurations reappeared.

Subsequent infrastructure validation established the current operational baseline used for security monitoring.

### Current Verified Systems

- `ServerM1` — Domain Controller and Windows Event Collector.
- `COMPUTER01` — Domain workstation and event-forwarding source.
- `MENAROL-WAZUH01` — Centralized Wazuh security monitoring server.
- `Menarol.local` — Current Active Directory domain.

### Follow-Up

- Preserve historical documentation.
- Record current operational configurations.
- Identify differences requiring future standardization.
- Avoid unnecessary infrastructure changes solely for documentation consistency.

---

## Changelog Maintenance

Future entries should record:

- The milestone or change being implemented.
- The date, when verified.
- Significant configuration or architectural changes.
- Validation outcomes.
- Known limitations and follow-up actions.
- References to relevant phase documentation.

Changes must not be recorded as completed until they have been implemented and verified.

---

## 2026-10-09 — Security Portfolio Evidence Integration

### Validated PoC Results

- Added the [Phase 03 validation record](02-Implementation-Phases/Phase-03-Enterprise-Security-Monitoring/Validation-2026-10-09.md), four primary screenshots, and two supporting screenshots from the supplied portfolio package.
- Recorded COMPUTER01 → WEF → ServerM1/WEC → Wazuh agent 001 → MENAROL-WAZUH01 with source attribution.
- Recorded two authorised 4625 records triggering built-in Wazuh rule 60122, severity 5; no real attack or brute-force correlation is claimed.
- Recorded minimum password length 7 → 14, verified in Active Directory and local ServerM1 SCA check 27003. Initial baseline: 95 passed / 264 failed, 26%. Pre-hardening reassessment: 98 passed / 261 failed, 27%; three existing-policy checks corrected without configuration changes. Final hardening retest: 99 passed / 260 failed, 27%; one additional check passed after the minimum-length change.
- Recorded local ServerM1 FIM added/modified/deleted events under rules 554/550/553; no workstation SCA/FIM coverage is claimed.
- Recorded WEF delivery timeout 900000 → 30000 milliseconds without claiming a measured end-to-end latency improvement.

### Documentation and Remaining Work

Integrated the README summary once with two featured screenshots, updated current Phase 03 status and roadmap, and appended journal, decision, and lesson records. Earlier milestone entries remain historical; the dated record supersedes their planned failed-logon status. LinkedIn and resume drafts remain outside the repository.

SCA reassessment passed, but post-reboot inconsistency remains unresolved. Temporary account cleanup and GPO backup confirmation remain unverified. Account-lockout testing, custom rules, advanced logging, WEF permission automation, and production readiness remain pending. No infrastructure changes or Git publication actions were performed during this integration.

---

## 2026-10-09 — Verified Test Cleanup Clarification

User-supplied verification confirms `secplus.test` is disabled (`Enabled=False`) and `C:\Menarol-FIM-Test\monitoring-test.txt` is absent (`Test-Path=False`). The empty demonstration folder and its FIM configuration remain intentionally retained.

The earlier integration entry is preserved as history; its pending cleanup status is superseded by this verification and the [updated validation record](02-Implementation-Phases/Phase-03-Enterprise-Security-Monitoring/Validation-2026-10-09.md). GPO backup confirmation remains unverified. SCA inconsistency after reboot, account-lockout testing, custom rules, advanced logging, WEF permission automation, and production readiness remain unresolved or pending. This update records supplied evidence; no running infrastructure was changed.
