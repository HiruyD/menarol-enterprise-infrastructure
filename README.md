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
- Enterprise Group Policy Management
- Microsoft Defender Enterprise Configuration
- Microsoft Defender SmartScreen

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
- DHCP
- File Services
- Active Directory Certificate Services (PKI)
- Windows Server Update Services (WSUS)
- PowerShell Automation
- Microsoft Entra ID
- Microsoft Intune
- Azure
- AWS
- Terraform
- Docker
- Kubernetes
- Wazuh SIEM

---

# Current Progress

---

## Phase 01 — Enterprise Infrastructure Foundation

### Status

✅ Completed

### Versions

- Version 1.0 – Windows Server Baseline
- Version 2.0 – Enterprise Active Directory Foundation
- Version 3.0 – Enterprise Active Directory Structure
- Version 4.0 – Enterprise Identity Foundation
- Version 5.0 – Enterprise Authorization Foundation

---

## Phase 02 — Enterprise Endpoint Integration

### Status

✅ Completed

### Versions

- Version 1.0 – Windows 11 Golden Image
- Version 2.0 – Enterprise Domain Workstation
- Version 3.0 – Enterprise Group Policy Foundation
- Version 4.0 – Enterprise Identity Expansion
- Version 5.0 – Enterprise Workstation Baseline
- Version 6.0 – Enterprise Endpoint Hardening

**Key Deliverables**

- Windows 11 Enterprise Golden Image
- Production workstation deployment
- Active Directory integration
- Enterprise identity management
- Layered Group Policy architecture
- Enterprise workstation baseline
- Microsoft Defender enterprise management
- Microsoft Defender SmartScreen
- Enterprise endpoint hardening

---

## Phase 03 — Enterprise Security Monitoring

### Status

🚧 In Progress

### Current Version

Version 2.0 – Windows Event Forwarding

**Objectives**

- - Windows Event Collector deployed and validated.
- Source-initiated Windows Event Forwarding configured.
- Group Policy-based forwarding infrastructure implemented.
- Functional validation completed on MENAROL-WKS01.
- Centralized automation of Security log permissions remains an open engineering improvement.

---

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

# Current Status

**Current Phase**

Phase 03 – Enterprise Security Monitoring

**Current Version**

Version 2.0 – Windows Event Forwarding

**Next Milestone**

Complete zero-touch deployment of the Security log permission prerequisite.

Objectives:

- Research and validate a supported centralized deployment method.
- Validate automated deployment on MENAROL-WKS01 and MENAROL-WKS02.
- Eliminate the remaining manual WEF configuration step.
- Begin Phase 03 Version 3.0 – Advanced Windows Auditing.

---

# Long-Term Objectives

The completed infrastructure will include:

- Enterprise Active Directory
- Identity and Access Management (IAM)
- Windows Server Administration
- Enterprise Networking
- Group Policy Management
- Enterprise Windows Workstation Management
- Enterprise Security Monitoring
- Public Key Infrastructure (PKI)
- Windows Server Update Services (WSUS)
- Microsoft Entra ID Hybrid Identity
- Microsoft Intune
- Microsoft Defender
- Infrastructure as Code (Terraform)
- Cloud Integration (Azure & AWS)
- Wazuh SIEM
- Enterprise Automation with PowerShell

---

# Project Philosophy

This repository represents the continuous engineering and operational development of the Menarol Enterprise infrastructure.

Every configuration change is documented.

Every milestone is validated.

Every implementation is version controlled.

Every engineering decision is recorded.
