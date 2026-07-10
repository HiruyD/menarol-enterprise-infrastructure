# Menarol Enterprise Infrastructure

> Building an enterprise IT environment from the ground up.

---

# Overview

This repository documents the design, implementation, validation, and continuous improvement of the Menarol Enterprise infrastructure.

Menarol is a diversified organization headquartered in Addis Ababa, Ethiopia, consisting of multiple business units including healthcare, fitness, wellness, administrative services, and future technology initiatives.

The objective of this project is to design and implement an enterprise-grade infrastructure using industry best practices in:

- Systems Administration
- Enterprise Networking
- Identity and Access Management (IAM)
- Cybersecurity
- Windows Server Administration
- Cloud Computing
- Infrastructure Automation

Every milestone is documented, validated, version controlled, and recoverable through VMware snapshots and Git.

---

# Vision

Design and maintain a secure, scalable, resilient, and well-documented enterprise infrastructure that mirrors real-world IT environments.

Each milestone is fully validated before progressing to the next phase.

---

# Current Environment

## Virtualization

- VMware Workstation 17 Pro

## Operating Systems

- Windows Server 2022 Standard Evaluation
- Windows 11 Enterprise Evaluation

## Core Technologies Implemented

- Active Directory Domain Services
- DNS
- Enterprise Organizational Units
- Enterprise Identity Management
- Global Security Groups
- Windows 11 Enterprise Golden Image

---

# Enterprise Group Policy Architecture

Menarol Enterprise follows a layered Group Policy design that separates policies by administrative scope and system role. This minimizes unintended policy inheritance, simplifies troubleshooting, and follows enterprise Active Directory design principles.

| Group Policy Object               | Scope                 | Purpose                                                                                                                                                                                               |
| --------------------------------- | --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Default Domain Policy             | Domain                | Domain-wide security settings that must apply to all domain members. Used only for core domain policies.                                                                                              |
| Default Domain Controllers Policy | Domain Controllers OU | Security configuration specific to Domain Controllers.                                                                                                                                                |
| GPO - Domain Security             | Domain                | Enterprise-wide security policies including password policy, account lockout policy, Kerberos policy, and other domain authentication settings.                                                       |
| GPO - Server Baseline             | Servers OU            | Security hardening and configuration standards for Windows Server systems.                                                                                                                            |
| GPO - Workstation Baseline        | Workstations OU       | Enterprise workstation configuration including endpoint hardening, Windows Defender, Windows Firewall, Windows Update, removable media controls, power management, and workstation security settings. |
| GPO - User Baseline               | User Accounts OU      | User environment configuration, desktop restrictions, Control Panel restrictions, and user experience policies.                                                                                       |

## Group Policy Design Principles

The Menarol Enterprise infrastructure follows these engineering principles:

- Domain-wide authentication policies remain separate from endpoint configuration.
- Server and workstation policies are managed independently.
- User configuration is separated from computer configuration whenever possible.
- Each Group Policy Object has a single administrative purpose.
- New security controls are added only after validation and documented testing.
- Every Group Policy modification is validated using Group Policy Results (`gpresult`) before being committed to the repository.

This layered architecture improves scalability, simplifies troubleshooting, and mirrors enterprise Active Directory administration practices.

---

# Planned Technologies

As the infrastructure evolves, the following technologies will be implemented:

- VMware Tools
- Group Policy
- DHCP
- File Services
- Active Directory Certificate Services (PKI)
- Windows Server Update Services (WSUS)
- PowerShell Automation
- Microsoft Entra ID
- Microsoft Intune
- Microsoft Defender
- Azure
- AWS
- Terraform
- Docker
- Kubernetes
- Wazuh SIEM

---

# Current Progress

## Phase 01 — Enterprise Infrastructure Foundation

### Version 1.0 – Windows Server Baseline

- ✅ Windows Server 2022 installed
- ✅ VMware Tools installed
- ✅ Server renamed to **MENAROL-SRV01**
- ✅ System configured
- ✅ Baseline snapshot created

---

### Version 2.0 – Enterprise Active Directory Foundation

- ✅ Static IPv4 configured
- ✅ Active Directory Domain Services installed
- ✅ DNS Server installed
- ✅ New forest created (**menarol.com**)
- ✅ MENAROL-SRV01 promoted to the first Domain Controller
- ✅ DNS forwarders configured
- ✅ Domain Controller validated using `dcdiag`
- ✅ Version 2.0 snapshot created

---

### Version 3.0 – Enterprise Active Directory Structure

- ✅ Enterprise Organizational Unit hierarchy designed
- ✅ Departmental Organizational Units created
- ✅ Computer Account Organizational Units created
- ✅ Group Organizational Units created
- ✅ Enterprise Active Directory structure established

---

### Version 4.0 – Enterprise Identity Foundation

- ✅ Enterprise user naming standard established
- ✅ Standard user account created
- ✅ Administrative user account created
- ✅ Administrative Organizational Unit structure implemented

---

### Version 5.0 – Enterprise Authorization Foundation

