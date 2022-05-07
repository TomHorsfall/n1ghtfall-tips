# Mimikatz: Stealin Passwords

## Mimikatz Modules (Each module is essentially a group of functions that are used to carry out a specific task)

1. **Crypto**: Manipulation of CryptoAPI Functions
2. **Kerberos**: "Golden Ticket" creation via MS Kerberos API
3. **Lsadump**: Handles manipulation of the SAM (Security Account Managers) database. This can be used against a live system or "offline" against backup hive copies.
    - Allows for access to password via LM Hash or NTLM
4. **Process**: Lists running processes (handy for pivots)
5. **Sekurlsa**: Handles extraction of data from LSASS (Local Security Authority Subsystem Service)
    - This includes tickets, pin codes, keys, and passwords
6. **Standard**: Main module of the tool. Handles basic commands and operation
7. **Token**: Context discovery and limited manipulation

## Reasons Mimikatz can be so dangerous:

1. Mimikatz supports both 64-bit and 32-bit x86 architectures with separate builds. 
2. The mimikatz DLL can be loaded reflexively into memory. 
3. When combined with PowerShell (Invoke-Mimikatz) the attack can be carried out without anything being written to disk. 

Resources: 
- https://resources.infosecinstitute.com/topic/mimikatz-walkthrough/
- https://www.sentinelone.com/cybersecurity-101/mimikatz/


## Starting Mimikatz

- As soon as you execute mimikatz you will want to run a couple of commands to make your life easier.

    1. **privilege::debug**
    - This command engsges the **SeDebugPrivilege** on Windows which will allow us to interact with processes owned by other accounts when we need to. 
    2. **log**
    - Typing this command will tell Mimikatz to save all output from your mimikatz session to a file. Obviously if we are doing a pentest or are trying to solve a CTF, we will want records of what we did/ a way to review all of our success offline if need be. 
    3. **sekurlsa::logonpasswords**
    - This command dumps the passwords (hashes unless using an older version of windows) of all currently logged in users.
    - This includes normal logins as well as RDP logins

**Question to ask: Why would you want only the logged on users?**
- Potential Answers:

**What types of password hashes can we expect to see after extraction?**
1. **AD Windows 2003**: NTLM is the only one available. 
2. **AD Windows Server 2008 (or later)**: NTLM and SHA1
3. **Windows 7**: WDigest (If this is the case you will see cleartext passwords alongside the password hashes)





