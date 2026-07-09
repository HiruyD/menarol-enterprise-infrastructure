# Engineering Decisions

## Phase 02 – Enterprise Endpoint Integration

---

# Decision 001

## Deploy a Golden Image First

### Decision

Deploy a dedicated Windows 11 Enterprise Golden Image before creating production workstations.

### Reason

Maintaining a reusable master image ensures every workstation begins from an identical baseline while simplifying deployment, recovery, and future maintenance.

---

# Decision 002

## Local Break-Glass Administrator

### Decision

Create a dedicated local administrator account:

menarol.admin

### Reason

The account provides emergency local administrative access without conflicting with enterprise domain accounts.

Future domain administration will be performed using dedicated Active Directory administrative identities.

---

# Decision 003

## Enterprise Workstation Hardware Standard

### Decision

Adopt the following virtual hardware baseline:

- 8 GB Memory
- 4 Virtual CPUs
- 80 GB Thin-Provisioned Disk
- Virtual TPM
- NAT Networking

### Reason

Provides sufficient performance while maintaining efficient host resource utilization and establishing a repeatable enterprise workstation standard.

---

# Decision 004

## Preserve the Golden Image

### Decision

The Golden Image will remain a standalone workstation and will never join the Active Directory domain.

### Reason

Production workstations will always be deployed as clones.

This preserves a clean deployment source and mirrors enterprise imaging practices.

---

# Decision 005

## Preserve the Golden Image as the Deployment Source

### Decision

Production workstations will always be created as full clones of the Windows 11 Golden Image.

### Reason

Maintaining an untouched Golden Image ensures every workstation begins from a standardized, validated baseline while simplifying future deployments, recovery, and lifecycle management.

---

# Decision 006

## Use the Domain Controller for Enterprise DNS

### Decision

All domain-joined workstations will use **MENAROL-SRV01** as their preferred DNS server.

### Reason

Active Directory relies on DNS for locating domain controllers, authentication services, and other directory resources. Using the Domain Controller as the preferred DNS server ensures reliable domain operations and mirrors enterprise best practices.

---

# Decision 007

## Organize Production Workstations in Dedicated Organizational Units

### Decision

After joining the domain, production workstations will be moved from the default **Computers** container into the **Computer Accounts → Workstations** Organizational Unit.

### Reason

Placing workstations in a dedicated Organizational Unit enables targeted Group Policy deployment, improves administrative organization, and supports future enterprise endpoint management.

---

# Decision 008

## Separate User and Computer Group Policy Objects

### Decision

Maintain separate baseline Group Policy Objects for User Configuration and Computer Configuration.

### Reason

Separating user and computer policies improves administrative organization, simplifies troubleshooting, and aligns with enterprise Group Policy design best practices.

---

# Decision 009

## Preserve Microsoft Default Group Policy Objects

### Decision

The Default Domain Policy and Default Domain Controllers Policy will remain unchanged except for settings that Microsoft intends to be configured within those policies, such as domain password and account lockout policies.

### Reason

Maintaining the Microsoft default Group Policy Objects reduces administrative risk while allowing enterprise-specific configurations to be managed independently through dedicated baseline Group Policy Objects.

---

# Decision 010

## Link Group Policy Objects According to Object Type

### Decision

User Configuration Group Policy Objects will be linked to Organizational Units containing user accounts, while Computer Configuration Group Policy Objects will be linked to Organizational Units containing computer accounts.

### Reason

Applying Group Policy according to the object type provides a cleaner enterprise design, simplifies policy management, and improves future scalability as the Menarol infrastructure grows.