- ✅ Global Security Groups created
- ✅ Enterprise security group naming convention established
- ✅ Initial user-to-group assignments completed
- ✅ Enterprise authorization foundation implemented

---

## Phase 02 — Enterprise Endpoint Integration

### Version 1.0 – Windows 11 Golden Image

- ✅ WIN11-GOLDEN virtual machine created
- ✅ Windows 11 Enterprise Evaluation installed
- ✅ Enterprise workstation hardware baseline established
- ✅ Virtual TPM configured
- ✅ Local break-glass administrator account (**menarol.admin**) created
- ✅ Operating system installation validated
- ✅ Version 1.0 snapshot created

---

### Version 2.0 – Enterprise Domain Workstation

- ✅ Golden Workstation cloned to create the production workstation
- ✅ Production workstation renamed **MENAROL-WKS01**
- ✅ DNS configured to use the Active Directory Domain Controller
- ✅ Successfully joined **MENAROL-WKS01** to the **menarol.com** domain
- ✅ Domain authentication validated using the enterprise Engineer account
- ✅ Computer object automatically created in Active Directory
- ✅ Workstation moved to **Computer Accounts → Workstations**
- ✅ Version 2.0 snapshot created

---

### Version 3.0 – Enterprise Group Policy Foundation

- ✅ Enterprise Group Policy management introduced
- ✅ Group Policy Management Console validated
- ✅ Enterprise Group Policy framework established
- ✅ GPO - Domain Security created
- ✅ GPO - Server Baseline created
- ✅ GPO - User Baseline created
- ✅ GPO - Workstation Baseline created
- ✅ User Baseline linked to the User Accounts Organizational Unit
- ✅ "Prohibit access to Control Panel and PC Settings" policy configured
- ✅ Group Policy successfully applied to MENAROL-WKS01
- ✅ User policy validation completed
- ✅ VMware snapshots created for MENAROL-SRV01 and MENAROL-WKS01

---

### Version 4.0 – Enterprise Identity Expansion

- ✅ Enterprise identity model expanded
- ✅ Departmental user accounts created
- ✅ User accounts organized into appropriate Organizational Units
- ✅ User attributes populated for company, office, department, and job title
- ✅ Users assigned to appropriate Global Security Groups
- ✅ Enterprise identity structure prepared for department-specific Group Policy
- ✅ VMware snapshot created for the updated stable state

### Version 5.0 – Enterprise Workstation Baseline

- ✅ GPO - Workstation Baseline linked to the Workstations Organizational Unit
- ✅ Computer Configuration Group Policy validated
- ✅ AutoPlay disabled for all drives
- ✅ AutoRun disabled
- ✅ Interactive logon inactivity timeout configured
- ✅ Last signed-in user hidden at logon
- ✅ Windows Defender Firewall baseline validated
- ✅ Enterprise Group Policy architecture documented

# Repository Structure

| Folder                 | Purpose                                               |
| ---------------------- | ----------------------------------------------------- |
| 00-Documentation       | Project documentation and engineering standards       |
| 01-Infrastructure      | Infrastructure configuration and server documentation |
| 02-Homelabs            | Individual enterprise implementation phases           |
| 03-Scripts             | PowerShell, Terraform, Bash, and automation           |
| 04-Network-Diagrams    | Network topology and architecture                     |
| 05-GitHub-Portfolio    | Portfolio-ready project summaries                     |
| 06-Certification-Notes | Certification study notes and references              |

---

# Documentation Standards

Every completed milestone includes:

- Objectives
- Engineering Decisions
- Configuration Documentation
- Validation Results
- VMware Snapshot
- Lessons Learned
- Git Commit History
- Future Improvements

---

# Engineering Methodology

Every infrastructure milestone follows the same workflow:

1. Design
2. Implement
3. Validate
4. Snapshot
5. Document
6. Commit
7. Push

This methodology ensures every version of the environment is reproducible, documented, and recoverable.

---

Current Version

---

Current Version

Version 5.0 – Enterprise Workstation Baseline

**Next Milestone**

Version 6.0 – Enterprise Endpoint Hardening

Objectives:

- Expand Microsoft Defender enterprise policies
- Expand Windows Defender Firewall configuration
- Configure Windows Update policies
- Configure enterprise power management
- Continue workstation security hardening
- Validate Computer Configuration deployment

# Long-Term Objectives

The completed infrastructure will include:

- Enterprise Active Directory
- Identity and Access Management (IAM)
- Windows Server Administration
- Enterprise Networking
- Group Policy Management
- File Services
- Enterprise Windows Workstation Management
- Public Key Infrastructure (PKI)
- Windows Server Update Services (WSUS)
- Microsoft Entra ID Hybrid Identity
- Microsoft Intune
- Microsoft Defender
- Infrastructure as Code (Terraform)
- Cloud Integration (Azure & AWS)
- Security Monitoring (Wazuh SIEM)
- Enterprise Automation with PowerShell

---

# Project Philosophy

This repository represents the continuous engineering and operational development of the Menarol Enterprise infrastructure.

Every configuration change is documented.

Every milestone is validated.

Every implementation is version controlled.

Every engineering decision is recorded.
