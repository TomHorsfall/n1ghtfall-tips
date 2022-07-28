# OS Command Injection

## What is OS Command Injection?

- OS Command injection is one of the most dangerous web vulnerabilities out there as the vulnerability will allow attackers to run OS level commands remotely.
- For anyone who is newbie, what this means is that you could send a simple request to a website, pass along some nefarious paramters and possible find out things like:
    - The contents of the "/etc/passwd" file on linux
    - Run a command the connects back as a reverse shell to the attacker's machine
    - View the network structure by running a command like "ifconfig" "ipconfig"


## What to look for to identify OS Command Vulnerabilities

1. To exploit OS Command Injection vulnerabilities means that the application is not properly santiizing input. So look for all areas where you may supply input and then either manually or in some automated fashion, fuzz the input with values that might allow for command injection (Send commands like "whoami" along with logical operators (& | ping `` etc.))
2. Try to determine the type of OS the application is running on. This will determine what types of commands you can run
3. 

## Blind OS Command Inhjections

- In many cases the application won't print the output of your attack to the website you are attacking. So to get clarification on if your attack works or not, you have to find some other ways to validate that the application is vulnerable
Here are some possible ways to do this:
1. Using Time Delays
2. Redirect the output of a command to a file, then read that file (must string commands together)
3. Having the OS interact with an Out of Band machine that you control
