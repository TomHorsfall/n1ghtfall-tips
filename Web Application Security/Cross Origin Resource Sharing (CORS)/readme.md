# Cross Origin Resource Sharing (CORS)

- CORS is a broswer mechanism which enables controlled access to resources located outside of a given domain
- It extends and adds felxibility to the Same-Origin Polic (SOP)
- If a CORS policy is poorly confiugred it can lead to detrimental attacks. 

## What is the Same-Origin Policy?
- The SOP is a web browser security mechanism that precents websites from attacking each other
- It restrcits scripts on one origin from accessing data from another origin. 
- An origin consists of:
    1. A URI scheme (http or https)
    2. A domain (ex: google.com)
    3. A port number (http=80, 443=https)
- The SOP controls the access that JS has to content that is loaded cross-domain
- Cross-origin loading of pages is generally permittied (for example, if you have a bunch of images stored in AWS, you might have them stored in AWS but show up on your website)
- 

# What is the HttpOnly Cookie Flag?
- The HttpOnly Flag is used to prevent client side scripts from accessing the cookie
- This will inherently block XSS attacks from happening even if a user clicks on a malicious link
- One issue to remember is that if a browser is out of date/ does not support the HttpOnly flag, it will not protect the user
- https://owasp.org/www-community/HttpOnly


