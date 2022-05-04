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





