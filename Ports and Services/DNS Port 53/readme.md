# DNS on Port 53

DNS stands for Domain Naming System and the purpose of DNS is to translate a human readable name (like google.com) back to it's IP address
- We humans are horrible at remembering IP addresses, but remembering that our favorite website is theonion.com is much easier for us to grasp.
- To make it easier for humans to traverse the web, DNS was created 

## Enumerating DNS

There are a few different ways to enumerate DNS

An easy way to do it is using any of the available nmap scripts:

```bash
broadcast-dns-service-discovery.nse
dns-blacklist.nse
dns-brute.nse
dns-cache-snoop.nse
dns-check-zone.nse
dns-client-subnet-scan.nse
dns-fuzz.nse
dns-ip6-arpa-scan.nse
dns-nsec3-enum.nse
dns-nsec-enum.nse
dns-nsid.nse
dns-random-srcport.nse
dns-random-txid.nse
dns-recursion.nse
dns-service-discovery.nse
dns-srv-enum.nse
dns-update.nse
dns-zeustracker.nse
dns-zone-transfer.nse
```

Quick tip: I created a bash alias on my kali machine that lists all nmap scripts and then I grep for a keyword within those scripts to return all of these. The alias looks like so:

```bash
alias lsnse='ls /usr/share/nmap/scripts |  grep'
```

So then you could run:

```bash
lsnse dns
```

And it would give you the output from above


