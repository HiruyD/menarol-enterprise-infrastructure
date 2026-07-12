# Phase 03 – Enterprise Security Monitoring

## Overview

Phase 03 introduces centralized security monitoring into the Menarol Enterprise Infrastructure.

After establishing a secure and centrally managed Windows endpoint environment during Phase 02, this phase focuses on visibility, auditing, event collection, and security monitoring using native Microsoft technologies.

The objective is to build an enterprise monitoring platform capable of collecting, analyzing, and investigating security events before integrating third-party security platforms.

Every monitoring component will be deployed, validated, documented, version controlled, and protected by VMware snapshots.

---

# Version 1.0 – Windows Event Collector

## Objectives

- Deploy the Windows Event Collector service.
- Configure the Windows Event Collector.
- Validate collector functionality.
- Prepare the environment for Windows Event Forwarding.

## Status

**Completed**

## Completed Work

- Windows Event Collector initialized on `MENAROL-SRV01`.
- Collector service availability confirmed.
- **Forwarded Events** log confirmed in Event Viewer.
- Server prepared for source-initiated event subscriptions.

---

# Version 2.0 – Windows Event Forwarding

## Objectives

- Configure a source-initiated subscription.
- Configure workstation forwarding through Group Policy.
- Configure required WinRM and firewall settings.
- Forward Windows Security and System events.
- Validate centralized event collection.
- Eliminate manual workstation-side configuration where a supported centralized method is validated.

## Status

**Functionally validated with one open standardization item**

## Completed Work

- Source-initiated event subscription created on `MENAROL-SRV01`.
- Workstation Subscription Manager configuration deployed through Group Policy.
- Required WinRM and Windows Firewall settings configured.
- WEF troubleshooting performed across the collector, subscription, network, policy, and permission layers.
- Security log access requirement identified.
- `NT AUTHORITY\NETWORK SERVICE` added to the local **Event Log Readers** group on `MENAROL-WKS01` for functional validation.
- Windows Event Forwarding architecture validated on `MENAROL-WKS01`.

## Open Engineering Improvement

The Security log access prerequisite has not yet been converted into a validated zero-touch enterprise deployment method.

An attempted Restricted Groups configuration was not adopted because the Group Policy object picker could not resolve the local well-known `NETWORK SERVICE` principal through Active Directory.

The manual configuration remains a temporary validated prerequisite, not the final Menarol deployment standard.

## Version 2.0 Completion Criteria

Version 2.0 will be considered fully standardized when:

- The required Security log access is deployed centrally.
- A workstation requires no manual WEF configuration after domain join and Group Policy refresh.
- The configuration is validated on both `MENAROL-WKS01` and `MENAROL-WKS02`.

---

# Planned Versions

## Version 3.0 – Advanced Windows Auditing

- Configure Advanced Audit Policy.
- Audit logon events.
- Audit account management.
- Audit privilege use.
- Audit object access.

---

## Version 4.0 – PowerShell Logging

- Configure Module Logging.
- Configure Script Block Logging.
- Configure PowerShell Transcription.
- Validate PowerShell event logging.

---

## Version 5.0 – Sysmon Deployment

- Deploy Sysmon.
- Configure enterprise Sysmon policy.
- Validate Sysmon event generation.

---

## Version 6.0 – Enterprise Security Monitoring

- Create custom Event Viewer views.
- Analyze authentication activity.
- Analyze endpoint security events.
- Analyze Microsoft Defender events.

---

## Version 7.0 – SIEM Preparation

- Prepare Windows event sources for SIEM ingestion.
- Validate enterprise logging architecture.
- Prepare for future Wazuh deployment.

---

# Current Status

**Current Version**

Version 2.0 – Windows Event Forwarding

The centralized Windows event collection architecture is operational and functionally validated on `MENAROL-WKS01`. Centralized automation of the Security log permission prerequisite remains an open engineering improvement.

---

# Next Milestone

- Research and test a supported zero-touch method for deploying the Security log access requirement.
- Validate the final method on `MENAROL-WKS02`.
- Continue to Version 3.0 only after recording the open improvement in the project backlog.
