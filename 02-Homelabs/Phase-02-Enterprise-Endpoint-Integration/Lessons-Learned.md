# Lessons Learned

## Phase 02 – Enterprise Endpoint Integration

---

# Lesson 001

## Create the Golden Image Before Domain Integration

Creating a reusable Golden Image before joining workstations to Active Directory provides a clean deployment source for every future enterprise workstation.

---

# Lesson 002

## Separate Local and Domain Administration

Maintaining a dedicated local administrative account separate from enterprise domain accounts provides an emergency recovery method if domain authentication becomes unavailable.

---

# Lesson 003

## Standardize Virtual Hardware

Defining workstation hardware standards before deploying production clients simplifies administration and ensures consistency across the enterprise environment.

---

# Lesson 004

## Validate Before Snapshot

The operating system installation should always be validated before creating a VMware snapshot.

Validation performed:

- hostname
- whoami
- winver

Capturing the snapshot after validation provides a reliable rollback point.

---

# Lesson 005

## Active Directory Depends on Proper DNS Configuration

The workstation initially failed to join the domain because it was using the default gateway as its DNS server instead of the Active Directory Domain Controller.

Updating the preferred DNS server to **MENAROL-SRV01** immediately resolved domain name resolution and allowed the workstation to successfully join the domain.

---

# Lesson 006

## Verify Network Connectivity Before Domain Join

Validating hostname resolution, network connectivity, and DNS before attempting to join Active Directory significantly reduces troubleshooting time.

The following commands should be included in future workstation deployments:

- ipconfig /all
- ping MENAROL-SRV01
- nslookup menarol.com
- hostname

---

# Lesson 007

## Preserve the Golden Image

The Windows 11 Golden Image should never be joined directly to Active Directory.

Instead, every production workstation should be deployed as a full clone of the Golden Image, ensuring a clean, reusable, and standardized deployment source.

---

# Lesson 008

## Organize Computer Objects Immediately After Domain Join

New domain-joined workstations are placed in the default **Computers** container.

Moving production systems into the **Computer Accounts → Workstations** Organizational Unit immediately after joining the domain establishes proper organization and prepares the environment for future Group Policy deployment.

---

# Lesson 009

## Separate User and Computer Group Policy Objects

Maintaining separate baseline Group Policy Objects for User Configuration and Computer Configuration creates a cleaner enterprise architecture while simplifying administration, troubleshooting, and future expansion.

---

# Lesson 010

## Link Group Policy Objects to the Correct Organizational Unit

Group Policy Objects should be linked to the Organizational Unit containing the objects they are intended to manage.

User Configuration policies should target user accounts, while Computer Configuration policies should target computer accounts.

Following this practice improves policy processing, reduces administrative complexity, and aligns with enterprise Active Directory design principles.

---

# Lesson 011

## Always Validate Group Policy Deployments

Creating and linking a Group Policy Object does not guarantee successful deployment.

Every Group Policy implementation should be validated using both administrative tools and functional testing.

Validation methods used during this milestone included:

- gpupdate /force
- gpresult /r
- Domain authentication verification
- Functional verification by confirming Control Panel restrictions

---

# Lesson 012

## Separate User and Computer Baselines Early

Establishing dedicated baseline Group Policy Objects early in the project creates a scalable management model.

This approach allows future workstation, server, and user policies to evolve independently while maintaining a consistent enterprise Group Policy structure.

---

# Lesson 011

## Build Enterprise Identities Before Expanding Security Controls

Creating a realistic enterprise identity structure before implementing additional Group Policies, file permissions, monitoring, and security tooling provides a scalable administrative foundation.

Representing real business departments rather than generic test accounts allows future security controls to reflect actual enterprise operations.

---

# Lesson 012

## Organizational Units and Security Groups Serve Different Purposes

Organizational Units determine administrative organization and Group Policy scope.

Global Security Groups determine authorization and resource access.

Maintaining this separation aligns with Microsoft's enterprise Active Directory design recommendations and simplifies long-term administration.

---

# Lesson 013

## Group Policy Objects Must Be Linked Before They Can Be Applied

Creating a Group Policy Object does not make it active.

The policy must be linked to the appropriate Organizational Unit before Active Directory can process it.

Validation using `gpresult` confirmed successful deployment after the Workstation Baseline Group Policy Object was linked to the Workstations Organizational Unit.

---

# Lesson 014

## Define Group Policy Ownership Before Expanding Security Baselines

Enterprise Group Policies should be organized according to administrative responsibility before adding large numbers of security settings.

Establishing ownership boundaries between Domain Security, Server Baseline, Workstation Baseline, and User Baseline Group Policy Objects provides a scalable architecture while reducing future rework.

---

# Lesson 015

## Validate Endpoint Protection Using PowerShell

Enterprise administrators should validate Microsoft Defender using PowerShell rather than relying solely on graphical interfaces.

Commands such as `Get-MpComputerStatus` provide authoritative confirmation of operational status and are suitable for automation and enterprise troubleshooting.

---

# Lesson 016

## Group Policy Validation Should Include Both User and Computer Policies

Successful Group Policy deployment requires validating both User Configuration and Computer Configuration.

Using `gpresult` confirmed that the Workstation Baseline and User Baseline Group Policy Objects were correctly applied to the intended Active Directory objects.

---

# Lesson 017

## SmartScreen Complements Microsoft Defender

Microsoft Defender Antivirus protects against malware execution, while Microsoft Defender SmartScreen provides protection against malicious websites, phishing attempts, and untrusted downloads.

Deploying both technologies creates a layered endpoint defense strategy consistent with enterprise security best practices.
