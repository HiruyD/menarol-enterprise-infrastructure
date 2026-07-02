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

## Version 3.0 – Enterprise Active Directory Structure

### Objectives

- Design the enterprise Organizational Unit hierarchy.
- Create departmental Organizational Units.
- Create Computer Account Organizational Units.
- Create Group Organizational Units.
- Implement enterprise Active Directory standards.
- Validate the enterprise directory structure.
- Create the Version 3.0 snapshot.

---

## Version 4.0 – Enterprise Identity Foundation

### Objectives

- Establish enterprise user naming standards.
- Create standard user accounts.
- Create administrative user accounts.
- Organize identities within the enterprise Organizational Unit structure.
- Validate enterprise identities.
- Create the Version 4.0 snapshot.

---

## Version 5.0 – Enterprise Authorization Foundation

### Objectives

- Design the enterprise authorization model.
- Create Global Security Groups.
- Implement enterprise security group naming standards.
- Assign initial users to Global Security Groups.
- Validate enterprise authorization.
- Create the Version 5.0 snapshot.

---

## Current Status

### Completed

- Windows Server 2022 deployed.
- Active Directory Domain Services installed.
- DNS Server configured.
- Enterprise Organizational Unit hierarchy implemented.
- Enterprise user identities created.
- Enterprise Global Security Groups implemented.

---

## Next Phase

Phase 02 will begin Enterprise Endpoint Integration.

The first Windows 11 Enterprise workstation will be deployed, joined to the **menarol.com** domain, validated, and prepared for centralized Group Policy management.
