# Menarol Enterprise Infrastructure

**Enterprise IT Infrastructure | Pre-Production Proof of Concept**

Designing, implementing, and validating a centrally managed enterprise infrastructure to support Menarol's business operations and future production deployment.

---

## Project Overview

Menarol is a business organization based in Addis Ababa, Ethiopia, with operations spanning healthcare, fitness, wellness, and shared administrative services.

The organization requires an IT infrastructure capable of supporting multiple business units while maintaining centralized identity management, consistent security policies, controlled access, and operational visibility.

This repository documents the design, implementation, testing, troubleshooting, and ongoing development of that infrastructure.

The initial implementation is hosted in a VMware virtualized environment as a **pre-production proof of concept (PoC)**. This allows configurations, integrations, and security controls to be validated before the organization commits to production infrastructure.

The objective is to establish a documented, technically validated foundation that can support an eventual production deployment.

## Business and Technical Objectives

- Establish centralized authentication and identity management.
- Organize users, computers, and security groups according to business requirements.
- Implement role-based access management and administrative separation.
- Standardize workstation configuration through Group Policy.
- Apply and validate Windows endpoint security controls.
- Centralize Windows security event collection.
- Introduce security monitoring and investigation capabilities.
- Maintain engineering documentation, validation evidence, and recovery checkpoints.
- Evaluate production deployment options based on cost, security, operational requirements, and maintainability.

---

## Current Implementation Status

**Project stage:** Pre-Production Proof of Concept

**Active implementation phase:** Phase 03 — Enterprise Security Monitoring

**Current milestone:** Wazuh SIEM integration and end-to-end Windows security event validation

**Production deployment:** Not yet implemented

### Implementation Summary

| Capability                       | Status                            | Implementation                                         |
| -------------------------------- | --------------------------------- | ------------------------------------------------------ |
| Active Directory Domain Services | Implemented                       | Centralized Windows domain                             |
| DNS                              | Implemented                       | Active Directory-integrated name resolution            |
| Organizational Units             | Implemented                       | Business and administrative organization               |
| Identity and security groups     | Implemented                       | Centralized account and group management               |
| Windows domain workstation       | Implemented                       | Domain-joined Windows client                           |
| Group Policy                     | Implemented                       | Centralized Windows configuration                      |
| Endpoint security baseline       | Implemented in earlier milestones | Windows Defender and workstation policies              |
| Windows Event Collector          | Validated                         | Centralized event collection                           |
| Windows Event Forwarding         | Validated                         | Source-initiated event forwarding                      |
| Wazuh SIEM                       | Operational in PoC                | Centralized security event ingestion and investigation |
| Custom security detections       | Planned                           | Controlled detection engineering exercises             |
| Production migration             | Pending                           | Cost and feasibility assessment                        |

_Implementation status does not imply production readiness. Historical configurations and current operational settings are documented separately where they differ._

---

## Current Infrastructure

The following systems represent the most recently verified monitoring environment.

| System            | Operating System        | Primary Role                                                 |
| ----------------- | ----------------------- | ------------------------------------------------------------ |
| `ServerM1`        | Windows Server 2022     | Domain Controller, DNS, Windows Event Collector, Wazuh Agent |
| `COMPUTER01`      | Windows client          | Domain workstation and Windows Event Forwarding source       |
| `MENAROL-WAZUH01` | Ubuntu Server 24.04 LTS | Wazuh Manager, Indexer, and Dashboard                        |

**Current Active Directory domain:** `Menarol.local`

**Virtualization platform:** VMware Workstation

### Configuration History

Earlier implementation milestones reference different system names, including `MENAROL-SRV01`, `MENAROL-WKS01`, and the domain `menarol.com`.

During relocation of the virtualized environment, some implementation progress was lost and older configurations were restored.

The current infrastructure inventory reflects the subsequently verified environment. Earlier documentation is retained as an engineering history and should not automatically be treated as the active configuration.

Any future naming changes will be evaluated separately rather than introduced solely to align documentation.

---

## Security Monitoring Architecture

The current monitoring implementation uses native Windows Event Forwarding together with Wazuh.

```text
                  Menarol Active Directory
                         ServerM1
                            |
                  Group Policy Management
                            |
                            v
                       COMPUTER01
                    Windows Security Log
                            |
                            | Windows Event Forwarding
                            v
                        ServerM1
                   Windows Event Collector
                       ForwardedEvents
                            |
                            | Wazuh Windows Agent
                            v
                     MENAROL-WAZUH01
                        Wazuh Manager
                        Wazuh Indexer
                        Wazuh Dashboard
                            |
                            v
                 Security Event Investigation
```

### Verified Monitoring Capabilities

- A source-initiated Windows Event Forwarding subscription has been configured.
- Group Policy is used to distribute workstation event-forwarding settings.
- Selected Windows Security events are collected centrally.
- A Wazuh Windows agent is installed on the event collector.
- The agent is configured to ingest the `ForwardedEvents` channel.
- Events originating from `COMPUTER01` have been identified in Wazuh.
- The original event source and the Wazuh collection agent can be distinguished during investigation.

These results establish an operational event collection and monitoring pipeline within the PoC.

### Monitoring Limitations

The following work remains outstanding:

