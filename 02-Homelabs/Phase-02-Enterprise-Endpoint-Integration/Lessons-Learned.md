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
