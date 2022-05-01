# NMAP Tips and Tricks/ Strategies/ and Port Scan Explanations


References for this document:
- https://nmap.org/book/synscan.html
- https://www.stationx.net/nmap-cheat-sheet/

nmap (short for Network Mapper) is a tool used to find open ports on servers across a network

The tool is one of the most common security tools utilized to find a way in to target machines

nmap comes with a variety of flags you can pass to it to a.) scan without setting off alarms b.) up the intensity or c.) diversify the type of scan to bypass firewalls
along with many other features

To perform a single simple nmap scan you can run a command like this:
```bash
nmap <ip address>
```
But this will only display information of the top 8000 ports or so when there might be something interesting lurking on higher port numbers

To do a port scan of all available ports on the machine you can run a command like this:

```bash
nmap <ip address> -p- 
```
or 
```bash
nmap <ip address> -p-65535
```

# Scanning Techniques ###

## 1. TCP Syn Scan: This type of scan is ran by default. When a computer sends a SYN packet in an attempt to open a connection, a SYN/ACK response indicates
## an open TCP port whereas an RST response indicates a closed port. 
- If no response is received OR there is an ICMP unreachable error, this indicates a "filtered" state (aka it may be behind a firewall of some kind)
- The SYN scan is one of the most common scans you will see and it is also referred to as a "Stealth" scan. This is due to the fact that it never completes a TCP connection. 

A SYN Scan (Also called Half-Open Scan) can be ran using nmap via the flags -sS. Below is an example:
```bash
nmap -sS <ip address>
```
## When a SYN scan is performed 3 things happen (if a port is open):

1. The attacker sends a SYN packet to the target (Requesting a port connection)
2. The target responds with a SYN/ACK (It's open, go ahead)
3. Attacker sends a RST packet (No, forget it!)

## This is different than a normal TCP Handshake where:

1. The attackers sends a SYN packet to the target (Requesting a port connection)
2. The target responds with a SYN/ACK (It's open, go ahead)
3. Attacker sends an ACK packet which starts the connection

The issue with this is if you make a connection, you have to worry about clsing it which means negotiating with a FIN packet rather than SYN. This is not ideal
so rather than sending an ACK, nmap responds with a RST. (It needs to respond with a RST because if NOTHING is sent it will keep resending SYN/ACK packets)

## If the port is not open, it's very simple:

1. The attackers sends a SYN packet to the target (Requesting a port connection)
2. The target responds with a RST (port is closed) and thats the end of that

## Filtered ports are also easy to understand. Typically the steps are:

1. nmap sends a SYN packet to request a connection
2. Since nmap doesn't receive a response (firewall intercepted it, network is flaky, return packet is dropped) it sends a second SYN
- nmap will also consider it filtered if it receives certain types of error messages (see https://nmap.org/book/synscan.html for more details)

Questions to ask:

- So what does a normal TCP Handshake look like?
- When is a FIN packet used?

# 2. TCP Connect Scan
- https://nmap.org/book/scan-methods-connect-scan.html

Can be run on nmap like so:
```bash
nmap -sT <ip address>
```
This scan is used if a user does not have RAW PACKET PRIVILEGES which is typical in a UNIX system. This separation exists because the NETWORK AND THE HARDWARE ARE
CONSIDERED TRUSTED because they are controlled by a select few adminsitrators. 

A TCP Connect Scan works a bit different than other scans. Rather than using raw packets it asks the OS to call the "connect" system call. This is the same high-level
system call that web browsers, P2P clients, and most other network-enabled applications use to establish a connection. (This is a part of the Berkley Sockets API)

Rather than reading raw packets off the wire nmap uses this API to obtain status information on each connection attempt. 

This type of scan is not recommended for anyone trying to stealthily enumerate a target. Nmap has less control over the high level "connect" call than with raw packets 
making it less efficient. 

The calls for connections also COMPLETES those connections which make it easily picked up by an IDS or it may land in the target machine's logs. 

## Steps of a TCP Connect Scan:

1. Client sends SYN (Request port connection)
2. Server sends SYN/ACK (Tells client the port is open)
3. Client sends an ACK (Connection Established)
4. Data is sent from server to client (For example: the SSH banner)
5. RST is sent to server (Kill connection)


## 3. UDP Scan
- https://nmap.org/book/scan-methods-udp-scan.html
Running an nmap UDP Scan looks like this:
```bash
nmap -sU <ip address>
```
**UDP** Stands for **User Datagram Protocol** and unlike TCP (Transmission Control Protocol), this protocol is connectionless. For example, some UDP protocols are DNS (port 53), SNMP (Port 161), DHCP (port 162). UDP scanning is generally slower and more difficult than TCP so sometimes security auditors ignore these ports. DO NOT IGNORE THESE PORTS. I once was working on a CTF and spent more than 2 hours looking into various open ports ony to realize I hadn't scanned UDP ports and thats where the attack vector was living. 

As an FYI you are able to run both a TCP scan alongside a UDP scan to hit both protocols at the same time. 

Example: 
```bash
nmap -sU -sS <ip address>
```

UDP Scanning is different than TCP scannign in that a UDP scan works by sending a UDP packet to every targeted port. For most ports, this packet will be empty (no payload) but for a few of the more common ports a protocol-specific payload will be sent. 

Based on the response (or lack thereof) the port is assigned to one of four states. 

![Screenshot](1udp-responses.png)

### Biggest challenges with UDP scans are that open ports rarely respond to empty probes. 
- The ports probed where nmap has prtocol specific payloads are more likely to get a response and be marked open
- Otherwise messages are usually passed up the TCP/IP stack to the listening application which usually discards it immediately as invalid. 
- When nmap receives no response after several attempts it cannot determine whether the port is open or filtered. 
- Every UDP protocol is slightly different and requires different pieces of information which is why it can be difficult to figure out if a port is open or not. 

When version scannings is enabled (using is -sV flag or the -A flag) it will send UDP probes to every open/filtered port. If any of the probes elicit a response from an open/filtered port that state is changed to open. 

For more information on UDP NMAP Scans go to: https://nmap.org/book/scan-methods-udp-scan.html

## 4. TCP FIN (-sF) , NULL (-sN), and Xmas (-sX) Scans

Resources: 
- https://nmap.org/book/scan-methods-null-fin-xmas-scan.html

One loophole to the TCP protocol is that if a destination port is CLOSED, any packet that is sent to it without a RST flag set will receive a RST flag in response. 

It also says that any packets sent to OPEN ports without the SYN, RST, or ACk bits set will return a RST if the port is closed and no response at all if the port is open. 

What this means is if we choose to exclude any of those three bits within an nmap scan, we should be able to determine what ports are opened or closed using this logic. Nmap created 3 scans for this including:

1. Null Scan (-sN)
```bash
nmap -sN <ip address>
```
- Does not set any buts (TCP flag header is 0)

2. FIN Scan (-sF)
```bash
nmap -sF <ip address>
```
-Just sets the FIN bit

3. Xmas Scan (-sX)
```bash
nmap -sX <ip address>
```














