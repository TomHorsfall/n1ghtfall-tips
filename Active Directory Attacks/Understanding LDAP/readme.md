# Understanding LDAP Lightweight Directory Access Protocol


## What is LDAP?
- LDAP is a protocol used to access Active Directory
    - Active Direcotry: A program that directory structure that is used to assign permissions to various users and groups throughput an organization
- When enumerating a network, it may be important to understand the basics of LDAP and how to query for pieces of information hidden within AD


## Using Direct LDAP Paths 

Another way to query information from a domain controller is by using the **DirectorySearcher** object.

For anyone not familiar with LDAP (Lightweight Directory Access Protocol), it is a protocl used by Domain Controllers to access objects/ search for information. 

LDAP is basically an API that supports search functionality against a DC. 