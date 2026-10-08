# Phase 02 – Enterprise Endpoint Integration

## Overview

Phase 02 introduces enterprise Windows client systems into the Menarol Enterprise Infrastructure.

Rather than immediately deploying production workstations, this phase begins with the creation of a standardized Windows 11 Enterprise Golden Image. The Golden Image serves as the deployment source for all future enterprise endpoints, ensuring consistency, repeatability, and simplified lifecycle management.

As the phase progresses, cloned workstations are integrated into Active Directory, managed through enterprise Group Policy, and secured using centralized endpoint configuration that mirrors real-world enterprise administration.

---

# Version 1.0 – Windows 11 Golden Image

## Completed

- WIN11-GOLDEN created.
- Windows 11 Enterprise installed.
- Virtual TPM configured.
- Enterprise hardware baseline established.
- Local break-glass administrator created.
- Version 1.0 snapshot created.

---

# Version 2.0 – Enterprise Domain Workstation

## Completed

- MENAROL-WKS01 deployed from the Golden Image.
- Joined to the menarol.com domain.
- DNS configuration validated.
- Domain authentication verified.
- Computer object moved into the Workstations Organizational Unit.
- Version 2.0 snapshot created.

---

# Version 3.0 – Enterprise Group Policy Foundation

## Completed

- Enterprise Group Policy architecture created.
- User Baseline GPO deployed.
- Initial User Configuration policies implemented.
- Group Policy validation completed.
- Version 3.0 snapshots created.

---

# Version 4.0 – Enterprise Identity Expansion

## Completed

- Enterprise departmental users created.
- Organizational Unit structure populated.
- Global Security Groups assigned.
- Enterprise identity model expanded.
- Version 4.0 snapshot created.

---

# Version 5.0 – Enterprise Workstation Baseline

## Completed

- Workstation Baseline GPO linked.
- AutoPlay protection configured.
- AutoRun protection configured.
- Interactive logon security configured.
- Windows Defender Firewall baseline validated.
- Enterprise workstation baseline established.
- Version 5.0 snapshots created.

---

# Version 6.0 – Enterprise Endpoint Hardening

## Completed

- Microsoft Defender Antivirus enterprise baseline implemented.
- Real-time protection enforced.
- Behavior monitoring enabled.
- Process scanning enabled.
- Script scanning enabled.
- Download and attachment scanning enabled.
- Raw volume write notifications enabled.
- Windows Defender SmartScreen configured for Explorer.
- Microsoft Edge SmartScreen configured.
- App Install Control configured.
- Group Policy validation completed.
- Microsoft Defender operational status validated using PowerShell.
- Version 6.0 snapshots created.

---

# Current Status

**Current Version**

**Version 6.0 – Enterprise Endpoint Hardening**

The Menarol workstation environment now includes:

- Standardized Windows 11 deployment
- Active Directory integration
- Enterprise identity management
- Enterprise Group Policy architecture
- Enterprise workstation security baseline
- Microsoft Defender enterprise protection
- Microsoft Defender SmartScreen
- Enterprise endpoint hardening

---

# Next Milestone

## Version 7.0 – Windows Event Forwarding (WEF)

### Objectives

- Deploy a Windows Event Collector.
- Configure Windows Event Forwarding.
- Forward Security event logs.
- Forward System event logs.
- Validate event subscriptions.
- Prepare the infrastructure for Sysmon and enterprise security monitoring.
