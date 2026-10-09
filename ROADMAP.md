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

**Status: Controlled failed-logon test validated; account-lockout testing pending**

- Two authorised 4625 records reached Wazuh through COMPUTER01 → WEF → ServerM1/WEC → agent 001 → MENAROL-WAZUH01.
- Built-in rule 60122 triggered at severity 5; brute-force correlation was not validated.
- WEF delivery timeout changed from 900000 to 30000 milliseconds; precise end-to-end latency improvement was not measured.
- [Validation record and evidence](02-Implementation-Phases/Phase-03-Enterprise-Security-Monitoring/Validation-2026-10-09.md) document results and limits.
- Account-lockout Event ID 4740 remains untested; no lockout policy change was made.

### Local ServerM1 Hardening and Integrity Validation — 2026-10-09

**Status: Focused tests validated; SCA reliability and GPO backup confirmation pending**

- Domain minimum password length changed from 7 to 14, verified in Active Directory and local SCA check 27003.
- Initial SCA baseline: 95 passed / 264 failed, 26%. Pre-hardening reassessment: 98 passed / 261 failed, 27%. Final hardening retest: 99 passed / 260 failed, 27%; one additional check passed after minimum password length changed from 7 to 14.
- Three existing-policy checks corrected on the pre-hardening reassessment without configuration changes, not additional remediation.
- Post-reboot assessment inconsistencies remain unresolved despite a passing reassessment.
- Local ServerM1 FIM verified added/modified/deleted events under rules 554/550/553.
- Cleanup verified: `secplus.test` disabled (`Enabled=False`); `C:\Menarol-FIM-Test\monitoring-test.txt` absent (`Test-Path=False`). The empty demonstration folder and its FIM configuration remain intentionally retained.
- GPO backup confirmation remains pending.
- These local assessments do not establish SCA or FIM coverage on COMPUTER01.

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
2. Review the integrated 9 October 2026 validation record and screenshots.
3. Confirm the GPO backup outcome.
4. Investigate post-reboot SCA inconsistency and evaluate account-lockout testing separately.
5. Continue security monitoring and detection engineering milestones.

---

_This roadmap is a living engineering document and will be updated as requirements, implementation results, and business decisions evolve._
