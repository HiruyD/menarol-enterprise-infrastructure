# Lessons Learned

## Phase 03 – Enterprise Security Monitoring

---

# Lesson 001

## Validate the Entire Event Forwarding Chain

Windows Event Forwarding depends on several components working together:

- Windows Event Collector
- Event subscription configuration
- Group Policy delivery
- Windows Remote Management
- Windows Firewall
- Source authorization
- Event log permissions

An empty **Forwarded Events** log does not identify which component failed. Each layer must be validated independently.

---

# Lesson 002

## Security Log Forwarding Has Additional Permission Requirements

Forwarding the Windows Security log requires more than a working subscription and network connection. The forwarding service must have permission to read the Security log.

In the validated configuration, adding `NT AUTHORITY\NETWORK SERVICE` to the local **Event Log Readers** group established the required access.

---

# Lesson 003

## Manual Validation Is Not the Same as Enterprise Deployment

A manual configuration can be useful for proving that a technology works. It should not be treated as the final enterprise standard.

The correct workflow is:

1. Validate the technology.
2. Identify every manual prerequisite.
3. Research a supported centralized deployment method.
4. Test the method in the environment.
5. Adopt it only after successful validation.

---

# Lesson 004

## Do Not Standardize an Unverified Group Policy Method

Restricted Groups was considered for centrally managing the required local group membership. During implementation, the Group Policy editor could not resolve `NT AUTHORITY\NETWORK SERVICE` through the Active Directory object picker.

Rather than forcing an unverified configuration, the implementation was stopped and recorded as an open improvement. Enterprise standards must be based on repeatable test results, not assumptions.

---

# Lesson 005

## Avoid Changing Architecture During Configuration

The deployment process became unnecessarily confusing when implementation recommendations changed between Restricted Groups and Group Policy Preferences before the research was fully resolved.

Future infrastructure decisions should follow a controlled sequence:

- Research
- Decision
- Implementation
- Validation
- Documentation

The selected method should not change during implementation unless new evidence demonstrates that it is invalid.

---

# Lesson 006

## Functional Progress and Engineering Debt Can Be Tracked Separately

The WEF architecture can be documented as functionally validated while the zero-touch permission deployment remains open.

This allows the project to progress without hiding the limitation or presenting a temporary manual step as a completed enterprise standard.
