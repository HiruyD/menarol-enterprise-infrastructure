# Phase 01 – Enterprise Infrastructure Foundation

## Overview

Phase 01 establishes the core infrastructure for the Menarol Enterprise Lab. The objective of this phase is to build a stable Windows Server 2022 environment that serves as the foundation for all future enterprise services.

This phase concludes with the deployment of the first Active Directory Domain Controller and the creation of the Menarol Active Directory forest.

---

## Objectives

### Version 1.0 – Windows Server Baseline

- Install Windows Server 2022
- Install VMware Tools
- Configure the operating system
- Rename the server to **MENAROL-SRV01**
- Configure the system time zone
- Create the Version 1.0 baseline snapshot

### Version 2.0 – Enterprise Active Directory Foundation

- Configure a static IPv4 address
- Install Active Directory Domain Services (AD DS)
- Install the DNS Server role
- Promote the server to the first Domain Controller
- Create the **menarol.com** forest
- Configure DNS forwarders
- Validate the deployment using `dcdiag`
- Create the Version 2.0 snapshot

---

## Environment

| Component        | Value                                   |
| ---------------- | --------------------------------------- |
| Hypervisor       | VMware Workstation 17 Pro               |
| Operating System | Windows Server 2022 Standard Evaluation |
| Server Name      | MENAROL-SRV01                           |
| Forest           | menarol.com                             |
| Domain           | menarol.com                             |
| NetBIOS          | MENAROL                                 |

---

## Deliverables

### Version 1.0

- Windows Server 2022 baseline
- VMware Tools installed
- Initial server configuration completed

### Version 2.0

- Active Directory Domain Services deployed
- DNS Server deployed
- First Domain Controller operational
- Forest created
- Domain health verified

---

## Validation

The deployment was validated using:

- `hostname`
- `whoami`
- `ipconfig /all`
- `nslookup`
- `dcdiag`

---

## Next Phase

Phase 02 will focus on designing the enterprise Active Directory structure, including Organizational Units (OUs), security groups, administrative standards, and identity management.
