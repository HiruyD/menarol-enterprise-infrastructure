# Engineering Journal

## Phase 02 – Enterprise Endpoint Integration

---

# Version 1.0 – Windows 11 Golden Image

## Summary

Created the initial Windows 11 Enterprise Golden Image that will serve as the standardized deployment source for all future enterprise workstations.

The Golden Image is intentionally maintained as a standalone workstation and will never be joined directly to the Active Directory domain.

Instead, production workstations will be created as full clones of this image before domain integration.

---

## Work Completed

- Created the WIN11-GOLDEN virtual machine.
- Configured enterprise virtual hardware standards.
- Configured VMware virtual TPM support.
- Installed Windows 11 Enterprise Evaluation.
- Created the local break-glass administrator account (menarol.admin).
- Completed the Windows Out-of-Box Experience (OOBE).
- Validated successful operating system installation.
- Created the Version 1.0 VMware snapshot.

---

## Virtual Machine Configuration

| Setting          | Value                            |
| ---------------- | -------------------------------- |
| Name             | WIN11-GOLDEN                     |
| Operating System | Windows 11 Enterprise Evaluation |
| Version          | 25H2                             |
| Memory           | 8 GB                             |
| CPU              | 1 Processor / 4 Cores            |
| Disk             | 80 GB Thin Provisioned           |
| Network          | NAT                              |
| TPM              | Enabled                          |

---

## Validation

Validation performed after installation:

```powershell
hostname

whoami

winver
```

Results

- Hostname verified as WIN11-GOLDEN.
- Local administrator account verified.
- Windows 11 Enterprise Evaluation verified.
- Operating system installation completed successfully.

---

Created Version 1.0 VMware snapshot.

---

# Version 2.0 – Enterprise Domain Workstation

## Summary

Deployed the first production Windows 11 Enterprise workstation by cloning the Golden Image and integrating it into the Menarol Active Directory environment.

The workstation was successfully joined to the **menarol.com** domain, authenticated using a domain user account, and organized within the enterprise Active Directory structure.

---

## Work Completed

- Cloned the Windows 11 Golden Image.
- Created the production workstation **MENAROL-WKS01**.
- Verified workstation hostname.
- Verified network connectivity to the Domain Controller.
- Identified and corrected the workstation DNS configuration.
- Successfully joined MENAROL-WKS01 to the **menarol.com** Active Directory domain.
- Restarted and completed domain enrollment.
- Logged in using the enterprise Engineer domain account.
- Verified successful domain authentication.
- Confirmed automatic computer object creation in Active Directory.
- Moved the workstation into **Computer Accounts → Workstations**.
- Created the Version 2.0 VMware snapshot.

---

## Validation

Validation performed after domain integration:

```powershell
hostname

whoami

ping MENAROL-SRV01

nslookup menarol.com
```

### Results

- Hostname verified as **MENAROL-WKS01**.
- Domain authentication verified using the Engineer account.
- Domain Controller name resolution verified.
- Active Directory domain name resolution verified.
- Computer object successfully registered in Active Directory.
- Workstation successfully moved into the Workstations Organizational Unit.

---

Created Version 2.0 VMware snapshot.

---

# Version 3.0 – Enterprise Group Policy Foundation

## Summary

Introduced enterprise Group Policy management into the Menarol Active Directory environment.

Established the initial enterprise Group Policy architecture by creating dedicated baseline Group Policy Objects, separating User and Computer policy design, and successfully deploying the first enterprise User Configuration policy to a production workstation.

---

## Work Completed

- Opened Group Policy Management Console.
- Reviewed the Microsoft default Group Policy Objects.
- Created GPO - Domain Security.
- Created GPO - Server Baseline.
- Created GPO - User Baseline.
- Created GPO - Workstation Baseline.
- Linked GPO - User Baseline to the User Accounts Organizational Unit.
- Configured the "Prohibit access to Control Panel and PC Settings" policy.
- Forced Group Policy processing on MENAROL-WKS01.
- Verified successful User Group Policy processing.
- Validated Control Panel restriction through Group Policy.
- Created Version 3.0 VMware snapshots for MENAROL-SRV01 and MENAROL-WKS01.

---

## Validation

Validation performed after Group Policy deployment:

```powershell
hostname

whoami

ping MENAROL-SRV01

gpupdate /force

gpresult /r
```

### Results

- Domain authentication verified.
- Domain Controller connectivity verified.
- User Group Policy processed successfully.
- GPO - User Baseline successfully applied.
- Control Panel and PC Settings successfully restricted.
- Computer Policy timeout observed during gpupdate and documented for future investigation.
- Enterprise Group Policy framework successfully established.

---

## Created Version 3.0 VMware snapshots.

# Version 4.0 – Enterprise Identity Expansion

## Summary

Expanded the Menarol Active Directory environment beyond the initial engineering accounts by creating realistic enterprise users representing multiple business units.

This milestone establishes the enterprise identity foundation required for future Group Policy targeting, file system authorization, endpoint management, and security monitoring.

---

## Work Completed

- Reviewed and validated the existing Active Directory Organizational Unit structure.
- Validated existing Global Security Groups.
- Standardized enterprise workstation naming as **MENAROL-WKS02**.
- Created enterprise users across departmental Organizational Units.
- Populated organizational user properties including:
  - Company
  - Department
  - Office
  - Job Title
- Assigned users to their appropriate Global Security Groups.
- Validated enterprise role-based identity organization.

---

## Validation

Validation performed after identity expansion:

```powershell
Active Directory Users and Computers

User Properties

Member Of
```

### Results

- Enterprise users successfully created.
- Departmental Organizational Unit placement verified.
- Global Security Group membership verified.
- Enterprise identity model successfully expanded.
- Organizational structure prepared for department-specific Group Policy deployment.

---

Created Version 4.0 VMware snapshot.
