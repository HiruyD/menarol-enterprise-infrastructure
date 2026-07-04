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
