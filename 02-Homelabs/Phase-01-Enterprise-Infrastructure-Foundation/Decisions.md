# Engineering Decisions

## Phase 01 – Enterprise Infrastructure Foundation

This document records the major technical decisions made during Phase 01 and the reasoning behind them.

---

# Decision 001

## Use VMware Workstation

### Decision

VMware Workstation was selected as the primary virtualization platform.

### Reason

- Mature virtualization platform
- Snapshot capability
- Excellent Windows Server compatibility
- Widely used for enterprise labs

---

# Decision 002

## Windows Server 2022

### Decision

Deploy Windows Server 2022 Standard Evaluation.

### Reason

- Current Long-Term Servicing Channel (LTSC)
- Supports all planned enterprise services
- Appropriate platform for learning modern Windows administration

---

# Decision 003

## Server Naming Standard

### Decision

Use:

MENAROL-SRV01

### Reason

The naming convention is simple, scalable, and descriptive.

Future servers will follow the same convention.

Examples:

- MENAROL-FS01
- MENAROL-APP01
- MENAROL-WEB01
- MENAROL-CA01

---

# Decision 004

## Static IP Address

### Decision

Assign a static IPv4 address before installing Active Directory.

### Reason

Domain Controllers should not rely on DHCP because clients and services depend on consistent addressing.

---

# Decision 005

## Active Directory Forest Name

### Decision

Forest Root Domain:

menarol.com

NetBIOS Name:

MENAROL

### Reason

Using a routable DNS namespace aligns with current Microsoft best practices and supports future hybrid identity integration.

---

# Decision 006

## DNS Architecture

### Decision

Install DNS on the first Domain Controller.

Configure DNS forwarders for external name resolution.

### Reason

The Domain Controller should remain authoritative for the Active Directory namespace while forwarding external requests to public DNS servers.

---

# Decision 007

## Versioned Milestones

### Decision

Manage the project using versioned milestones.

### Reason

Each milestone represents a stable infrastructure state that includes:

- Validation
- VMware Snapshot
- Documentation
- Git Commit

This approach provides a reproducible deployment history and simplifies future troubleshooting.

---
