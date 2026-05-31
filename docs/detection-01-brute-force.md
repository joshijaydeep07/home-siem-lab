# Detection Use Case 01 — Brute Force Login Attack

## What is this attack?
A brute force attack is when an attacker tries many different passwords 
repeatedly against an account hoping to guess the correct one. This is 
one of the most common attack techniques used against Windows systems 
exposed to a network.

## MITRE ATT&CK Mapping
- Tactic: Credential Access
- Technique: T1110 — Brute Force
- Sub-technique: T1110.001 — Password Guessing

## How I simulated it
On the Windows endpoint VM I ran a PowerShell loop that attempted 
10 failed logins against the local Administrator account:

```powershell
for ($i=1; $i -le 10; $i++) {
    net use \\localhost\IPC$ /user:Administrator "WrongPassword$i"
}
```

## How it was detected
- Windows generated Event ID 4625 (logon failure) for each attempt
- Sysmon forwarded these to the Wazuh agent
- Wazuh built-in rule 60122 fired for each individual failure
- My custom rule 100101 fired when 5+ failures occurred within 60 seconds

## Alert evidence
Rule: 100101 (level 12) -> 'BRUTE FORCE DETECTED - Multiple failed logins in 60 seconds'

## Incident response steps
1. Identify the source IP of the failed login attempts
2. Block that IP at the firewall immediately
3. Check if any login eventually succeeded after the failures
4. Review all activity from that account for the past 24 hours
5. Reset the targeted account password
6. Enable account lockout policy to prevent future brute force

## Detection rule
Located in `wazuh-rules/local_rules.xml` — rule ID 100101
