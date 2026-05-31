# 🛡️ Home SIEM Lab — Wazuh + Sysmon on VirtualBox

A fully functional home Security Operations Center (SOC) lab built for learning cybersecurity detection and incident response skills.

---

## 🏗️ Lab Architecture

| Component | Details |
|---|---|
| **SIEM Server** | Ubuntu 22.04 — IP: 192.168.56.101 |
| **Endpoint** | Windows 10 — IP: 192.168.56.102 |
| **Network** | VirtualBox Host-Only (isolated, safe) |
| **Log flow** | Windows → Sysmon → Wazuh Agent → Wazuh Server |

```
[Windows 10 VM]  ── logs ──▶  [Ubuntu VM]
  Sysmon                        Wazuh Manager
  Wazuh Agent                   Wazuh Dashboard
  192.168.56.102                192.168.56.101
```

---

## 🛠️ Tools Used

| Tool | Version | Purpose |
|---|---|---|
| VirtualBox | 7.x | Virtualization platform |
| Ubuntu Server | 22.04 LTS | Wazuh server OS |
| Windows 10 | Pro | Monitored endpoint |
| Wazuh | 4.7 | SIEM platform |
| Sysmon | 15.x | Windows event enrichment |
| SwiftOnSecurity config | Latest | Sysmon detection rules |

---

## 🎯 Detection Use Cases

| # | Attack | MITRE Technique | Rule ID | Severity |
|---|---|---|---|---|
| 1 | Brute force login | T1110 | 100101 | Level 12 |
| 2 | Mimikatz credential dump | T1003.001 | Sysmon Event 10 | Level 15 |
| 3 | Rogue admin account created | T1136.001 | 100102 | Level 14 |

---

## 📁 Repository Structure

```
home-siem-lab/
├── README.md
├── sysmon-config/
│   └── sysmonconfig.xml       # Sysmon configuration file
├── wazuh-rules/
│   └── local_rules.xml        # Custom Wazuh detection rules
└── docs/
    ├── detection-01-brute-force.md
    ├── detection-02-mimikatz.md
    └── detection-03-rogue-admin.md
```

---

## 📖 Key Learnings

- How SIEMs collect and analyze logs from endpoints
- How Sysmon enriches Windows event logs beyond defaults
- How to write custom detection rules mapped to MITRE ATT&CK
- How to triage security alerts like a SOC analyst
- How attackers use brute force, credential dumping, and persistence

---

## ✅ Alerts Confirmed Working

Both custom rules were verified firing in the Wazuh alerts log:

```
Rule: 100101 (level 12) -> 'BRUTE FORCE DETECTED - Multiple failed logins in 60 seconds'
Rule: 100102 (level 14) -> 'ROGUE ADMIN DETECTED - User added to administrators group'
```

---

## 👤 Author

**Jaydeep Joshi** — Cybersecurity Student  
Building hands-on security skills through home lab projects.
