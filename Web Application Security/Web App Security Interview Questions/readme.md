# Web Application Security Interview Questions



1. What is an HTTP Header?
 - How can it be exploited?
2. What is CSP (Content Security Policy)?
 - CSP is used to detect and mitigate certain types of attacks including XSS and data injection attacks.
 - https://www.imperva.com/learn/application-security/content-security-policy-csp-header/
 - You can deisgnate that only certain sites can execute scripts and disallow inline scripts
 - This keeps other sites from executing on your site (if there is a xss vuln in the site)
 - It is a header that can be set to allow only absolutely necessary sites to run scripts
 - 
3. What is a Vulnerabnility?
- A weakness in a system through whicvh intruders or bugs can attack

4. Name all types of XSS and how they are different. 
- Reflected: XSS comes from the url and is reflected back onto the user
- DOM Based: There is unsafe javascript in the site that access the DOM which can be leveraged to attack the suer
- Stored: Malicious script or commands are sotred in the database so everytime the site opens up, it runs in the user's browser. 

5. What is CORS?
- A request for a resouece (ike an image or type of font) outside fo the origin is known as a *cross-origin request*
- Content-Security-Policy prevents calls to external resources and Cross-Origin-Resource-Sharing prevents calls from external sources. To provide an example. For abc.com to show def.net in an iframe, abc.com must not block def.net with its CSP settings and def.net must not block abc.com with its CORS settings.

6. What are your favorite tools to use when doing Web App Pentesting?
- Burpsuite
- OWASP ZAP
- HCL AppScan
- Tenable Web Application Scanner
- Dirb, dirbuster
- Nikto (to analyze web servers)
- nmap HTTP NSE Scripts
- Searchsploit (used to find vulns against specific web app frameworks)
- 





7. What are some projects you've worked on recently?
- Built the RFP App
- Worked on a containerzied python app that would be used to help streamline the CyberArk account creation process
- Created a script to go to different sites and pull information for IP lookups
- Built a script in python that turned on a proxy, crawled a website through that proxy, and then downloaded the file that kept track of its traffic
- Building a portfolio site for myself using Flask

8. What is session hijacking? Name some ways an attacker can achieve this. 
- Session hijacking is when an attacker is able to successfully steal a cookie or session token from another user and then use that to access information on a site that they should not have access to. 
- Because HTTP is a *stateless* protocol there needs to be ways for websites to keept rack of when someone is logged in. Typically that is with a session token stored in a cookie. 
- If an attacker is able to get their hands on this cookie, they can inject it into their own session and then act as that user. 
- This can happen if the session key is easily guessable or if it is stolen by way of another vulnerability (like XSS)
- How can this be mitigated:
    - Secure session token creation is extrmeley important. Making sure that the tokens gneerated are randomized and difficult to guess. 
    - Also making sure that there are not toehr vulnerabilites in the site where this token could be stolen.

9. What is SQL Injection and how can it be prevented?
- SQL Injection is an attack on the backend database used by a website
- When executed, this could allow the attacker to gain information on the system that they shouldn't have access to OR even sometimes allowing for remote code execution
- SQL Injection can be mitigated a number of different ways:
    - Prepared Statements with Paramterized Queries:
    - Use Stored Procedures: Pre built SQL calls that don't take external input
    - Escaping All user Supplied Input: Might be disallowing quotations or other punctuations commonly used in SQL calls
    - Enforcing Least Privelege: Make sure the account the website uses to access the database has limite rights in the event of attack. 

10. What is Cross Site Request Forgery? How can it be mitigated?
- This is when an attacker might leverage a vulnerable site to make a request to another site that is open in a user's browser. 
- Can be mitigated by including a nonce in all forms called a CSRF token which is randomly generated for each user session. If the token does not match or is not included when the form is submitted, the request will fail. 
    - https://www.synopsys.com/glossary/what-is-csrf.html#:~:text=A%20CSRF%20token%20is%20a,token%20for%20every%20user%20session.
- 

How does DNS work?
1. Request is submitted
2. Computer looks in local DNS cache to try to retrieve IP for site
3. If not found it goes to the ISP Recursive DNS Server
4. Uses DNS root server to find any sites with ".com" (or whatever your site's root is)
5. Looks for another server for the actual name (The domain name)
6. Goes to an authoritative DNS server where it provides the IP Address
- https://phoenixnap.com/kb/what-is-domain-name-system-works


11. What is HTTP Request Smuggling?
- Attacks the content-length-header and the *Transfer-Encoding* header
- 

12. What is a file inclusion vulnerability?
- This is where a website does not validate the uploaded files which may allow an attacker to upload a script that will give them remote access to the machine
- There are two types:
    - Local File Inclusion: Allows an attacker to read (and sometimes execute) files on the victim machine.
    - Remote File Inclusion: Being able to execute code from the attackers machine on the remote server
        - You can do this be referencing the url of a page you control in the url of the vulnerable application



13. How to exploit password reset vulnerabilities?

14. How to exploit URL redirects?

15. How can you tell the difference between an app that uses NTLM and regular authentication?

16. 




