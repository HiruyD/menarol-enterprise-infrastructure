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

Phase 02 — Enterprise Endpoint Integration

**Current Version**

Version 1.0 – Windows 11 Golden Image

**Next Milestone**

Version 2.0 – Enterprise Workstation Baseline

Objectives:

- Install VMware Tools
- Configure Windows Update
- Verify regional settings and time zone
- Apply enterprise workstation baseline configuration
- Prepare the Golden Image for cloning

---

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
