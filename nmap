References for this document:
- https://nmap.org/book/synscan.html
- https://www.stationx.net/nmap-cheat-sheet/

nmap (short for Network Mapper) is a tool used to find open ports on servers across a network

The tool is one of the most common security tools utilized to find a way in to target machines

nmap comes with a variety of flags you can pass to it to a.) scan without setting off alarms b.) up the intensity or c.) diversify the type of scan to bypass firewalls
along with many other features

To perform a single simple nmap scan you can run a command like this:

nmap <ip address>

But this will only display information of the top 8000 ports or so when there might be something interesting lurking on higher port numbers

To do a port scan of all available ports on the machine you can run a command like this:

nmap <ip address> -p- 

or 

nmap <ip address> -p-65535


### Scanning Techniques ###

1. TCP Syn Scan: This type of scan is ran by default. When a computer sends a SYN packet in an attempt to open a connection, a SYN/ACK response indicates
an open TCP port whereas an RST response indicates a closed port. 
- If no response is received OR there is an ICMP unreachable error, this indicates a "filtered" state (aka it may be behind a firewall of some kind)
- The SYN scan is one of the most common scans you will see and it is also referred to as a "Stealth" scan. This is due to the fact that it never completes a TCP connection. 

A SYN Scan (Also called Half-Open Scan) can be ran using nmap via the flags -sS. Below is an example:

nmap -sS <ip address>

### When a SYN scan is performed 3 things happen (if a port is open):

1. The attacker sends a SYN packet to the target (Requesting a port connection)
2. The target responds with a SYN/ACK (It's open, go ahead)
3. Attacker sends a RST packet (No, forget it!)

### This is different than a normal TCP Handshake where:

1. The attackers sends a SYN packet to the target (Requesting a port connection)
2. The target responds with a SYN/ACK (It's open, go ahead)
3. Attacker sends an ACK packet which starts the connection

The issue with this is if you make a connection, you have to worry about clsing it which means negotiating with a FIN packet rather than SYN. This is not ideal
so rather than sending an ACK, nmap responds with a RST. (It needs to respond with a RST because if NOTHING is sent it will keep resending SYN/ACK packets)

### If the port is not open, it's very simple:

1. The attackers sends a SYN packet to the target (Requesting a port connection)
2. The target responds with a RST (port is closed) and thats the end of that

### Filtered ports are also easy to understand. Typically the steps are:

1. nmap sends a SYN packet to request a connection
2. Since nmap doesn't receive a response (firewall intercepted it, network is flaky, return packet is dropped) it sends a second SYN
- nmap will also consider it filtered if it receives certain types of error messages (see https://nmap.org/book/synscan.html for more details)

Questions to ask:

- So what does a normal TCP Handshake look like?
- When is a FIN packet used?

# TCP Connect Scan
- https://nmap.org/book/scan-methods-connect-scan.html

Can be run on nmap like so:

nmap -sT <ip address>

This scan is used if a user does not have RAW PACKET PRIVILEGES which is typical in a UNIX system. This separation exists because the NETWORK AND THE HARDWARE ARE
CONSIDERED TRUSTED because they are controlled by a select few adminsitrators. 

A TCP Connect Scan works a bit different than other scans. Rsther than using raw packets it asks the OS to call the "connect" system call. This is the same high-level
system call that web browsers, P2P clients, and most other network-enabled applications use to establish a connection. (This is a part of the Berkley Sockets API)

Rather than reading raw packets off the wire nmap uses this API to obtain status information on each connection attempt. 

This type of scan is not recommended for anyone trying to stealthily enumerate a target. Nmap has less control vover the high level "connect" call than with raw packets 
making it less efficient. 

The calls for connections also COMPLETES those connections which make it easily picked up by an IDS or it may land in the target machine's logs. 















