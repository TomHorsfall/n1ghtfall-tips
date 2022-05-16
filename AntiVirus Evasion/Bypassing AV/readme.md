# Bypassing AV: On-Disk and In-Memory Evasion Tactics

Most modern malware employs in-memory operations as this is harder to detect (it leaves no trace on the hard drive)

Despite this, on-disk evasion techniques are still improtant to understand and will be useful in your journey to become a hackerman/woman. 

## Types of On-Disk Evasion Technique:

1. Packers
2. Obfuscators
3. Crypters
4. Software Protectors


## Packers

- This technique is not used as much anymore but essentially what this technique does is compress the exectuable which changes its signature, thus being able to bypass AV. 
- Popular Packers:
    - UPX


## Obfuscators
- The main purpose of obfuscators is to just change the code that is written without changing the functionality of the malware
- Many AV detection tools inspect code and look for specific byte strings or patterns. 
- By changing the structure of the code, it changes the signature and makes it harder for AV tools to pick up that it is indeed malware


## Crypters:
- Crypters are one of the most common modern technuques of bypassing malware
- The malware will include a decrypting stub that restores the original code upon execution
- This action happens in memory so the only thing that is written to disk is the encrypted code
    - This is great for attackers because it makes it difficult for forensic experts to examine the code and determine where it came from


## Software Protectors
- These are a combination of all of the previous tehcniques mentioned combined
- Some additional features may also include:
    - Anti-reversing
    - Anti-debugging
    - VM Emulation detection
    - 

# In-Memory Evasion Techniques (Process Execution Injections aka PE)

What is a PE Injection?
- Rather than any of the tools used above to obfuscate or change code, PE injections focus on the manipulation of RAM or volatile memory to keep anything from being written to disk

## Types of In-Memory Evasion Techniques:
1. Remote Process Memory Injection
2. Reflective DLL Injection
3. Process Hollowing
4. Inline Hooking

### Remote Process Memory Injection
- The technique takes a valid/ safe process and injects it with a malicious payload
- One Windows, the Windows API can be leveraged to do this



