# Active Directory Enumeration

Table of Contents:
1. [net.exe command](#using-the-"net"-user-command)
2. [Get-ADUser CMDlet](#get-aduser-cmdlet)
3. 

## Using the "net" user command

The "net" command is one of the easiest and most common ways for an attacker to learn more about an AD environment. 

Running "net" along with multiple commands can tell you A TON about an AD environment. 

### Some of the big ones:
```bash
1. net user - Info about local users
2. net user <username> - More detilaed info about a local user
3. net localgroup - Groups on the local machine
4. net user /domain - All users in the domain
5. net user <username> /domain - More information about a user on the domain
6. net localgroup /domain - All groups in the domain
7. net group /domain - All groups on the domain (same as above)
```

## Limitations of the "net.exe" command:
1. Oftentimes groups within AD are "nested" aka some groups exist within other groups
    - Example: 
        - If there is a "users" group and all users require RDP access they may also all be in the "Remote Desktop Group"
        - This is a bad example but it just means that one group is inside another group
2. The net.exe command may work well for smaller implementations but there are other tools developed and built specifically to help enumerate an AD environment

## Get-ADUser Cmdlet

If you are unfamiliar with powershell, PS is a scripting tool created by Windows for Windows to help automate certain tasks. If it can be built to help windows admins, it can also be used to hurt them. 

One cool feature of PS are CMDlets which are essentially built in functions that allow you as an attacker to query information (as well as many other things)

It's basically a souped up command line. 

Anyways, the "Get-ADUser" cmdlet can provide a lot of interesting information if it is enabled. 

if you run the command like so (and it is enabled) you can be surprised by how much information you might be able to get back:
```cmd
Get-ADUser <username>
```

More info on this cmdlet can be found here:
- https://docs.microsoft.com/en-us/powershell/module/activedirectory/get-aduser?view=windowsserver2022-ps
- https://github.com/S1ckB0y1337/Active-Directory-Exploitation-Cheat-Sheet#using-ad-module 


## Using Direct LDAP Paths 

Another way to query information from a domain controller is by using the **DirectorySearcher** object.

For anyone not familiar with LDAP (Lightweight Directory Access Protocol), it is a protocl used by Domain Controllers to access objects/ search for information. 

LDAP is basically an API that supports search functionality against a DC. 


### What is an LDAP Provider Path