- Controlled failed-authentication and account-lockout detection testing.
- Privileged group membership change monitoring.
- PowerShell activity monitoring and validation.
- Custom Wazuh detection rules and alert tuning.
- Documented detection test cases and investigation procedures.
- Production logging, retention, and recovery requirements.
- Resolution or formal acceptance of remaining WEF deployment automation limitations.

---

## Implementation Phases

### Phase 01 — Enterprise Infrastructure Foundation

Established the Windows Server and Active Directory foundation, including domain services, DNS, organizational structure, identities, and security groups.

[View Phase 01 Documentation](02-Implementation-Phases/Phase-01-Enterprise-Infrastructure-Foundation/README.md)

### Phase 02 — Enterprise Endpoint Integration

Introduced Windows enterprise endpoints, domain integration, Group Policy management, workstation baselines, and endpoint security configuration.

[View Phase 02 Documentation](02-Implementation-Phases/Phase-02-Enterprise-Endpoint-Integration/README.md)

### Phase 03 — Enterprise Security Monitoring

Introduced centralized Windows event collection, source-initiated Windows Event Forwarding, and Wazuh security monitoring.

This phase remains active while additional detection engineering and monitoring validation are completed.

[View Phase 03 Documentation](02-Implementation-Phases/Phase-03-Enterprise-Security-Monitoring/README.md)

---

## Repository Navigation

| Document                                                                                     | Purpose                                         |
| -------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| [Phase 01](02-Implementation-Phases/Phase-01-Enterprise-Infrastructure-Foundation/README.md) | Enterprise infrastructure foundation            |
| [Phase 02](02-Implementation-Phases/Phase-02-Enterprise-Endpoint-Integration/README.md)      | Windows endpoint integration and security       |
| [Phase 03](02-Implementation-Phases/Phase-03-Enterprise-Security-Monitoring/README.md)       | Centralized security monitoring                 |
| [Roadmap](ROADMAP.md)                                                                        | Implementation priorities and future milestones |
| [Changelog](CHANGELOG.md)                                                                    | Project milestone and documentation history     |

Each implementation phase maintains supporting engineering records:

- **README.md:** Objectives, implementation scope, and validation status.
- **Decisions.md:** Technical decisions and their rationale.
- **Engineering-Journal.md:** Implementation activities, troubleshooting, and test results.
- **Lessons-Learned.md:** Operational findings and engineering improvements.

_Some document names and repository paths will be standardized during the publication cleanup. Existing links are retained until the corresponding files are moved or renamed._

---

## Engineering Methodology

The implementation follows a controlled engineering process:

1. **Requirements:** Identify business needs and technical constraints.
2. **Design:** Select an architecture and define implementation scope.
3. **Implementation:** Configure infrastructure components in the PoC environment.
4. **Validation:** Test functionality, security controls, and system integration.
5. **Recovery:** Establish appropriate VMware recovery checkpoints.
6. **Documentation:** Record configurations, decisions, results, and limitations.
7. **Version Control:** Review, commit, and publish engineering documentation.
8. **Improvement:** Track outstanding risks and prepare the next milestone.

A component is considered validated only when its expected behavior has been observed and recorded.

---

## Production Deployment Strategy

Menarol has not yet selected its production infrastructure or migration method.

The final decision will consider total cost of ownership, business requirements, security, system compatibility, reliability, operational complexity, and long-term maintainability.

The following approaches remain under consideration:

| Deployment Option                     | Description                                                 |
| ------------------------------------- | ----------------------------------------------------------- |
| Virtual machine migration             | Migrate compatible PoC systems to production infrastructure |
| Rebuild from validated configurations | Deploy production systems using the documented PoC design   |
| Hybrid deployment                     | Migrate selected components while rebuilding others         |

The lowest-cost option that satisfies the organization's operational and security requirements will be evaluated before a final deployment decision.

### Production Readiness Considerations

Before production implementation, the organization will need to assess:

- Hardware and infrastructure capacity.
- Windows Server and endpoint licensing.
- Active Directory naming and identity requirements.
- Network architecture and segmentation.
- Backup, restore, and disaster recovery.
- Administrative access and credential management.
- Monitoring coverage, log retention, and storage capacity.
- Security hardening and configuration management.
- Business continuity and operational support.
- Migration testing and rollback procedures.

Successful PoC validation is one input into production planning, not a substitute for production acceptance testing.

---

## Current Engineering Priorities

1. Complete and publish the current infrastructure documentation.
2. Add sanitized configuration and validation evidence.
3. Validate failed-login and account-lockout monitoring.
4. Test privileged identity and group membership change monitoring.
5. Expand Windows auditing and PowerShell event visibility.
6. Develop and validate Wazuh detection rules.
7. Document production readiness requirements and unresolved engineering decisions.

---

## Documentation and Security

This repository is intended to provide a technical record of the infrastructure implementation without exposing operational secrets.

Public documentation must not contain passwords, recovery keys, authentication tokens, private certificates, or other sensitive credentials.

Configuration screenshots and supporting evidence will be reviewed before publication.

---

## Project Status

**Active:** Enterprise Security Monitoring and Detection Engineering

**Environment:** Pre-Production Proof of Concept

**Next technical milestone:** Controlled Windows authentication failure detection and validation through the WEF-to-Wazuh monitoring pipeline.

The repository will continue to evolve as additional infrastructure components are implemented, validated, and documented.
