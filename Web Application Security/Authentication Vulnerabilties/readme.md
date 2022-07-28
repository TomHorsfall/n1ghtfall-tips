# Authentication Vulnerabilities

## What is Authentication and how is it different than Authorization?
- Authentication asks the question "Who is this person?" and authorization asks "Does this person have the permission to access certain files/ applications?'
    - Example: Two users can authentication to Azure Devops but only one of them is authorized to access all projects within the application. 


## What is Authentication?
- Authentication is the process of verifying the identity of a given user or client. 
- Authentication should take three factors into consideration:
    - Something you **know**, such as a password or the answer to a specific security question aka **knowledge factors**
    - Something you **have** aka a keycard or security token aka **posession factors**
    - Something you **are** or **do**. for example: biometrics OR patterns of behavior. These are called **ionherence factors**

## Most common vulnerabilities in Authentication
1. The Authentication mechanisms are weak and can be easily brute-forced
    - Does not use an account lockout feature
    - Does not enforce best-practice password policies
2. Poor coding allows for attackers to bypass authentication all together.
    - Does not validate input and Attackers can leverage SQL injection to bypass auth
    - Poor password reset functionality allowing an attacker to change the password
 
 
## Vulnerabilities in Password-based Login
1. Bruteforcing usernames: See if you can find the pattern of the username a company uses. Then you can extrapolate that to create other usernames.
2. Brute forcing Passwords: 
3. Username Enumeration: If the website is built poorly it might tell you that a username is correct at the login page. If a website does this, you can leverage it to test and see what usernames are correct which can then lead to figuring out the password for specific users. 
4. 
