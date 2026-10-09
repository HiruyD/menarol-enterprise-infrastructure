# Engineering Decisions

## Phase 03 — Enterprise Security Monitoring

**Project:** Menarol Enterprise Infrastructure
**Environment:** Pre-Production Proof of Concept
**Status:** Active

This document records the technical decisions made during the implementation of centralized security monitoring.

Each decision identifies the selected approach, the engineering rationale, and any relevant limitations.

---

## Decision 001 — Centralize Windows Event Collection

**Decision:** Deploy Windows Event Collector (WEC) before introducing third-party security monitoring platforms.

### Rationale

Native Windows Event Forwarding provides a centrally managed method of collecting Windows events.

Implementing WEC first establishes an understanding of event generation, forwarding, subscriptions, and collection before introducing additional monitoring technologies.

It also allows the Microsoft event collection architecture to be validated independently of a SIEM platform.

**Status:** Implemented and validated.

---

## Decision 002 — Use Source-Initiated Windows Event Forwarding

**Decision:** Use source-initiated Windows Event Forwarding subscriptions for domain workstations.

### Rationale

Source-initiated subscriptions allow domain-joined workstations to receive their Subscription Manager configuration through Group Policy.

This reduces the need to configure individual collector-initiated connections and provides a more scalable approach for future workstation deployments.

### Implementation

- Windows Event Collector hosted on `ServerM1`.
- Subscription named `Menarol Security Events`.
- Group Policy Object named `Menarol - Windows Event Forwarding`.
- Events collected in the `ForwardedEvents` channel.

**Status:** Functionally validated.

---

## Decision 003 — Validate Functionality Before Standardizing Deployment

**Decision:** Permit controlled manual configuration during initial validation, but do not automatically adopt manual procedures as the enterprise deployment standard.

### Rationale

During the original Windows Event Forwarding implementation, Security log forwarding required additional access for `NT AUTHORITY\NETWORK SERVICE`.

Adding the principal to the workstation's local `Event Log Readers` group allowed the forwarding architecture to be validated.

This helped distinguish the access issue from potential collector, subscription, firewall, WinRM, or Group Policy connectivity problems.

### Engineering Principle

A temporary configuration used to establish functionality must be separately evaluated for repeatability, security, and centralized deployment before production adoption.

**Status:** Validation completed; centralized deployment improvement remains open.

---

## Decision 004 — Do Not Adopt an Unvalidated Restricted Groups Configuration

**Decision:** Do not adopt the attempted Restricted Groups configuration for `NT AUTHORITY\NETWORK SERVICE` as the Menarol deployment standard.

### Rationale

During the original implementation, the Group Policy object picker attempted to resolve `NETWORK SERVICE` through Active Directory and could not resolve the well-known security principal.

The proposed configuration was not successfully validated in the environment.

### Current Position

- The manual configuration was retained for the originally validated workstation.
- A centrally managed alternative remains to be evaluated.
- Security log access control changes must be tested before standardization.
- Security log SDDL will not be modified without a defined requirement and controlled validation.

**Status:** Restricted Groups approach not adopted; alternative deployment method pending.

---

## Decision 005 — Integrate Wazuh with the Existing Windows Event Collector

**Decision:** Install the Wazuh Windows agent on the existing Windows Event Collector and ingest the `ForwardedEvents` event channel.

### Rationale

The Windows Event Forwarding architecture was already collecting events centrally.

Using the collector as the Wazuh ingestion point allows the existing Microsoft collection pipeline to be retained without immediately deploying a Wazuh agent to every domain workstation.

This also provides an opportunity to evaluate centralized event collection and SIEM ingestion as separate architectural components.

### Implementation

- Wazuh agent installed on `ServerM1`.
- Agent configured to monitor `ForwardedEvents`.
- Wazuh Manager, Indexer, and Dashboard deployed on `MENAROL-WAZUH01`.

### Limitations

This approach depends on the availability and correct configuration of the Windows Event Collector.

Monitoring coverage is limited to events selected for forwarding and successfully collected.

Additional event sources may require separate collection methods or direct agents in future deployments.

**Status:** Implemented and validated in the PoC.

---

## Decision 006 — Validate Original Event Source Attribution

**Decision:** Confirm that Wazuh preserves enough information to identify the original workstation generating a forwarded Windows event.

### Rationale

When Wazuh collects events from the Windows Event Collector, the Wazuh agent identifies the collector rather than the originating workstation.

Investigations must distinguish the collection host from the actual event source.

### Validation

An event observed through Wazuh contained:

- Wazuh agent: `ServerM1`
- Original computer: `Computer01.Menarol.local`
- Windows event channel: `Security`
- Event ID: `4634`

The event could be associated with its original workstation despite being collected through the Wazuh agent on the server.

**Status:** Validated.

---

## Decision 007 — Preserve the Current Working Infrastructure After VM Recovery

**Decision:** Retain the currently functioning infrastructure names and configuration rather than renaming systems solely to match earlier documentation.

