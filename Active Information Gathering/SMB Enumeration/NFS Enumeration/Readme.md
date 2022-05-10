# Network File System (NFS)

Resources:
- https://linuxhint.com/nfs-ports/

- NFS is a file system protocl that allows a cleitn computer to access files over a computer network as if the were on locally-mounted storage
- NFS is most commonly used in **Unix** systems and is commonly misconfigured
- It is commonly abused by attackers to gain information on a system, escalate privielges, etc.
- Think about NFS as the equivalent of the SMB protocol on Windows machines

## Services Required for NFS to work:

1. Portmapper
2. Mountd
3. nfsd
4. lockd
5. Statd

### Portmapper (Port 111)
- The portmapper service will keep track of what functions and services are sitting on what ports and route connections appropriately
- So if someone is trying to run a Remote Procedure Call (RPC) this service will be used to say "Hey! you want to run X? Well that service is sitting on this port!"
 - More info: https://tldp.org/HOWTO/NIS-HOWTO/portmapper.html

 ### Mountd 
- The mmountd daemon is an RPC that answers a client request to mount a filesystem. 
- The mountd daemone finds out which file systems are available by reacing the 

