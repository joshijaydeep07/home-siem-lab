# Detection Use Case 02 — Mimikatz Credential Dumping

## What is this attack?
Mimikatz is a post-exploitation tool that extracts passwords, hashes, 
and Kerberos tickets from Windows memory. It targets the LSASS process 
(Local Security Authority Subsystem Service) which stores credential 
information. It is used in almost every major ransomware attack.

## MITRE ATT&CK Mapping
- Tactic: Credential Access
- Technique: T1003.001 — LSASS Memory Dumping

## How I simulated it
On the Windows endpoint VM with Windows Defender disabled:

```powershell
mimikatz.exe "privilege::debug" "sekurlsa::logonpasswords" "exit"
```

## How it was detected
- Sysmon Event ID 10 (process access) fired when Mimikatz 
  accessed lsass.exe memory
- The Wazuh agent forwarded the Sysmon log to the server
- Wazuh detected the LSASS access pattern

## Alert evidence
Mimikatz accessed LSASS process memory
Target process: C:\Windows\System32\lsass.exe
Source process: mimikatz.exe

## Incident response steps
1. Isolate the affected machine from the network immediately
2. Assume ALL credentials on that machine are compromised
3. Force password reset for every user who logged into that machine
4. Check for lateral movement to other machines using those credentials
5. Look for persistence mechanisms (scheduled tasks, registry keys)
6. Re-image the machine — do not trust it after credential theft

## Detection rule
Detected via Sysmon Event ID 10 forwarded through Wazuh agent
