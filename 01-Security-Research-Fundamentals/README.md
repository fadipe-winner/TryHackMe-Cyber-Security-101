# Module 1: Security Research Fundamentals

## Overview

The beginning of Cyber Security 101 revisited **offensive and defensive security**, which I had already covered during the TryHackMe Pre Security path.

Because those concepts were already familiar to me, I focused more on the new part of the module: learning how cybersecurity professionals can use resources such as **Shodan, VirusTotal, CVEs, and GitHub** to research systems, suspicious activity, threats, and vulnerabilities.

---

## Offensive and Defensive Security

This part was mainly a refresher for me.

**Offensive security** focuses on finding and understanding weaknesses in systems from an attacker's point of view.

**Defensive security** focuses on protecting systems, monitoring activity, detecting threats, and responding to security incidents.

Since I am interested in SOC and Blue Team security, I found it useful to reinforce the idea that understanding how attackers operate can also help defenders recognise suspicious activity.

---

## Shodan Practical

Shodan is a **search engine for Internet of Things (IoT) devices and other internet-connected systems**.

It scans the internet and can be used to search for publicly exposed systems such as:

- Networking equipment
- Industrial control systems
- Traffic cameras
- Servers
- Other devices connected to a public network

Shodan also supports search filters such as:

```text
country:
port:
org:
hostname:
```

These filters make it easier to narrow down search results.

### What I Learned

I learned that an IP address can be searched on Shodan to find information that Shodan has collected about publicly exposed services associated with that address.

For security investigations, this can provide additional context about an external system.

However, Shodan results alone do not mean that a system is malicious. The information would still need to be compared with other evidence.

---

## VirusTotal Practical

VirusTotal collects results from **over 70 antivirus engines and website scanners into a single interface**.

This makes it useful for checking suspicious indicators without having to use many different security services separately.

VirusTotal can be used to investigate things such as:

- Files
- File hashes
- URLs
- Domains
- IP addresses

For example, if a suspicious file is found during an investigation, its hash can be searched on VirusTotal to see how different security vendors have classified it.

```text
Suspicious File
      ↓
Get File Hash
      ↓
Search VirusTotal
      ↓
Review Results
```

### What I Learned

VirusTotal can give an analyst useful information about something suspicious, but its results still need to be interpreted.

For example, a file having no detections does not automatically mean that the file is safe.

This means VirusTotal should be used as part of an investigation rather than as the only source of evidence.

---

## Vulnerability Research and CVEs

**Common Vulnerabilities and Exposures (CVE)** is more or less like a **dictionary of known publicly disclosed vulnerabilities**.

Each vulnerability is assigned a unique identifier using a format such as:

```text
CVE-YEAR-NUMBER
```

For example:

```text
CVE-2026-1337
```

This makes it easier for security researchers, vendors, and organisations to refer to the same vulnerability.

When researching a vulnerability, some of the things worth considering include:

- Its impact
- How difficult it is to exploit
- The affected software or system
- Whether availability, confidentiality, or integrity could be affected
- Whether a fix or patch is available

This helped me understand that knowing a CVE number is only the beginning. The important part is understanding **what the vulnerability affects and how serious it could be**.

---

## GitHub for Security Research

Before this module, I mostly used GitHub for documenting my own cybersecurity learning.

I learned that **GitHub is also a useful resource for staying updated on threats and vulnerabilities**.

Security researchers may use GitHub to share:

- Vulnerability research
- Security tools
- Technical explanations
- Proof-of-concept code

### CVE Research Practical

During the TryHackMe practical, I searched GitHub for the fictional vulnerability:

```text
CVE-2026-1337
```

I opened the related repository, read the README, and identified the Python script used to demonstrate the vulnerability:

```text
exploit.py
```

The main thing I learned from this exercise was how GitHub can be used as a research resource when investigating a vulnerability.

The goal was not to run the exploit, but to understand how to:

```text
Find a CVE
    ↓
Search for research about it
    ↓
Read the repository documentation
    ↓
Identify relevant files
    ↓
Understand what the vulnerability affects
```

---

## How This Relates to SOC Work

One thing I noticed is that each resource can help answer a different question during an investigation.

```text
External IP
    ↓
Shodan

Suspicious File / Hash / URL
    ↓
VirusTotal

Known Vulnerability
    ↓
CVE Research

Technical Vulnerability Information
    ↓
GitHub
```

A SOC analyst may use these resources to gather more information, but the results should still be compared with logs, alerts, endpoint activity, network activity, and other available evidence.

---

## Key Takeaway

The offensive and defensive security part of this module mostly reinforced what I had already learned during Pre Security.

The main new thing I took from this module was learning how to **research security information more effectively**.

I now have a better understanding of how Shodan can provide information about publicly exposed systems, how VirusTotal can help investigate suspicious indicators, how CVEs are used to identify known vulnerabilities, and how GitHub can be used to find security research.

The biggest lesson for me is that one source does not normally tell the whole story. During an investigation, I need to gather information from different sources and understand the context before making a conclusion.
