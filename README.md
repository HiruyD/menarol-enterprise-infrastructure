# Menarol Enterprise Infrastructure

> Building an enterprise IT environment from the ground up.

---

## Overview

This repository documents the design, implementation, and continuous improvement of the Menarol Enterprise infrastructure.

Menarol is an organization headquartered in Addis Ababa, Ethiopia, with multiple business units including healthcare, fitness, wellness, administrative services, and future technology initiatives.

This repository serves as the central engineering documentation for building a secure, scalable, and modern enterprise environment while applying industry best practices in systems administration, networking, cybersecurity, cloud computing, and Identity and Access Management (IAM).

---

## Vision

Design and maintain an enterprise-grade infrastructure that is secure, scalable, resilient, and well documented. Every phase of the project is version controlled and validated before moving to the next milestone.

---

## Current Environment

### Virtualization

- VMware Workstation

### Operating Systems

- Windows Server 2022
- Windows 11 Enterprise

### Technologies

- Active Directory Domain Services
- DNS
- DHCP
- Group Policy
- PowerShell
- Microsoft Entra ID
- Microsoft Intune
- Microsoft Defender
- Azure
- AWS
- Terraform
- Docker
- Kubernetes
- Wazuh SIEM
- Git & GitHub

---

## Current Progress

### Phase 1 — Enterprise Foundation

**Version 1.0 – Windows Server Baseline**

- ✅ Windows Server 2022 installed
- ✅ VMware Tools installed
- ✅ Server renamed to **MENAROL-SRV01**
- ✅ Time zone configured
- ✅ Version 1.0 snapshot created

**Version 2.0 – Enterprise Active Directory Foundation**

- ✅ Static IPv4 configured
- ✅ Active Directory Domain Services installed
- ✅ DNS Server installed
- ✅ New forest created: **menarol.com**
- ✅ MENAROL-SRV01 promoted to the first Domain Controller
- ✅ DNS forwarders configured
- ✅ Domain Controller health validated using `dcdiag`
- ✅ Version 2.0 snapshot created

---

## Repository Structure

| Folder                 | Purpose                                               |
| ---------------------- | ----------------------------------------------------- |
| 00-Documentation       | Project documentation and implementation guides       |
| 01-Infrastructure      | Infrastructure configuration and server documentation |
| 02-Homelabs            | Individual lab projects and exercises                 |
| 03-Scripts             | PowerShell, Terraform, Bash, and automation scripts   |
| 04-Network-Diagrams    | Network topology and architecture diagrams            |
| 05-GitHub-Portfolio    | Portfolio-ready project summaries                     |
| 06-Certification-Notes | Study notes and certification references              |

---

## Documentation Standards

Each completed phase includes:

- Objectives
- Architecture decisions
- Configuration steps
- Validation
- Screenshots
- Lessons learned
- Rollback strategy
- Future improvements

---

## Status

**Current Version:** 2.0

**Current Phase:** Enterprise Active Directory Foundation

**Next Milestone:** Design and implement the Active Directory organizational structure, including Organizational Units (OUs), security groups, and administrative standards.
