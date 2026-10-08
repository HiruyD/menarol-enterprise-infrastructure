# Menarol Enterprise Infrastructure — Project Roadmap

**Project Classification:** Enterprise IT Infrastructure — Pre-Production Proof of Concept
**Current Phase:** Phase 03 — Enterprise Security Monitoring
**Production Deployment:** Pending business approval and cost assessment

---

## Purpose

This roadmap tracks the phased implementation and validation of Menarol's enterprise IT infrastructure.

The infrastructure is being developed in a virtualized environment to validate business requirements, technical configurations, security controls, and system integrations before production deployment.

The roadmap distinguishes between completed work, active engineering activities, future enhancements, and production-readiness requirements.

Milestone completion is determined by documented validation rather than a predetermined deadline.

---

## Phase 01 — Enterprise Infrastructure Foundation

**Status: Completed in the original implementation**

### Scope

- Windows Server 2022 deployment.
- Active Directory Domain Services and DNS.
- Enterprise organizational unit structure.
- User and administrative identities.
- Security groups and authorization foundations.
- VMware recovery checkpoints.

### Engineering Note

Some original configuration details changed following the relocation and recovery of the virtualized environment.

The current operational infrastructure must be distinguished from historical implementation records.

[Phase 01 Documentation](02-Implementation-Phases/Phase-01-Enterprise-Infrastructure-Foundation/README.md)

---

## Phase 02 — Enterprise Endpoint Integration

**Status: Completed in the original implementation; current configuration subject to verification**

### Scope

- Windows 11 Enterprise golden image.
- Domain-joined workstation deployment.
- Enterprise Group Policy structure.
- Workstation configuration and security baseline.
- Microsoft Defender and SmartScreen policies.
- User and computer policy management.

### Outstanding Validation

Confirm which original endpoint-hardening configurations remain active following VM recovery before representing them as currently enforced.

[Phase 02 Documentation](02-Implementation-Phases/Phase-02-Enterprise-Endpoint-Integration/README.md)

---

## Phase 03 — Enterprise Security Monitoring

**Status: In Progress**

### Milestone 3.1 — Windows Event Collection

**Status: Validated**

- Windows Event Collector configured on `ServerM1`.
- Source-initiated Windows Event Forwarding implemented.
- Group Policy used to configure workstation forwarding.
- Selected Security events forwarded from `COMPUTER01`.
- Centralized event collection verified.

**Open improvement:** Standardize the remaining manual Security log permission prerequisite.

### Milestone 3.2 — Wazuh SIEM Integration

**Status: Validated in the PoC**

- Ubuntu Server deployed for Wazuh.
- Wazuh Manager, Indexer, and Dashboard installed.
- Windows agent enrolled on `ServerM1`.
- Agent configured to ingest `ForwardedEvents`.
- Events originating from `COMPUTER01` identified in Wazuh.
- Original event source and collection agent attribution verified.

### Milestone 3.3 — Authentication Monitoring

**Status: Next Technical Milestone**

- Generate controlled failed Windows authentication attempts.
- Identify and investigate Security Event ID 4625.
- Verify event collection through Windows Event Forwarding.
- Verify event ingestion and visibility in Wazuh.
- Evaluate alert behavior and detection coverage.
- Document test procedure, evidence, findings, and limitations.
- Extend testing to account lockout Event ID 4740 where appropriate.

### Milestone 3.4 — Privileged Access Monitoring

**Status: Planned**

- Identify security-relevant Active Directory group membership events.
- Generate authorized, controlled group membership changes.
- Verify event generation and collection.
- Evaluate Wazuh visibility and alert behavior.
- Document investigation procedures and findings.

### Milestone 3.5 — PowerShell and Endpoint Visibility

**Status: Planned**

- Evaluate Advanced Audit Policy requirements.
- Configure and validate PowerShell Script Block Logging.
- Evaluate PowerShell Module Logging and transcription requirements.
- Assess Sysmon deployment and configuration.
- Confirm collection and monitoring coverage.

### Milestone 3.6 — Detection Engineering

**Status: Planned**

- Develop custom Wazuh detection rules.
- Validate rules against controlled test events.
- Investigate false positives and detection limitations.
- Document rule logic and expected behavior.
- Establish repeatable detection test cases.

### Milestone 3.7 — Monitoring Operations

**Status: Planned**

- Review log retention and storage requirements.
- Document Wazuh maintenance and backup considerations.
- Establish initial investigation procedures.
- Define monitoring responsibilities and escalation requirements.
- Assess monitoring coverage against business risks.

[Phase 03 Documentation](02-Implementation-Phases/Phase-03-Enterprise-Security-Monitoring/README.md)

---

## Production Readiness and Deployment Planning

**Status: Pending**

Menarol has not selected a final production hosting or migration approach.

The preferred solution will be determined through a cost and feasibility assessment, subject to the organization's operational, security, and reliability requirements.

### Evaluation Areas

| Area       | Required Assessment                                               |
| ---------- | ----------------------------------------------------------------- |
| Hosting    | Physical, virtualized, or hybrid infrastructure                   |
| Migration  | Existing VM migration versus clean deployment                     |
| Licensing  | Windows Server, endpoints, and supporting software                |
| Networking | Business segmentation, addressing, DNS, and connectivity          |
| Identity   | Domain architecture, administrative access, and account lifecycle |
| Security   | Endpoint protection, auditing, monitoring, and access controls    |
| Resilience | Backup, recovery, restoration testing, and continuity             |
| Operations | Maintenance, patching, documentation, and support                 |
| Cost       | Initial investment and ongoing operating expenses                 |

### Deployment Decision

**Pending business review.**

No production architecture, hosting provider, migration approach, or implementation date has been approved in this roadmap.

---

## Engineering and Documentation Improvements

These improvements will be addressed alongside technical milestones:

- Align documentation with the current operational infrastructure.
- Preserve historical configurations and recovery context.
- Standardize repository navigation and file naming.
- Maintain engineering decisions and implementation journals.
- Capture sanitized screenshots and architecture diagrams.
- Track unresolved technical issues and implementation risks.
- Maintain a project changelog.
- Document acceptance criteria for future milestones.

---

## Completion Criteria

A technical milestone is considered complete when:

1. The implementation scope and expected behavior are documented.
2. Required configurations have been applied.
3. Functional validation has been performed.
4. Supporting evidence has been reviewed.
5. Engineering decisions and limitations have been recorded.
6. Recovery requirements have been considered.
7. The corresponding documentation has been reviewed and version controlled.

**PoC milestone completion does not constitute production approval.**

---

## Immediate Next Actions

1. Complete repository publication cleanup.
2. Capture and review WEF and Wazuh validation evidence.
3. Complete the controlled failed-authentication monitoring exercise.
4. Document the results in Phase 03.
5. Continue security monitoring and detection engineering milestones.

---

_This roadmap is a living engineering document and will be updated as requirements, implementation results, and business decisions evolve._
