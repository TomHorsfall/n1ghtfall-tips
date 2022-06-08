# Understanding Linux Privileges
Resources: 
- https://www.redhat.com/sysadmin/suid-sgid-sticky-bit
- https://www.hackingarticles.in/linux-privilege-escalation-using-suid-binaries/


In order to learn how to escalate privileges on a Linux system, it's important to first understand how Linux permissions work. 

## Groups, Users and the Read, Write, and Execute Privileges

### Users and Groups
In Linux/ Unix there are **Users** and **Groups**

**Users** Are obviously people and accounts that can access the file system
**Groups**: Are ways of organizing permissions based on roles of different users
- For example, you may have a "Docker" group for users who are Docker admins on a machine
    - Anyone in this group may have admin access to a certain set of files

The first thing to understand with learning linux privileges is that all files and folders within a Unix/ Linux system are given certain permissions. These include:
1. Read (r): A user or group can read the file or folder 
2. Write (w): A user or group can alter a file or folder
3. Execute (x): A user or group can execute (like run a script) a file or folder
    - A note on the execute privilege: When it comes to directories and the execute privilege. The execute privilege means you can access folders and files within that folder
4. Sticky Bit (t): 

## SUID Bit (Special User ID)
- A file with an SUID is always run in the context of the USER who owns the file
- This can be set for example if you need a particular file needs to run with elevated permissions but pnly for that file

## GUID (Special GROUP ID)
- The GUID is the same as the SUID but instead of run in the contect of the user ID it's run in the context of the group that owns the file
- 



```bash
drwxr-xr-x 2 kali kali 4096 Oct  6  2021 Alpha
```
