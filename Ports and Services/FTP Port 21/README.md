
# FTP runs on Port 21 ###

What is an FTP server?
- FTP stands for File Transfer Protocol and it is typically used by organizations to transfer files within or between organizations
- It can be connected to using netcat (nc), telnet, or the ftp command


Steps to determine if FTP is available:
1. Run nmap agains the IP and look for an open port on port 21
2. If it is open, attempt to connect to it via:
  a. ftp <ip address> 
  b. nc -v <ip address> 21
  c. telnet <ip address> 21
3. Using one of these 3 connections, you can determine the version of the FTP server

Once you have the version of FTP you can use a tool like searchsploit to search for vulnerabilities
- https://www.exploit-db.com/searchsploit

Example Command:
searchsploit ftp

Or you can use Exploit DB directly:
- https://www.exploit-db.com/

# Anonymous Login ###

FTP Servers are typically not configured to allow anonymous login BUT every so often somone will forcefully configure a server to allow this.

If this happens a person can connect to the ftp service using a command like so:

ftp <ip address>
USER: anonymous
PASS: anonymous



## Active vs Passive FTP Connections

Active FTP (FTP server connects back to client):
1. Client opens connection (Port N) to FTP server on Port 21
2. Client tells server what port the client will listen on (N+1)
3. From port 20 on the FTP server, the server connects back to the client on port N+1
4. Data transfer happens
5. Connection closes

### Active FTP: 
a. The FTP client first initates the control connection from its port N to FTP servers command port 21
b. The client then listens to port N+1 and sends the port N+1 to FTP server.
c. FTP Server then initiates the data connection, from its port M to the port N+1

### Passive FTP:
a. Client initiates the control connection from its port N to the port 21 of FTP server. 
b. The client issues a passv command
c. The server then sends the client one of its port number M
d. Client initiates the data connection from its port P to port M of the FTP server

### Why is Passive Mode Dangerous?? ###

Passive mode is dangerous because this can allow an FTP Bounce Attack
FTP Bounce Attack: Using an intermediary FTP server to transfer files from a target server somewhere else. 

Steps for an FTP Bpunce Attack:
1. Open a connection to a vulnerable intermediary FTP server
2. Issue a PORT command on the vulnerable server and ask the server to open a data connection to Port M and speciofy the IP address of the target server.
3. Send the intermediary server a file of FTP commands to execute that target the target server
The file may have these set of instructions:
- Open an FTP connection to target.com
- Middle man server uses passive mode, so it must send a port number to which target/com shpuld open a data connection. Middle mand.com specifies that with a port command but instead of 
giving the IP address of middle mand.com it sepcficfies the IP address pf the attacker machine
- Transefer the required file over the connection thus establushed



Types of Attacks that can be leveraged againt FTP:
1. File inclusion (uploading a file that can be uploaded to a publicly accessible location)
2. FTP Bounce Attack (Connect Client <-> FTP server <-> Target Server)
  - https://www.thesecuritybuddy.com/vulnerabilities/what-is-ftp-bounce-attack/
  - https://book.hacktricks.xyz/pentesting/pentesting-ftp/ftp-bounce-attack
3. 


Other options:
1. Use hydra to brute force FTP
  a. https://infosecwriteups.com/beginner-guide-on-attacking-and-defending-ftp-server-part-1-2-635d5373adf1
  b. https://linuxhint.com/bruteforce_ssh_ftp/
  c. https://book.hacktricks.xyz/pentesting/pentesting-ftp/ftp-bounce-attack
  d. A good list of default FTP creds: https://github.com/danielmiessler/SecLists/blob/master/Passwords/Default-Credentials/ftp-betterdefaultpasslist.txt
