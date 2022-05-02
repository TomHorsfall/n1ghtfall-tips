# Netcat - The Swiss Army Knife of Network Connections

Definition of what netcat does: A utility which reads and writes data across network connections using TCP or UDP protocols

### Connecting to a TCP or UDP Port

Netcat is an incredible tool used by penetration testers largely because of its ease of use, combined with it's ability to open shells or reverse shells to target machines. 

The tool also allows us to:
1. Connect to a network service manually
2. Check if a port is open
3. Determine the versioning of a service by grabbing its banner

To run a netcat command against a remote host,. all that is needed is:
1. The IP of the machine you are testing
2. The port on which you want to test
3. (Optional) Flags that can be passed to netcat for various additional functionalities. 

An Example:

```bash
nc <ip address> <port>

nc 10.10.10.10 22
```

Some additional information on what netcat can do can be found here:
- https://www.varonis.com/blog/netcat-commands
- https://www.ionos.com/digitalguide/server/tools/netcat/

### LISTENING on a TCP/ UDP Port

One great thing about netcat is that the tool allows you to run netcat as a SERVER (listening for a connection) or a CLIENT (Trying to connect to a remote host). 

In penetration testing, it is common to try to get a remote machine to connect BACK to the machine you are working from. This is because there are often INGRESS firewall rules (Ingress= information coming into a system, EGRESS= Information going OUT of a system) in place that say "Disallow any incoming connections" BUT firewalls typically have no issue with allowing OUTGOING connections as computers are obviously being used to retrieve information from out on the web. 

This makes netcat a handy tool for tricking a user or a program on a computer to send a netcat connection to your machine, where you have set up a netcat listener to open a command shell (if this doesn't make sense, keep reading. It will eventually make sense).

To listen on your local machine with netcat we can run the following (pay attent to the -l flag as that is the flag that tells the computer to listen on a specific port)

```bash
nc -lnvp 4444
```
In this instance the flags each have their own meaning:

- -n : Disable DNS resolution (aka use an IP address as an address instead of a domain name)
- -l : Listen
- -v : Verbose output
- -p : Local port to listen on

In this case the local machine is now listening for connections on port 4444. 

### Transferring files with Netcat

One cool additional functionality of netcat is that we can transfer files with it. 

An example to try out if you have two machines:

1. Run this on your local machine
```bash
nc -nlvp 4444 > bringit.txt
```
2. Run this on your remote machine:
```bash
nc -nv <IP of local machine> 4444 < <filename>
```

At the end of this the file you chose should have transeferred to your local machine. Depending on the sizr, it might take a while. but this is a good technique to use when trying to pull information down from a remote machine that happens to have netcat installed. 




