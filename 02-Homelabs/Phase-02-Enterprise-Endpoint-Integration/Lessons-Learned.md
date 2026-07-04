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
