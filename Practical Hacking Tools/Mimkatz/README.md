# Mimikatz: Stealin Passwords

## Mimikatz Modules (Each module is essentially a group of functions that are used to carry out a specific task)

1. Crypto: Manipulation of CryptoAPI Functions
2. Kerberos: "Golden Ticket" creation via MS Kerberos API
3. Lsadump: Handles manipulation of the SAM (Security Account Managers) database. This can be used against a live system or "offline" against backup hive copies.
- Allows for access to password via LM Hash or NTLM
4. Process: Lists running processes (handy for pivots)
5. Sekurlsa: Handles extraction of data from LSASS (Local Security Authority Subsystem Service)
- This includes tickets, pin codes, keys, and passwords
6. Standard: Main module of the tool. Handles basic commands and operation
7. Token: Context discovery and limited manipulation

## Reasons Mimikatz can be so dangerous:

1. Mimikatz supports both 64-bit and 32-bit x86 architectures with separate builds. 
2. The mimikatz DLL can be loaded reflexively into memory. 
3. When combined with PowerShell (Invoke-Mimikatz) the attack can be carried out without anything being written to disk. 

Resources: 
- https://resources.infosecinstitute.com/topic/mimikatz-walkthrough/
- https://www.sentinelone.com/cybersecurity-101/mimikatz/


Commands to know. Running Mimikatz:

1. Must have local admin permissions on machine where you run Mimikatz or else it won't work. 
2. 
