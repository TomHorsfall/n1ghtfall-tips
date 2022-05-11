# PowerShell Execution Policy ByPass

One of the most frustrating things for me as a new user to PowerShell was learning to understand the different components of how to run a script. 

When working in PowerShell, there are a set of rules and restrictions that are in place to keep malicious users from running scripts. Luckily, they are usually not terribly difficult to bypass with the right know-how. 

## PowerShell Execution Policy

**So what is the PowerShell Execution Policy?**

- It is a policy that determines the type of PowerShell scripts can be run on a system. 
- By default, it is set to "Restricted" which essentially means "no scripts allowed"
- One interesting thing to note is that originally, this was never meant to be a **security** control. It was meant to be used as a safeguard so that admins wouldn't run scripts that would break their environments without proper warning

**Why do we want to bypass the PowerShell Execution Policy (as Attackers)?**

- I think this is a pretty obvious answer; because we want to be able to run enumeration scripts or possibly exploits that can help as gain higher level access to a system
- The other thing is that if we are able to use PowerShell, it has a number of really wonderful features that we as attackers can take advantage of. This includes:

1. PowerShell is native to Windows so understanding it will always come in handy if exploiting a Windows Machine
2. It can talk with the Windows API which can help us enumerate systems much easier
3. It can run commands without writing to disk (This is huge for sneaking past IDS/ IPS systems)
4. Able to avoid Anti-virus (Because PowerShell is native to windows, it can be hard for Anti-Virus to pick up on malicious powershell activity)
5. Typically whitelisted by most applications
6. Many exploit toolkits leverage powershell which makes it handy for attackers

**Viewing the Execution Policy**

It's pretty easy. Just run:

```powershell
Get-ExecutionPolicy
```
Now if you want to see the execution policy for various **scopes** you can run this command:

```powershell
Get-ExecutionPolicy -List
```

And you'll be able to see what execution policy is set for each different scope (To learn more about scopes, see below)

```powershell
        Scope ExecutionPolicy
        ----- ---------------
MachinePolicy       Undefined
   UserPolicy       Undefined
      Process       Undefined
  CurrentUser       Undefined
 LocalMachine    Unrestricted
 ```

 ## Types of Execution Policies:
 1. **Unrestricted** - Can run anything but will prompt a warning if running scripts and configuration files that are not from the local intranet zone
 2. **RemoteSigned** - Requires a digital signature form a trusted publisher on scripts and configuration files that are downloaded from the internet
 3. **Restricted** - This is the default execution policy for Windows Client Computers. 
    - Permits individual commands but not scripts
    - Prevents running of all script files inclduing formatting and configuration files. 
 4. **Bypass** - Nothing is blocked and there are no warnings or prompts
 5. **Default** - Whatever the default execution policy is (Restricted for Windows Clients, RemoteSigned for Windows Servers)
 6. **AllSigned** - All Scripts must be signed by a verified publisher. 
    - Prompts you before running scripts from publishers that havent been classifed yet.
    - Risks running signed but malicious scripts




## **Scopes**

https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_scopes?view=powershell-7.2

PowerShell protects access to variables, aliases, functions, and PowerShell drives by limiting where they can be read and changed. 

The scope rules are in place so that users do not inadvertently msake changes they didn't mean to make. 

For example:
- You may want to run a script that makes a change only for the current user
- If you run it in the wrong scope, you may make changes to other user's settings and cause issues

### **List of scopes:**
1. **MachinePolicy** - Set by a Group Policy for all users of the computer
2. **UserPolicy** - Set by a group policy for the user of the computer
3. **Process** - Only affects the current PowerShell session. 
    - This execution policy is saved in the powershell env variable:
        - $env:PSExecutionPolucyPreference
4. **CurrentUser**
    - Affects only the current user
        - Set in the HKEY_CURRENT_USER registry subkey
5. **LocalMachine** - Execution policy affects all users on the current computer. 
    - Stored in the HKEY_LOCAL_MACHINE registry subkey

## Setting the Execution Policy

You can change the execution policy byfor your current user by running the following:

```powershell
Set-ExecutionPolicy -ExecutionPolicy <policyname> -scope CurrentUser
```

**If you'd like to change the execution policy for the local computer, it requires adminsitrator access (on versions of Windows Vista and later)**







You can also see the **scope** of the execution policy for each context