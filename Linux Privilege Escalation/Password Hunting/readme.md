# Linux Privilege Escalation – Strategies for Finding Stored Passwords

Resources:

https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Linux%20-%20Privilege%20Escalation.md#looting-for-passwords
 

1. The “history” Command
2. Leveraging the sudo command/ privileges
3. The “find” command
4. Leveraging grep
5. Automated linux privilege escalation tools:
    - Linepeas.sh
    - LinEnum.sh
6. Insecure File Permissions (Viewing /etc/passwd + /etc/shadow)
7. Common config files
8. Escalation via SSH Keys

## The History Command:

Running the history command will give us a detailed list of commands that were previously run by the user who you have compromised.

 

Reasons this is helpful:

1. Users sometimes enter credentials into the command line to access a database or some other type of system
2. This will tell you what other file locations the user typically travels to which may lead to privileged information
3. Tips on what kinds of commands are available to you as an attacker
 

## Hunting for SSH Keys


Public Key

Private Key


Public Key would be copied to an SSH server. That’s how it knows how to identify us as who we are

The public key would be stored in the “Authorized Keys” folder


User keeps the identification key

Do we have an ID_rsa on the compromised host?

Is there a backup
If so, is it utilized somewhere?
Id_rsa is a secret key