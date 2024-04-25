# Reverse TCP Shell Using Metasploit 

## Objective

In this lab, I will exploit a Windows 10 system using the Metasploit Framework on Kali Linux. By doing so, I will have near-complete access to the victim machine through a reverse TCP shell. Once the shell is established, I will then demonstrate the ability to read directories and files on the target machine. 

The steps below can be followed in order to achieve the same results. 

### Skills Learned

- Networking Concepts
- Metasploit Framework 
- Post-Exploitation Techniques
- Payload Creation

### Project Enviroment Details
- Machine A is a Kali Linux VM.
- Machine B is a Windows 10 VM.
- For testing purposes both machines are on the same network (10.0.2.0/24).
- For testing purposes antivirus will be disabled.
- For testing purposes the Windows 10 firewall is disabled.

# Project
## Reverse TCP Shell
A reverse TCP shell is a type of shell session initiated by the target machine connecting back to the attacker's machine. By initiating a reverse TCP shell, the attacker will gain remote control over the compromised system. This allows the attacker capabilities to execute commands on the target machine and even transfer of data between both macines. 



 


