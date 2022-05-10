# Active Directory Attacks

<!-- 1. Pass The Hash
2. OverPass The Hash
3. Pass The Ticket
4. Distributed Component Object Model (DCOM)
5. AD Persistence
6. Service Account Attacks
7. Password Guessing (Without getting caught)
8. Golden Ticket
9. Silver Ticket
10.  -->

## Key Takeaways from this page:
1. What is LSASS? 
- What does it stand for?
- What does it store?
- What permissions must we have to access it?
- What does it store and why do we need it?
- What can be used to defend it?



## Cached Credential Storage and Retrieval and LSASS

- Microsoft's Implementation of Kerberos makes use of single sign-on which means passwords need to be stored somewhere in order to renew a TGT request. 
- In current versions of Windows these hashes are stored in the Local Security Authority Subsystem Service (LSASS)
- If an attacker gains access to these hashes we could crack them to obtain plaintext passwords OR reuse them to perform various activites (Pass the Hash *poke poke*)
- As an attacker, the only way to get access to the hashes stored in LSASS is if you are running as a local administrator. So before we can even run something like **mimikatz** to retrieve these hashes, the attacker must perform privilege escalation. 
- More info: https://en.wikipedia.org/wiki/Local_Security_Authority_Subsystem_Service 
- Attacking LSASS: https://attack.mitre.org/techniques/T1003/001/ 

## Mimikatz: Here comes the fun

And as the previous passage mentioned, what's one of the best tools to use to retrieve credentials once you have admin access? MIMKATZ!

Some resources to help you understand mimkatz:
- https://www.varonis.com/blog/what-is-mimikatz

Mimikatz is an open-source application that allows users to view and save authentication credentials like Kerberos tickets. The application is still being supported by it's creator Benjamin Delpy and works with the most recent versions of Windows. 
- Mimkatz is an essential tool in penetration testing and is very commonly used to find holes in AD security. 

Attacks that Mimikatz can carry out (It's honestly very scary how much it can do)

- QUICK REMINDER: Mimikatz is very dangerous BUT it DOES need to be ran as admin or else it will not work. 

1. **Pass-The-Hash**: In older versions of Windows, password data was stored in an NTLM hash. Attackers can leverage mimikatz to take that exact NTLM hash and pass it to a target computer to login. Attackers don't even need to crack the password. They just need the hash as it is (ONE OF MANY REASONS TO NOT USE NTLM AUTH)
2. **Pass-The-Ticket**: Oh fun now we've got to what it can do if the machine uses Kerberos. Mimikatz provieds functionality for a user to pass a kerberos ticket to another computer and login with that user's ticket. This is essentially the same as pass-the-hash but Kerberos-style. 
3. **Over-Pass The Hash (Pass the Key)**: Very similar to pass-the-hash but it uses a unique key to impersonate a user you can obtain from a domain controller. 
- More info: https://stealthbits.com/blog/how-to-detect-overpass-the-hash-attacks/ 
4. **Kerberos Golden Ticket**
5. **Kerberos Silver Ticket**
6. **Pass-the-Cache**





### Manual Ways of Attacking AD

## The klist command

This command can be used to display all cached Kerberos tickets for the current user. 

## Attacking Service Accounts (Aka KERBEROASTING)

Some things to remember as we dive into this topic:
1. When a user wants to access a resource hosted by an SPN the client requests a service ticket created by the DC. 
- The service ticket is then decrypted and validated by the Application Server
- **KEY TAKEAWAY**: THE SERVICE IS ABLE TO BE DECRYPTED AND VALIDATED BY THE APPLICATION SERVER ***BECAUSE IT IS ENCRYPTED THROUGH THE PASSWORD HASH OF THAT SERVICE ACCOUNT**

Ok, so why did I just yell at you in italics. 

I yelled because as it turns out, the DC will hand over tickets of SPNs without verifying that you (the super crazy good pentester logged in as someone else) has permissions to access the service hosted by any particular SPN. 

SO if you were being evil, you could guess some common SPN/ Service names using I don't know *shrug* an automated script that tries to collect tickets.

OK, so again, why did I yell in italics. 

***Because we can take those tickets (encrypted using the Service Account passwords), and try to decrypt them offline. If we succeed, we get passwords. And now you know what Kerberoasting is. ***

Bam, we may have access to service account logins. 

## So how can we attack the service accounts








## Pass The Hashm (PtH)

Important info to note about PtH: ***This technique only works against servers/ services using NTLM for authentication. This technique DOES NOT WORK against kerberos.***

Tools that can be used to perform PtH:

1. Metasploit
2. Passing-the-hash Toolkit
3. Impacket

Pass the Hash is typically carried out through the utilization of the SMB protocol (On port 445 typically FYI. SMB shares are typically turned on within an enterprise environment). In order for PtH to be successful we need to authenticate to this protocol with the hashed password of an admin user. 

The reason we need an admin user to Pass the Hash is because if we are exploiting this vulnerability through SMB, these exploits will attempt tpo authenticate to the $admin SMB share. (File and print dharing also need to be enabled for this to work)

When a user connects to the SMB share via PtH, the usage of the hash is actually not illicit in nature. What makes it illicit is that the attacker gained access to the hash in an illicit way. 



## Overpass the Hash

Unlike PtH, OPtH can be used to gain a full Kerberos Ticket (TGT) or service ticket which grants us access to another machine or serivce as that user. 

Steps: 
1. Compromise a workstation or server (so easy right?)
2. Run mimikatz (or any other tool that can list logonpasswords) - aka check for cached passwords
3. Take the hash from the last step and use the NTLM hash of an admin user to OPtH
    - Reminder: The main purpose of OPtH is to leverage an NTLM hash to create a Kerberos ticket. 
    - We want to avoid using NTLM authentication
    - To do this we can run the mimikatz command:
    ```bash
    sekurlsa::pth
    ```
    - What this does is create a new process in the context of whatever user we may be targeting
    - A full example command:
        ```bash
        sekurlsa::pth /user:admin /domain:bigbiz.com /ntlm:<hash value goes here> /run:<an executable of your choosing>
        ```