### Rationale

Relocation and recovery of the virtualized environment resulted in some loss of implementation progress and the reappearance of earlier configurations.

The recovered environment was subsequently used to validate Windows Event Forwarding and Wazuh integration.

Renaming an operational domain controller or modifying Active Directory settings solely for documentation consistency would introduce unnecessary risk.

### Current Operational Baseline

- Active Directory domain: `Menarol.local`
- Domain Controller and WEC: `ServerM1`
- Domain workstation: `COMPUTER01`
- Wazuh server: `MENAROL-WAZUH01`

### Follow-Up

- Preserve earlier implementation history.
- Document the current verified environment.
- Revalidate historical settings where necessary.
- Evaluate future naming changes through a separate change-management process.

**Status:** Adopted for the current PoC.

---

## Decision 008 — Separate PoC Validation from Production Approval

**Decision:** Treat the VMware implementation as a pre-production proof of concept rather than an approved production deployment.

### Rationale

Successful technical validation demonstrates that specific configurations and integrations function within the test environment.

It does not establish production readiness, business acceptance, resilience, licensing compliance, or operational support requirements.

### Production Options Under Consideration

- Migration of compatible virtual machines.
- Rebuilding production systems from validated configurations.
- A hybrid approach combining migration and clean deployment.

The selected option will depend on cost, feasibility, security, reliability, and operational requirements.

**Status:** Production decision pending.

---

## Decision 009 — Prioritize Controlled Detection Testing

**Decision:** Begin controlled authentication monitoring tests using the existing WEF-to-Wazuh pipeline before expanding to additional monitoring technologies.

### Rationale

The event collection pipeline has been validated using an observed Windows Security event.

The next step is to determine whether it can support repeatable security monitoring scenarios, beginning with failed authentication.

This allows event generation, collection, ingestion, and detection behavior to be evaluated independently.

### Initial Test Scope

- Failed authentication events (4625).
- Account lockout events (4740), where appropriate.
- Event source attribution.
- Wazuh event visibility and rule behavior.
- Documentation of results and limitations.

**Status:** Approved engineering direction; testing not yet completed.

---

## Open Engineering Decisions

The following items require further evaluation before a final standard is established:

| Topic                              | Current Position                                                                           |
| ---------------------------------- | ------------------------------------------------------------------------------------------ |
| WEF Security log access deployment | Centrally managed method not yet validated                                                 |
| Direct Wazuh agents on endpoints   | Not required for the current validated collection path; future coverage assessment pending |
| Advanced Audit Policy              | Further requirements and validation pending                                                |
| PowerShell logging                 | Planned                                                                                    |
| Sysmon deployment                  | Planned                                                                                    |
| Wazuh retention and storage        | Production requirements pending                                                            |
| Production infrastructure          | Cost and feasibility assessment pending                                                    |

---

## Decision Management

Future decisions should document:

1. The technical problem or requirement.
2. The selected approach.
3. The rationale and alternatives considered.
4. Implementation or validation evidence.
5. Risks, limitations, and outstanding work.

A proposed configuration will not be documented as an approved enterprise standard until it has been successfully validated.

---

## 2026-10-09 — Decision 010 — Record Focused Validation Within Its Evidence Limits

**Decision:** Retain the current COMPUTER01 → WEF → ServerM1/WEC → Wazuh agent 001 → MENAROL-WAZUH01 architecture and distinguish forwarded workstation telemetry from local ServerM1 SCA/FIM coverage.

**Rationale:** Two controlled 4625 records demonstrate built-in rule 60122 at severity 5, not a real attack or brute-force correlation. The password-length change from 7 to 14 is one remediation verified in AD and SCA check 27003; three earlier corrected checks resulted from reassessment. FIM rules 554/550/553 validate the local test directory only.

**Status:** Adopted for reporting the [9 October validation](Validation-2026-10-09.md). This updates Decision 009's earlier planned status for failed-logon testing only. Account-lockout testing remains pending.

Do not treat a passing SCA reassessment as a permanent fix for post-reboot inconsistency, or the WEF timeout reduction from 900000 to 30000 milliseconds as a measured latency improvement. Keep temporary account cleanup and GPO backup confirmation unverified. Custom rules, advanced logging, WEF permission automation, and production readiness require separate validation.

---

## 2026-10-09 — Cleanup Verification Clarification

User-supplied verification confirms `secplus.test` is disabled (`Enabled=False`) and `C:\Menarol-FIM-Test\monitoring-test.txt` is absent (`Test-Path=False`). The empty demonstration folder and its FIM configuration remain intentionally retained.

This clarification supersedes the pending account/file cleanup status in the earlier 9 October entry, which is retained as history. See the [updated validation record](Validation-2026-10-09.md). GPO backup confirmation remains unverified. SCA inconsistency after reboot, account-lockout testing, custom rules, advanced logging, WEF permission automation, and production readiness remain unresolved or pending.
