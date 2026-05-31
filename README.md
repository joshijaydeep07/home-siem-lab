# Home SIEM Lab — Wazuh + Sysmon on VirtualBox

A fully functional home Security Operations Center (SOC) lab built 
for learning cybersecurity detection and incident response skills.

## Lab Architecture
Windows VM (Endpoint)          Ubuntu VM (SIEM Server)
┌─────────────────────┐        ┌──────────────────────┐
│  Sysmon (logging)   │──logs─▶│   Wazuh Manager      │
│  Wazuh Agent        │        │   Wazuh Dashboard    │
│  Windows 10         │        │   Ubuntu 22.04       │
└─────────────────────┘        └──────────────────────┘
192.168.56.102                192.168.56.101
└──────── Host-Only Network ──────────┘
## Tools Used
- VirtualBox — virtualization platform
- Ubuntu 22.04 — Wazuh server operating system
- Windows 10 — monitored endpoint
- Wazuh 4.7 — SIEM platform
- Sysmon 15 — Windows event enrichment
- SwiftOnSecurity Sysmon config — community detection rules

## Detection Use Cases

| # | Attack | MITRE Technique | Wazuh Rule |
|---|--------|----------------|------------|
| 1 | Brute force login | T1110 | 100101 |
| 2 | Mimikatz credential dump | T1003.001 | Sysmon Event 10 |
| 3 | Rogue admin account | T1136.001 | 100102 |

## Repository Structure
- `sysmon-config/` — Sysmon XML configuration
- `wazuh-rules/` — Custom Wazuh detection rules
- `docs/` — Detection use case writeups

## Key Learnings
- How SIEMs collect and analyze logs from endpoints
- How Sysmon enriches Windows event logs beyond defaults
- How to write custom detection rules mapped to MITRE ATT&CK
- How to triage security alerts like a SOC analyst
- How attackers use brute force, credential dumping, and persistence

## Author
Jaydeep Joshi — Cybersecurity Student
