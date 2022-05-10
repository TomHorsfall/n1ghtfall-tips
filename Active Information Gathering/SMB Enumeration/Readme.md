# Table of Contents

1. SMB Overview
2. NetBIOS Overview
3. Tools for Enumeration



# SMB Enumeration

SMB (Server Message Block) is a protocol very commonly used in enterprise environments to share files across a network. 

SMB is what is responsible for allowing users to have "shared drives."

The issue with SMB is sometimes it is poorly configured and other times, it can be used as a vector to attack a system. 

# Understanding NetBIOS

A service that goes hand in hand with SMB is the NetBIOS service. 

**NetBIOS** listens on port **139** (as well as a few other UDP ports) and is what allows computers on a local network to communicate with each other. (NetBIOS stands for **Network Basic Inout Output System**)

While modern implementations of SMB can work without NetBIOS,**NetBIOS over TCP is required for backward compatibility** and is often enabled together. 

NetBIOS Provides 3 Services:
1. Name Service (NetBIOS-NS) for name registration and resolution
2. Datagram distribution service (NetBIOS-DGM) for connectionless communication
3. Session service (NetBIOS-SSN) for connection oriented communication 

## SMB and NetBIOS are Different Protocols

- SMB on port 445 and NetBIOS on port 139 are separate protocols but are often scannned together. 
- NetBIOS allows computers on a network to communicate with one another
- SMB can do the same thing but NetBIOS has been used in older machines and so NetBIOS over TCP (NBT) was created so that newer and older computers could still communicate. 
- This is why you will often see SMB and NetBIOS clumped together in examples. 



## Tools for SMB and NetBIOS Enumeration

1. nmap (Don't forget about NSE Scripts!)
2. nbtscan
3. smbmap


Nmap is often used to search for these services 

```bash
nmap <ip address> -p 139,445
```

