# Manually Enumerating a Windows Machine

When we gain access to a windows machine, typically we do not have admin access. This makes running tools like Mimikatz or other exploitation tools difficult. 

So if we have a low-leve user account, the goal is to find pieces of information that might help us in our journey to escalate to a higher privileged user or possibly move laterally to a user with similar privielges. 

The first thing to do when you log into a machine is run a few commands to find out:

1. Who you are in the context of this computer?
2. What permissions/ privileges do you have as that user?
    - This could mean looking at groups
3. What is the name of the computer you are on?
4. What ports are open/ listening on the computer?
    - For newbies this might be confusing. "I'm already in the computer. Why do I need to know what ports are open?" 
    - This is because sometimes there are applications hosted on the machine that you can use to your advantage
        - Examples:
            - SQL Databases
            - Services with elevated priviliges
            - Services that may give you clues as to what other tools are used in the environment
5. What is the OS?
    - Knowing about the Operating system is important for seeing what kinds of kernel exploits you might be able to run against it
6. 


## The whoami command

This command works on both windows and linux and can be used to determine who you are as a user:

```cmd
whoami
```

## The hostname command

The hostname command tells you the name of the computer you are currently on. 

## The systeminfo command

This is a great command for figuring out a TON of information about the machine you are logged into.

Some info this command gives ou:
1. The hostname
2. The OS name
3. Computer Model
4. Type of PC architecture (x64 or x32)
5. The hotfixes installed

This tool can be leveraged to gain info offline by running 

```cmd
systeminfo
``` 

And then running the "windows-priv-checker.py" tool against it (Google it, its a great tool)

## Open Ports and Network Configuration

Networking is one of the most useful knowledge bases to have when penetration testing. In order to pivot, it is almost essential to understand basic networking. 

A couple of command commands to know to run during enumeration are:

```cmd
ipconfig
```
 and

 ```cmd
 netstat -ano
 ```

 **Ipconfig** will tell you about the current network, the current IP of the machine you are on, 
