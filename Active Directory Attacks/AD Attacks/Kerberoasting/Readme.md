# Kerberoasting: An Attacker's Toolset for Stealing and Cracking Passwords

## What is kerberoasting?

Kerberoasting is the act of exploiting the pitfalls of the Kerberos authentication protocol to steal Kerberos tickets and crack them offline. 

Kerberos tickets can be requested by any domain user, regardless of their permissions.

Each of these tickets are encrypted using the **hashed password of the service account behind an Service Principal Name**

So if an attacket enumerates a system for SPNs and requests tickets for them, they can bring this offline and use a cracking tool to get their passwords, thus giving them access to certain service accounts. 

Some Resources I used during the creation of this page:
- https://github.com/nidem/kerberoast
- https://www.netspi.com/blog/technical/network-penetration-testing/15-ways-to-bypass-the-powershell-execution-policy/ 


## First things first: We have to get Kerberos tickets to crack

As a quick reminder, Kerberos is a ticket system that provides tickets to users so that they can access services across a network. 


