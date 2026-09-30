# Windows and Active Directory Fundamentals | TryHackMe Cyber Security 101

My notes and hands-on practice from the Windows Fundamentals rooms and Active Directory Basics in TryHackMe's Cyber Security 101 path. This module moved me from using Windows to understanding how it is managed, secured and monitored in a company environment.

## What I Learned

- **Windows basics:** the desktop and taskbar, the NTFS file system, and how NTFS permissions grant or deny access to files and folders.
- **System tools:** System Information, Resource Monitor, Device Manager, Disk Management, Shared Folders and System Configuration (`msconfig`).
- **Event Viewer:** how Windows records what happens on a machine, and the difference between the standard logs.
- **Windows security:** Windows Update, Windows Security, virus and threat protection, firewall profiles, core isolation, TPM and BitLocker.
- **Active Directory:** domains, domain controllers, users, machines and security groups.
- **Managing an environment:** Organisational Units (OUs), delegation and Group Policy.
- **Authentication:** Kerberos and NetNTLM, plus how trees and forests connect multiple domains.

## What I Practised

- Created Organisational Units to separate workstations and servers in Active Directory.
- Created a Group Policy Object (GPO) that stops non-IT users from opening the Control Panel.
- Created a GPO that locks the screen automatically after 5 minutes of inactivity.
- Linked the GPOs to the correct OUs and forced an update with `gpupdate /force`.
- Used the Command Prompt to check system and network information.

## Tools and Commands

| Tool or Command | What It Does |
|---|---|
| `hostname` | Shows the name of the machine |
| `whoami` | Shows the current user |
| `ipconfig` / `ipconfig /all` | Shows network configuration |
| `cls` | Clears the Command Prompt screen |
| `msinfo32` | System Information: a full view of the hardware and system |
| `resmon` | Resource Monitor: per-process CPU, memory, disk and network usage |
| `msconfig` | System Configuration: troubleshooting and startup issues |
| `regedit` | Registry Editor: settings for the system, users, apps and hardware |
| `gpupdate /force` | Forces Group Policy to apply straight away |

## Key Concepts

### Event Viewer

| Event Type | Standard Windows Logs |
|---|---|
| Error | Application |
| Warning | Security |
| Information | System |
| Success Audit | |
| Failure Audit | |

### Firewall Profiles

| Profile | When It Applies |
|---|---|
| Domain | The machine can authenticate to a domain controller |
| Private | A user-assigned profile for home or private networks |
| Public | The default profile, for public networks |

### Important AD Groups

| Group | What It Can Do |
|---|---|
| Domain Admins | Has administrative privileges over the domain |
| Server Operators | Can administer domain controllers |
| Backup Operators | Can back up any file, ignoring its permissions |

### Authentication

- **Kerberos:** the default protocol in recent versions of Windows. After a user logs in, they get tickets as proof of a previous authentication. The Key Distribution Center (KDC) issues a Ticket Granting Ticket.
- **NetNTLM:** a legacy protocol kept for compatibility. It works with a challenge-response mechanism.

### Trees and Forests

A **tree** joins multiple domains under the same namespace, which lets each country's IT team manage its own resources through delegation. A **forest** covers domains configured in different namespaces.

## Challenges and Mistakes

> Replace this with something real. What confused you most in this module? Was it the difference between a domain and an OU, getting the GPO to apply, or Kerberos? What finally made it click?

## Why This Matters for SOC / Blue Team Work

- **Event Viewer and the Security log:** successful and failed logons are recorded here, so this is where I would start investigating suspicious account activity.
- **Active Directory:** it controls identity and access in most companies. Knowing who belongs to groups like Domain Admins is important, because attackers often go after privileged accounts.
- **Kerberos and NetNTLM:** knowing which authentication protocol is in use helps me read authentication logs, and legacy protocols are a common weak point.
- **Defender exclusions:** excluded files and folders are not scanned, so an unexpected exclusion is something I would check during an investigation.
- **Group Policy:** this is how security settings are enforced across many machines at once, so I now see why a bad or missing policy matters.
- **Registry and System Configuration:** the registry and startup settings are common places to look when checking how something keeps running on a machine.
- **Volume Shadow Copy Service:** shadow copies are used for backup and recovery, which is why they matter when investigating ransomware.
- **BitLocker and TPM:** these protect data if a device is lost or stolen.

## Key Takeaway

Windows security is not one tool. It is layers: permissions, policies, firewall, antivirus, encryption and logging all work together, and Active Directory is what ties them across a whole company. Doing the Group Policy tasks myself made it click that one policy can change the behaviour of hundreds of machines.

## Next Step

A small Windows log investigation: open Event Viewer on my own machine, filter the Security log for logon events, find one successful and one failed logon, and write up what each event tells me.
