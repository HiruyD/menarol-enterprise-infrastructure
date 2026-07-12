# Engineering Journal

## Phase 03 – Enterprise Security Monitoring

---

# Version 1.0 – Windows Event Collector

## Summary

Windows Event Collector was deployed on `MENAROL-SRV01` to establish the centralized event collection foundation for the Menarol Enterprise Infrastructure.

---

## Work Completed

- Enabled and initialized the Windows Event Collector service.
- Confirmed that the collector service was available on `MENAROL-SRV01`.
- Prepared the server to receive events from domain-joined Windows workstations.
- Confirmed the **Forwarded Events** log was available in Event Viewer.

---

## Validation

- Windows Event Collector initialization completed successfully.
- The collector service was available and ready for subscription configuration.
- Event Viewer displayed the **Forwarded Events** log.

---

# Version 2.0 – Windows Event Forwarding

## Summary

A source-initiated Windows Event Forwarding deployment was configured for Menarol workstations. Group Policy was used for the workstation-side forwarding configuration, and the collector subscription was created on `MENAROL-SRV01`.

---

## Work Completed

- Created a source-initiated event subscription on `MENAROL-SRV01`.
- Configured the workstation Subscription Manager setting through Group Policy.
- Configured the required Windows Remote Management and firewall settings.
- Applied the workstation Group Policy to the domain workstation.
- Investigated an empty **Forwarded Events** log.
- Verified the collector, subscription, workstation policy, and network prerequisites.
- Identified Security log access as the remaining prerequisite.
- Added `NT AUTHORITY\NETWORK SERVICE` to the workstation's local **Event Log Readers** group for functional validation.
- Confirmed that the manual prerequisite established the required Security log access.
- Began testing whether the local group membership could be centrally enforced through Restricted Groups.
- Stopped the Restricted Groups implementation after the well-known local principal could not be resolved through the domain object picker.

---

## Validation

### Confirmed

- The Windows Event Collector service is deployed.
- The source-initiated subscription is configured.
- Workstation Group Policy delivery is functioning.
- Required WEF-related firewall and WinRM configuration is present.
- The required local Security log access can be established by adding `NT AUTHORITY\NETWORK SERVICE` to **Event Log Readers**.
- The WEF architecture was functionally validated on `MENAROL-WKS01`.

### Not Yet Standardized

- Zero-touch deployment of the required **Event Log Readers** membership has not yet been validated.
- The attempted Restricted Groups method was not adopted.
- The same clean deployment validation still needs to be completed on `MENAROL-WKS02` after a supported centralized method is selected.

---

## Engineering Outcome

The implementation successfully separated two concerns:

1. **Technology validation:** Prove that Windows Event Forwarding works.
2. **Deployment standardization:** Replace temporary manual prerequisites with a tested centralized configuration.

The first objective was achieved. The second remains a tracked engineering improvement and will not block documentation of the functional WEF deployment.
