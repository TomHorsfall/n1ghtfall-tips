# Cross Site Request Forgery (CSRF)

## What is it?
- Cross Site Request Forgery is an attack that forces a user to make a request to a site or application that they did not intend to do
- CSRF can be quite difficult to pull off and requires a number of factors to be true in order to work. 

## What conditions must exist for CSRF to occur?

1. **A Relevant Target Action**: This is the action the attacker wishes to induce. This could be an action that only specifc users can perform (like changing their password, or transferring money from one account to another.)
2. **Cookie-based session handling**: Performing the action involves issuing one or more HTTP requests and the aplication relies solely on session cookies to idenitfy the user who has made the requests. 
3. **Predictable Request Parameters**: The targeted requests that are performed must have a predictable set of parameters that the attacker will be able to determine. For example, an application that requires the user's password in order to a password rest would not be vulnerable to CSRF since the attacker might not know the password of the user they are targeting. 
- Technically it can happen if there are unkown paramters involved but in those cases the requests automatically inject credentials which still allow the atack to happen
- *Note*: Session tokesn can be implemented in the cookie or within a separate header. It is best practice not to put sessions in the URL as this information is logged and this increasese risk of exposure. 
- Notes on best practices for session management: https://www.packetlabs.net/posts/session-management/ 


## How is this exploited?
- For an attacker to exploit this, they will need to create a new webpage with a form that submits a request to the vulnerable web application.
- When the user clicks on the malicious link, the form that targets the vulnerable application will be submitted, and they'll have made a request on that pager without their knolwedge. 


