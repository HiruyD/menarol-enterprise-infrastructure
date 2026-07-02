# Lessons Learned

## Phase 01 – Enterprise Infrastructure Foundation

This document records the key lessons learned during the implementation of Phase 01.

---

# Lesson 001

## Protect the Golden Image

The Windows Server baseline should never be modified after it becomes the golden image.

Instead:

- Preserve the golden image.
- Create a full clone for each new server.
- Perform all configuration on the clone.

This allows new enterprise servers to be deployed from a known-good baseline.

---

# Lesson 002

## Rename the Clone, Not the Original

Renaming or moving the parent virtual machine can cause VMware to lose track of the virtual machine files.

The preferred workflow is:

1. Keep the golden image unchanged.
2. Create a full clone.
3. Rename the clone.
4. Continue building from the clone.

---

# Lesson 003

## Domain Controllers Require Static IP Addresses

A Domain Controller should always have a static IP address before Active Directory is installed.

This ensures reliable DNS registration and consistent communication with domain clients.

---

# Lesson 004

## DNS Behavior Before Domain Promotion

Using the server as its own DNS server before installing Active Directory prevents external hostname resolution because the DNS service is not yet installed.

This behavior is expected.

After the DNS Server role is installed and forwarders are configured, both internal and external name resolution function correctly.

---

# Lesson 005

## Validate Before Continuing

Major infrastructure changes should always be validated before moving to the next milestone.

Validation performed during this phase included:

- hostname
- whoami
- nslookup
- ipconfig /all
- dcdiag

Capturing a VMware snapshot only after successful validation provides a reliable rollback point.

---

# Lesson 006

## Document Every Milestone

Each completed milestone should include:

- Engineering documentation
- Validation results
- VMware snapshot
- Git commit

This creates a repeatable deployment history and makes troubleshooting significantly easier as the environment grows.

---

# Lesson 007

## Organizational Units Should Reflect Administration

Organizational Units should be designed around administrative boundaries and Group Policy requirements rather than simply mirroring departments.

---

# Lesson 008

## Separate Standard and Administrative Accounts

Administrative activities should always be performed using dedicated privileged accounts instead of everyday user accounts.

Separating privileged identities reduces risk and aligns with enterprise security best practices.

---

# Lesson 009

## Use Security Groups Instead of Direct Permissions

Permissions should be assigned to security groups rather than individual user accounts.

This simplifies administration, improves scalability, and supports Microsoft's AGDLP authorization model.

---

# Lesson 010

## Build the Foundation Before Expanding

Establishing enterprise standards for Organizational Units, naming conventions, identities, and security groups before deploying additional systems creates a scalable infrastructure that is easier to manage as the environment grows.
