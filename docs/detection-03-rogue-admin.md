# Detection Use Case 03 — Rogue Administrator Account

## What is this attack?
After gaining access to a system, attackers create a hidden 
administrator account to maintain persistent access even if 
their initial entry point is discovered and closed. This is 
called persistence.

## MITRE ATT&CK Mapping
- Tactic: Persistence
- Technique: T1136.001 — Create Local Account

## How I simulated it
On the Windows endpoint VM:

```powershell
net user hacker P@ssw0rd123 /add
net localgroup administrators hacker /add
```

## How it was detected
- Windows generated Event ID 4720 (new account created)
- Windows generated Event ID 4732 (account added to privileged group)
- Wazuh rule 60109 fired for the account creation
- My custom rule 100102 fired specifically for admin group addition

## Alert evidence
Rule: 100102 (level 14) -> 'ROGUE ADMIN DETECTED - User added to administrators group'

## Incident response steps
1. Immediately disable the suspicious account
2. Check when the account was created and what it accessed
3. Review all login events for that account
4. Search for other unauthorized accounts created around the same time
5. Determine how the attacker gained the privileges to create accounts
6. Patch the initial access vulnerability

## Detection rule
Located in `wazuh-rules/local_rules.xml` — rule ID 100102
