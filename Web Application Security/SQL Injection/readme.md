# SQL Injection Attacks

## What is a SQL Injection Attack?
- A SQL injection attack occurs when an application improperly handles input from a user, allowing the user to access tables of a databse on the backend that they should not have access to.
- SQL Injection can also be used to bypass password prompts by applications that have poorly built authentication mechanisms
- In this page we will go over various forms of SQL Injection and then discuss how application developers can mitigate SQL Injection attacks

## What are some other common dangers of SQL Injection Attacks?
1. Retrieving hidden data
2. Subverting Application Logic
3. UNION Attacks
4. Examining the database
5. Blind SQL Injection

## Learning How to Perform SQL Injection Quickly
- To learn about SQL Injection and to get yourself off the ground there are a few questions you can ask yourself to exploit a page as quickly as possible
1. What kind of DB language are they using (There are many SQL languages and figuring out which one is being used will aid you in properly exploiting it)
2. How is the query structured? (If you can see an error that contains the query, view how it is structured and write it out in a notepad document. Then adjust it until you believe it will provide the fucntionality you are looking for)
3. How many results are returned?
- This can be helpful when attempting to perform a UNION attack. A Union attack is when you not only retrieve information from the original targeted table but also another table that may exist in the database
    - For example, one default table that many SQL DBs have is the "user" table. So if you perform a Union attack you can have the DB pull both the original information as well as information about different users. 
4. What version is the Database?
- Gathering information on a target is always impportant. Versioning may tell you about bugs that affect it as well as any vulnerabilities that may exist for that version
5. Gather information about entire database. 
- The example below is something that can be ran against almost all DBs:
```bash
SELECT * FROM information_schema.tables
```
6. OK you can't see the results of what you are injecting, but is it vulnerable to blind SQL injection?

## PortSwigger SQLi CheatSheet
- https://portswigger.net/web-security/sql-injection/cheat-sheet


## How to Prevent SQLi
1. Using Parameterized Queries
- OK but what the hell does that mean?
    - 




