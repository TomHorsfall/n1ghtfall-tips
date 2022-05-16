# Data Exfiltration

When doing a CTF or Penetration Test, one talent that is extremely important to attain is figuring out **how to pull information from a target**

This might be because there is a file that has sensitive information, but you can't do anything with it on the remote system. 

Below are a few ways you can do go about doing this: 

1. Starting an FTP server on your attack machine and transferring the files to it
2. Starting an http server on the target machine and pulling them down to your attack machine (the target machine will have to have certain tools installed to do this)
3. Using your attack machine as an SMB server
4. SCP ( the attacker has to have SSHd running)
5. Netcat (Both the attacker and target machine will require this to be installed)
6. using /dev/tcp on your attack machine
    - 
