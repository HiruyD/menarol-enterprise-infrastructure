# Engineering Journal

## Phase 01 – Enterprise Infrastructure Foundation

This journal documents the implementation work completed during Phase 01 of the Menarol Enterprise Lab.

---

## Version 1.0 – Windows Server Baseline

### Summary

Built the initial Windows Server 2022 baseline virtual machine to serve as the foundation for future enterprise servers.

### Work Completed

- Created the Windows Server 2022 virtual machine in VMware Workstation.
- Installed Windows Server 2022 Standard Evaluation.
- Installed VMware Tools.
- Renamed the server to **MENAROL-SRV01**.
- Configured the system time zone.
- Verified successful reboot after hostname change.
- Created the Version 1.0 baseline snapshot.

### Validation

- Confirmed the server booted successfully.
- Verified hostname after reboot.
- Confirmed VMware Tools installation completed.
- Confirmed the Version 1.0 snapshot was created.

---

## Version 2.0 – Enterprise Active Directory Foundation

### Summary

Promoted **MENAROL-SRV01** from a standalone Windows Server into the first Domain Controller for the Menarol enterprise environment.

### Work Completed

- Configured a static IPv4 address for the server.
- Installed the Active Directory Domain Services role.
- Installed the DNS Server role as part of Domain Controller promotion.
- Created a new Active Directory forest named **menarol.com**.
- Promoted **MENAROL-SRV01** as the first Domain Controller.
- Configured the NetBIOS domain name as **MENAROL**.
- Configured DNS forwarders for external name resolution.
- Verified internal and external DNS resolution.
- Ran Domain Controller diagnostics using `dcdiag`.
- Created the Version 2.0 snapshot.

### Network Configuration

| Setting         | Value                     |
| --------------- | ------------------------- |
| IPv4 Address    | 192.168.45.10             |
| Subnet Mask     | 255.255.255.0             |
| Default Gateway | 192.168.45.2              |
| DNS Server      | 127.0.0.1 / 192.168.45.10 |
| Domain          | menarol.com               |

### Validation Commands

```powershell
hostname
whoami
ipconfig /all
nslookup menarol.com
nslookup google.com
dcdiag
```
