# Using Searchsploit

Resources: 
- https://www.hackingarticles.in/comprehensive-guide-on-searchsploit/

Searchsploit is a command line search tool for Exploit-DB that also allows you to take a copy of Exploit Database with you, everywhere you go.

SearchSploit gives you the power to perform detailed offline searches through your locally checked-out copy of the repository. This capability is particularly useful for security assessments on segregated or air-gapped networks without Internet access.

## Searching just the title

Let's say you know the name of an exploit and would like to return results that only will have that name. This is when you can use the "-t" option:

```bash
searchsploit -t Samba
```