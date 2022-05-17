# Understanding Windows Privileges

Privileges: The permissions granted to an account that allows them to make changes to the system. Changes can include:
- Modifying the filesystem
- Adding Users
- Shutting down the system
 
## Tokens
 
- The Windows OS uses objects called **access tokens**
- When a user is authenticated Windows generates an access token that is assigned to that user.
- The token itself contains various pieces of information that describe the security context and permissions of a given user
- Tokens are unique and an **SID (Security Identifier)** is created for this reason          
    - SIDs are assigned to both user and group accounts

## The Windows Integrity Mechanism

- Windows assigns **integrity levels** to application processes and secureable objects
- These levels describe the **trust** the OS has in running applications or objects
    - Example: The integrity level of an application may allow it to read from a certain file but never to write to it.
- APIs can be blocked from specific integrity levels (which can make it hard for pentesters to run certain tools)

Windows Integrity Levels for modern Windows Machines (as of 2022):

1. **System Integrity Process: System Rights** – Can do anything it wants
2. **High Integrity Process: Administrative rights** – Same rights as SYSTEM but Administrative rights is tied to a user account with a password where SYSTEM is a service account
3. **Medium Integrity Process: User Rights** - All regular users have these rights
4. **Low Integrity Process: Very restricted rights often used in sandboxed processes**
 

## UAC – User Account Control

What is UAC?

- UAC is an Access Control system created by MS
- UAC was not built as a security mechanism but as a means of getting admin approval prior to running certain programs
- The goal is to alert system admins of changes that users would like to make so that they are reviewed prior to making changes
- This can be bypassed with the correct know-how
    - Example:
        - This is what happens if you have ever worked in an office and attempted to download a program to your work machine. It will says something to the effect of “You need admin access to download this program” and then prompt you for a username and password
        - If you are an admin on a computer on an enterprise network, you will also receive a prompt but typically you will only receive a consent prompt asking you if you are sure you want to download that program
        
## UAC and the Windows Integrity Mechanism: Mixing them Together
 
So if we are prompted for an admin credential when installing a program what is interesting is that in that scenario we would then be running at two different integrity levels.

- One at the Medium Integrity Level: Our Normal User Profile
- One at a High Integrity Level: The Admin Credential Profile
    - This can be checked by using the whoami /groups command on Windows