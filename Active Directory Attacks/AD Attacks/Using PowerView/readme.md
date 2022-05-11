# PowerView

Resources:
- https://powersploit.readthedocs.io/en/latest/Recon/

PowerView is a tool that was developed to help give pentesters situational awareness on Windows domains. 

The tool essentially acts as the "net.exe" command in windows but using purely PowerShell. 

PowerView has a collection of specifically created cmdlets that leverage the Windows API as well as the AD hooks to better understand the landscape of an AD environment.

Some things it can do:
1. User hunting functions that can identify where a user is logged into (Can be used to find out what they're doing/ ways to possibly trick them)
2. Can check which machines on the domain a user has local administrative access to (Useful for finding pivot targets)
3. A variety of functions that can be used to abuse domain trusts (aka finding out if one domain has access to another domain's resources)

To learn more about it directly you can go here: https://powersploit.readthedocs.io/en/latest/Recon/ 

