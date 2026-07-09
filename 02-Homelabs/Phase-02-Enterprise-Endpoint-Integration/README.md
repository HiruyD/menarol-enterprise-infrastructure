# Phase 02 – Enterprise Endpoint Integration

## Overview

Phase 02 introduces enterprise Windows client systems into the Menarol Enterprise Infrastructure.

Rather than immediately deploying a production workstation, this phase begins by creating a reusable Windows 11 Enterprise Golden Image. The Golden Image serves as the standardized baseline for all future Windows workstation deployments.

Using a Golden Image ensures consistency, repeatability, and simplified lifecycle management while following enterprise deployment best practices.

---

# Objectives

## Version 1.0 – Windows 11 Golden Image

- Create the WIN11-GOLDEN virtual machine.
- Configure enterprise virtual hardware standards.
- Install Windows 11 Enterprise Evaluation.
- Configure virtual TPM support.
- Create the local break-glass administrator account.
- Validate successful operating system installation.
- Create the Version 1.0 VMware snapshot.

---

# Completed

- WIN11-GOLDEN virtual machine created.
- Windows 11 Enterprise Evaluation installed.
- Enterprise hardware baseline established.
- Virtual TPM configured.
- Local break-glass administrator account created.
- Operating system installation validated.
- Version 1.0 VMware snapshot created.

---

# Current Status

Current Version

Version 2.0 – Enterprise Domain Workstation

---

# Next Milestone

## Version 3.0 – Enterprise Group Policy Foundation

Objectives

- Design the enterprise Group Policy strategy.
- Create baseline Group Policy Objects (GPOs).
- Link GPOs to the appropriate Organizational Units.
- Validate Group Policy application on MENAROL-WKS01.
- Document the enterprise Group Policy baseline.

---

# Version 2.0 – Enterprise Domain Workstation

## Objectives

- Clone the Windows 11 Golden Image.
- Deploy the production workstation.
- Configure Active Directory DNS.
- Join the workstation to the menarol.com domain.
- Validate domain authentication.
- Move the workstation into the Workstations Organizational Unit.
- Create the Version 2.0 VMware snapshot.

---

## Completed

- Created the production workstation by cloning the Golden Image.
- Verified workstation hostname (MENAROL-WKS01).
- Corrected DNS configuration to use the Domain Controller.
- Successfully joined MENAROL-WKS01 to the menarol.com Active Directory domain.
- Verified domain authentication using the Engineer account.
- Confirmed automatic computer object creation in Active Directory.
- Moved MENAROL-WKS01 into the Computer Accounts → Workstations Organizational Unit.
- Created the Version 2.0 VMware snapshot.

---

# Version 3.0 – Enterprise Group Policy Foundation

## Objectives

- Introduce enterprise Group Policy management.
- Create an enterprise Group Policy framework.
- Separate User and Computer policy design.
- Configure the first enterprise User Configuration policy.
- Validate Group Policy deployment on MENAROL-WKS01.
- Create Version 3.0 VMware snapshots.

---

## Completed

- Opened and validated Group Policy Management.
- Reviewed Microsoft default Group Policy Objects.
- Created GPO - Domain Security.
- Created GPO - Server Baseline.
- Created GPO - User Baseline.
- Created GPO - Workstation Baseline.
- Linked GPO - User Baseline to the User Accounts Organizational Unit.
- Configured "Prohibit access to Control Panel and PC Settings".
- Successfully applied the GPO - User Baseline Group Policy.
- Validated Group Policy deployment on MENAROL-WKS01.
- Created Version 3.0 VMware snapshots.

---

# Current Status

Current Version

Version 3.0 – Enterprise Group Policy Foundation

---

# Next Milestone

## Version 4.0 – Enterprise Workstation Baseline

Objectives

- Configure Computer Configuration Group Policies.
- Configure Microsoft Defender baseline.
- Configure Windows Defender Firewall.
- Configure Windows Update settings.
- Configure enterprise power management.
- Validate Computer Configuration policy processing.
- Document the enterprise workstation baseline.
