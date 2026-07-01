# Cybersecurity Home Lab Portfolio — Project Context

## Purpose of This File

This Markdown file is the permanent context file for my cybersecurity homelab portfolio. Whenever I upload this file in a future ChatGPT conversation, use it as the source of truth for the project so the work stays consistent and does not go out of context.

The goal is to build, document, and publish a two-year cybersecurity homelab portfolio that supports my long-term career direction in:

- IAM / Identity and Access Management
- Cloud Security
- Networking fundamentals
- Scripting and automation
- Security operations fundamentals
- Infrastructure and systems administration

This project should not be treated as random practice. It should be treated like a professional portfolio that shows progression from beginner infrastructure labs to cloud, IAM, automation, and security engineering labs.

---

## User Background and Constraints

- I am preparing for a career transition into cybersecurity.
- My target direction is IAM and Cloud Security.
- I am starting with Security+ study before and during my UMGC cybersecurity master's program.
- I already installed VMware.
- I want to build homelabs weekly or at least once every two weeks.
- I want GitHub documentation that proves practical experience, not just certifications and a degree.
- My networking and scripting skills should reach at least novice level early in the roadmap.
- I prefer step-by-step guidance, not vague instructions.
- Do not assume I already know advanced system administration concepts.
- Explain commands before asking me to run them.
- When creating labs, keep documentation clean enough for GitHub.

---

## Project Name

Primary project name:

**Cybersecurity Home Lab Portfolio**

Optional GitHub repository name:

```text
cybersecurity-homelab
```

Optional branded name for future use:

```text
menarol-cybersecurity-lab
```

Use the generic professional name unless I specifically ask to use Menarol branding.

---

## Main Project Goal

Over the next two years, build a structured cybersecurity homelab portfolio that demonstrates hands-on experience in:

1. Virtualization and lab infrastructure
2. Windows Server administration
3. Linux administration
4. Active Directory
5. DNS, DHCP, and basic networking
6. PowerShell, Bash, and Python basics
7. Security+ aligned technical labs
8. CCNA-aligned networking labs
9. Cloud fundamentals, especially AWS
10. IAM and access control
11. Terraform and Infrastructure as Code
12. Logging, monitoring, and basic detection
13. Cloud security and identity security projects

The portfolio should show growth over time.

---

## Root Folder Structure

Create the project folder like this:

```text
Cybersecurity-HomeLab/
│
├── README.md
├── ROADMAP.md
├── CHANGELOG.md
│
├── 00-Documentation/
│   ├── Lab-Network-Diagrams/
│   ├── Screenshots/
│   ├── Notes/
│   └── Templates/
│
├── 01-Infrastructure/
│   ├── VMware/
│   ├── ISOs/
│   ├── VM-Templates/
│   └── Snapshots/
│
├── 02-HomeLabs/
│   ├── Lab01-Building-the-Lab/
│   ├── Lab02-Ubuntu-Server/
│   ├── Lab03-Kali-Linux/
│   ├── Lab04-Windows-Server/
│   ├── Lab05-Active-Directory/
│   ├── Lab06-DNS/
│   ├── Lab07-DHCP/
│   ├── Lab08-Organizational-Units-and-Users/
│   ├── Lab09-Group-Policy/
│   ├── Lab10-Windows-Client-Domain-Join/
│   ├── Lab11-File-Server-and-Permissions/
│   └── Lab12-PowerShell-Administration/
│
├── 03-Scripts/
│   ├── PowerShell/
│   ├── Bash/
│   └── Python/
│
├── 04-Network-Diagrams/
│
├── 05-GitHub-Portfolio/
│
└── 06-Certification-Notes/
    ├── Security+/
    ├── CCNA/
    ├── AWS/
    └── Terraform/
```

---

## Standard Lab Folder Template

Every lab folder should follow this format:

```text
LabXX-Lab-Name/
│
├── README.md
├── Objectives.md
├── Commands.txt
├── Lessons-Learned.md
├── Screenshots/
└── Diagrams/
```

Do not create inconsistent lab structures unless there is a strong reason.

---

## Standard Lab README Template

Each lab README should use this structure:

```markdown
# Lab XX - Lab Title

## Objective

Briefly explain what this lab accomplishes.

## Why This Lab Matters

Explain how this lab connects to cybersecurity, IAM, cloud, networking, or systems administration.

## Skills Practiced

- Skill 1
- Skill 2
- Skill 3

## Tools and Technologies

- VMware Workstation
- Operating systems used
- Any relevant tools

## Lab Environment

| Component | Details |
|---|---|
| Host Machine | Windows PC |
| Virtualization | VMware |
| Network Type | NAT / Host-only / Bridged |
| VM 1 | Example |
| VM 2 | Example |

## Steps Completed

1. Step one
2. Step two
3. Step three

## Screenshots

Add screenshots here with short explanations.

## Commands Used

```bash
# Example commands go here
```

## Problems Encountered

Describe issues and how they were solved.

## Lessons Learned

Explain what was learned in plain language.

## Next Steps

Explain what this lab leads to next.
```

