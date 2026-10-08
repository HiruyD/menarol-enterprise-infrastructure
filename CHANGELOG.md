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