---

## First 12 Labs

| Lab | Topic | Main Outcome |
|---|---|---|
| Lab 01 | Building the Lab Environment | Create folder structure, understand VMware networks, prepare documentation |
| Lab 02 | Ubuntu Server | Install and configure a Linux server |
| Lab 03 | Kali Linux | Install Kali and understand its role in security testing |
| Lab 04 | Windows Server | Install Windows Server and prepare for AD |
| Lab 05 | Active Directory | Promote Windows Server to Domain Controller |
| Lab 06 | DNS | Configure and test internal DNS |
| Lab 07 | DHCP | Configure automatic IP assignment |
| Lab 08 | OUs and Users | Create users, groups, and organizational units |
| Lab 09 | Group Policy | Apply basic security and desktop policies |
| Lab 10 | Windows Client Domain Join | Join a Windows client to the domain |
| Lab 11 | File Server and Permissions | Configure shared folders and NTFS permissions |
| Lab 12 | PowerShell Administration | Automate basic admin tasks |

---

## Lab 01 Scope

Lab 01 is the first active project.

Title:

**Lab 01 - Building the Home Lab Environment**

Lab 01 deliverables:

- Create the main project folder structure.
- Create the standard documentation files.
- Confirm VMware is installed.
- Understand VMware network types:
  - NAT
  - Host-only
  - Bridged
- Create the first lab README.
- Create a place for screenshots.
- Start the project changelog.
- Prepare for the first virtual machine build.

Lab 01 should not become too complicated. The purpose is to create the foundation for future labs.

---

## VMware Network Notes

Use these explanations when teaching me VMware networking:

### NAT

The virtual machine can access the internet through the host computer, but the rest of the physical network usually cannot directly reach the VM.

Good for:

- Most beginner labs
- Internet access
- Safe isolated practice

### Host-only

The VM can communicate with the host machine and other VMs on the same host-only network, but usually cannot access the internet.

Good for:

- Isolated internal networks
- Active Directory labs
- Malware-safe or attack-defense practice later

### Bridged

The VM acts like a real machine on the physical network and receives an IP from the same network as the host computer.

Good for:

- Advanced networking tests
- Realistic network behavior

Use NAT or Host-only for most early labs. Do not recommend Bridged unless there is a clear reason.

---

## Documentation Rules

Every lab should document:

- What was built
- Why it matters
- Tools used
- Network settings
- Commands used
- Screenshots
- Problems encountered
- Lessons learned
- Next steps

Use plain but professional language.

The documentation should look good on GitHub.

---

## GitHub Portfolio Rules

When the project is ready for GitHub:

- Keep one repository for the whole homelab journey.
- Use clear folder names.
- Do not upload ISO files.
- Do not upload passwords, license keys, private IP screenshots with sensitive data, or personal information.
- Do upload Markdown documentation, screenshots, diagrams, scripts, and sanitized notes.
- Each lab should be understandable by someone reviewing my portfolio.

---

## Security and Safety Rules

For offensive security labs:

- Keep practice inside my own lab environment.
- Do not guide attacks against real public targets.
- Do not include unauthorized exploitation.
- Focus on legal, ethical, defensive learning.
- When using Kali or security tools, explain the defensive purpose.

---

## Preferred Assistant Behavior

When helping me with this project:

1. Walk me through one step at a time.
2. Give commands I can copy and paste when appropriate.
3. Explain what each command does.
4. Tell me what screenshot to take for documentation.
5. Help me write the lab README after each lab.
6. Keep the project aligned with IAM and Cloud Security.
7. Do not skip foundational knowledge.
8. Do not turn the project into random hacking labs.
9. Keep the documentation portfolio-ready.
10. At the end of each lab, summarize what I completed and what comes next.

---

## Current Status

- VMware is already installed.
- The project folder still needs to be created.
- Lab 01 is ready to begin.

---

## Next Immediate Task

Begin Lab 01:

**Create the Cybersecurity-HomeLab project folder structure on my computer.**

Recommended location on Windows:

```text
C:\Users\<MyUsername>\Documents\Cybersecurity-HomeLab
```

Alternative location:

```text
C:\Cybersecurity-HomeLab
```

Use whichever location is easier to manage.
