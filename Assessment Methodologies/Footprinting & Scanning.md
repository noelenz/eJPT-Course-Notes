# Footprinting & Scanning

  ##   Introduction
  
  ###     Prerequisites

| Protocol/Service      | Port Number(s) | TCP | UDP |
|-----------------------|----------------|-----|-----|
| HTTP                  | 80             | ✓   |     |
| HTTPS                 | 443            | ✓   |     |
| FTP (Control)         | 21             | ✓   |     |
| FTP (Data)            | 20             | ✓   |     |
| SSH                   | 22             | ✓   |     |
| Telnet                | 23             | ✓   |     |
| SMTP                  | 25             | ✓   |     |
| POP3                  | 110            | ✓   |     |
| IMAP                  | 143            | ✓   |     |
| SMB                   | 445            | ✓   | ✓   |
| DNS                   | 53             | ✓   | ✓   |
| MySQL                 | 3306           | ✓   |     |
| PostgreSQL            | 5432           | ✓   |     |
| RDP                   | 3389           | ✓   |     |
| Kerberos              | 88             | ✓   | ✓   |
| NetBIOS               | 139            | ✓   |     |
| DHCP (Server)         | 67             |     | ✓   |
| DHCP (Client)         | 68             |     | ✓   |
| TFTP                  | 69             |     | ✓   |
| SNMP                  | 161            |     | ✓   |
| SNMPTRAP              | 162            |     | ✓   |
| NTP                   | 123            |     | ✓   |
| RIP                   | 520            |     | ✓   |
| Syslog                | 514            |     | ✓   |
| SIP (unencrypted)     | 5060           |     | ✓   |
| SIP (encrypted)       | 5061           |     | ✓   |
| LDAP                  | 389            | ✓   | ✓   |
| Microsoft SQL Server  | 1433           | ✓   | ✓   |


## Active Information Gathering

![image](https://github.com/user-attachments/assets/821d40f0-d174-4bd3-b23a-f651b2638a3b)

![image](https://github.com/user-attachments/assets/9d130611-ee35-4260-a1dd-5e1d5a888223)

## Networking Fundamentals

### Packets

Packets bestehen aus Header und Payload. Header besteht aus wichtigen Informationen vom Paket. Payload besteht aus tatsächlichen Daten die gesendet werden. The header has a protocol-specific structure: this ensures that the recieving host can correctly interpret the payload and handle overall communication


### OSI Model (Open Systems Interconnection)
![image](https://github.com/user-attachments/assets/7140f543-e5b7-4040-a317-7d6cef7ec0c1)

### Network Layer
Network Layer is responsible for logical addressing, routing, and forwarding data packets between devices across different networks
Network layer protocols:
- IP Versions
  - IPv4, 32 bit addresses
  - IPv6, 128 bit addresses
- Internet Control Message Protocol (ICMP)
  - Used for error reporting and diagnostics. ICMP messages include ping (echo request and echo reply), traceroute, and various error messages

### Internet Protocol (IP) Functionality
- Packet Structure:
  - IP organzies data into packets for transmission across networks. Each packet consists of a header and payload.
  - Header contains essential information, including the source and destination IP addresses, version number, time to live (TTL), and protocol type
- Fragmentation and Reassembly:
  - IP allows for the fragmentation of large packets into smaller fragments when traversing networks with varying Maxium Transmisson Unit (MTU) sizes.
  - The recieving host reassembles these fragments to reconstruct the original packet.
- IP Addressing Types:
  - There are three types: unicast (one-to-one communication). broadcast (one-to-all communication within a subnet). and multicast (one-to-many communication to a selected group of devices).
- Subnetting:
  - technique to divide a large IP network into smaller, more manageable sub-networks.
- Internet Control Message Protocol (ICMP):
  - closely associated with IP and is used for error reporting and diagnostics. Common ICMP messages include echo request and echo reply, which are used in the ping utility
- Dynamic Host Configuration:
  - DHCP is oftem used in conjunction with IP to dynamically assign IP addresses to devices on a network, simplifying the process of network configuration

### IP Header Format
- The IP protocol defines many different fields in the packet header. These fields contain binary values that the IPv4 services reference as they forward packets across the network.
  - IP source address - Packet Source
  - IP Destination Address - Packet Destination
  - Time-to-Live (TTL) - An 8-bit value that indicates the remaining life of the packet.
  - Type-of-Service (ToS) - The Type-of-Service field contains an 8-bit binary value that is used to determine the priority of each packet.
  - Protocol - This 8-bit value indicated the data payload type that the packet is carrying.b

![image](https://github.com/user-attachments/assets/21ddce2a-45dd-4ae4-9b55-751d1b35d79f)

![image](https://github.com/user-attachments/assets/4d81584c-440b-411e-8f87-9fc85b64356c)

![image](https://github.com/user-attachments/assets/758e0002-6ed8-4b7a-b103-e922c47e03f1)

![image](https://github.com/user-attachments/assets/59276f45-e3ca-4a39-8bb2-a9324aeff536)

### IPv4 Addresses
- IPv4 address consists of four bytes, or octets; a byte consists of 8 bits.
- a dot delimits every octet in the address.

### Reserved IPv4 Addresses
- 0.0.0.0 - 0.255.255.255 representing "this" network.
- 127.0.0.0 - 127.255.255.255 representing the local host
- 192.168.0.0 - 192.168.255.255 reserved for private networks.

## Transport Layer
- fourth layer of the OSI model, plays a crucial role in faciliating communication between two devices across a network.
- enrsures end-to-end communication, handling tasks such as error detection, flow control, segmentation of data into smaller units.
- responsible for providing end-to-end communication and ensuring the reliable and ordered delivery of data between two devices on a network.

### Transport Layer Protocols
- TCP (Tansmission Control Protocol): Connection-oriented protocol providing reliable and ordered delivery of data.
- UDP (User Datagram Protocol): Connectionless protocol that is faster but provides no guarantees regarding the rder or reliability of data delivery.

### TCP
- TCP is one of the main protocols operating at the Transport Layer (Layer 4) of the OSI model.
- Connection oriented, reliable protocol that provides a dependable and ordered delivery of data between two devices over a network.
- Ensures, that data sent from one application on a device is recieved accurately and in the correct order by another application on a different device.

- Connection-Oriented:
  - TCP establishes a connection between the sender and receiver before any data is exchanged. This connection is a virtual circuit that ensures reliable and ordered data transfer.
- Reliability:
  - TCP guarantees reliable delivery of data. It achieves this through mechanisms such as acknowledgements (ACK) and retransmissions of lost or corrupted packets. If a segment of data is not acknowledged. TCP automatically resends the segment.
- Ordered Data Transfer:
  - TCP ensures that data is delivered in the correct order. If segments of data arrive out of order, TCP reorders them before passing them to the higher-layer application.
    
#### TCP 3-Way Handshake
- The TCP three-way handshake is a process used to establish a reliable connection between two devices before they begin data transmission.
- It involves a series of three messages exchanged between the sender (client) and the reciever (server).
![grafik](https://github.com/user-attachments/assets/38c3ec03-f419-4478-959d-447a69bb0a58)
example: before a HTTP request can happen, a TCP 3-Way Handshake must happen.

1. Syn (Synchronize): process begins with the client sending a TCP segment with the SYN flag set. This initial message indicates the client's intention to establish a connection and includes an initial sequence number (ISN), which is a randomly chosen value.
2. SYN-ACK (Synchronize-Acknowledge): Upon recieving the SYN segment, the server responds with a TCP segment that has both the SYN and ACK (Acknowledge) flags set. The acknowledgment (ACK) number is set to one more than the initial sequence number recieved in the client's SYN segment. The server also generates its own initial sequence number.
3. ACK (Acknowledge): Finally, the client acknowledges the server's response by sending a TCP segment with the ACK flag set. The acknowledgment number is set to one more than the server's initial sequence number.
4. At this point, the connection is established, and both devices can begin transmitting data.
5. Ather the three-way handshake is complete, the devices can exchange data in both directions. The acknowledgment numbers in subsequent segments are used to confirm the receipt of data and to manage he flow of information.
![grafik](https://github.com/user-attachments/assets/4464b2cf-1efc-4793-b36c-9a89929cd7cd)
![grafik](https://github.com/user-attachments/assets/ac26bee8-e927-4254-a19a-d4c5e074e2db)

#### TCP Control Flags
- TCP (Transmission Control Protocol) uses a set of control flags to manage various aspects of the communication aspects of the communication process.
- These flags are included in the TCP header and control different features during the establishment, maintenance, and termination of a TCP connection.

- Establishing a Connection:
  1. SYN (Set): initiates a connection request.
  2. ACK (Clear): No acknowledgment yet.
  3. FIN (Clear): No termination request.
 
- Establishing a Connection (Response):
  1. SYN (Set): Acknowledges the connection request.
  2. ACK (Set): Acknowledge the recieved data.
  3. FIN (Clear): No termination request.

- Terminating a Connection:
  - SYN (Clear): No connection request.
  - ACK (Set) Acknowledges the recieved data.
  - FIN (Set) Initiates connection termination.
  
#### TCP Port Range
- TCP uses port numbers to distinguish between different services or applications on a device.
- Port numbers are 16-bit unsigned integers, and they are divided into three ranges
- The maximum port number in the TCP/IP protocol suite is 64.535
- Well-Known Ports (0-1023): Port numbers from 1023 are reserved for well-known services and protocols. These are standarized by the Internet Assigned Numbers Authority (IANA). Examples include:
  - 80: HTTP (Hypertext Transfer Protocol)
  - 443: HTTPS (HTTP Secure)
  - 21: FTP (File Transfer Protocol)
  - 22 SSH (Secure Shell)
  - 25: SMTP (Simple Mail Transfer Protocol)
  - 110: POP3 (Post Office Protocol version 3)
- Registered Ports (1024-49151): Port numbers from 1024 to 49151 are registered for specific services or applications. These are typically assigned by the IANA to software vendors or developers for their applications. While they are not standarized, they are often used for well-known services. Example include:
    - 3389: RDP
    - 3306: MySQL Database
    - 8080 HTTP alternate port
    - 27017: MongoDB Database
      - example: if 3389 Port is open on a windows machine, most likely that system is running rdp (or allows connection)

### UDP
- UDP, or User Datagram Protocol, is a connectionsless and lightweight transport layer protocol that provides a simple and minimalistic way to transmit data between devices on a network.
- UDP does not establish a connection before sending data and does not provide the same level of reliablity and ordering guarantees. Instead, it focuses on simplicity and efficiency, making it suitable for certain types of applications.
- Connectionless: UDP is a connectionless protocol, it doesnt establish a connection before sending data. Each UDP packet (datagram) is treated independently, and there is no persistent state maintained between sender and reciever.
- Unreliable: UDP does not provide reliable delivery of data. It does not guarantee that packets will be delivered, and there is no mechanism for retransmission of lost packets. This lack of reliability makes UDP faster but less suitable for applications that require guaranteed delivery.
- Used for Real-Time Applications: UDP is commonly used in real-time applications where low latency is crucial, such as audio and video streaming, online gaming, and voice-over-IP (VoIP) communication.
- Simple and Stateless: UDP is a stateless protocol meaining that it does not maintain any state informaion about the communication.
- Each UDP packet is independent of previous or future packets. 
![grafik](https://github.com/user-attachments/assets/e22f63f6-19fe-4156-9866-6dc843317c15)
Terminal: `netstat -antp` to see TCP connections
Windows:  `netstat -ano`  to see TCP connections


1. On my kali linux VM i opened Wireshark and Firefox.
2. I started the Wireshark capturing.
3. visited `google.com`
4. stopped the capturing
5. filtered for `tcp`
6. In `info` we can see the 3-way-handshake
7. IP Layer Source Address is Host, Destination Address is the Webserver i connected to
8. If i click on the TCP Packet, Source Port is the Port where the request comes from. Destination Port is 443.
9. Flags (set to syn), other flags are not set. proper sync request.
10. TLS Protocol after the TCP connection has been established


#TP layer Part 2 wiederholen. How to demonstrate the TCP Handshake


# Host Discovery

## Network Mapping
- After collecting information about a target organization during the passive information gathering sage, a penetration tester typically moves n to active information gathering phase which involves discovering hosts on a network, perfoming port scanning and enumeration.
- Every host connected to the Internet or a private network must have a unique IP address that uniquely identifies it on a said network.
- How can a pentester determine what hosts, within an in-scope network are online? what ports are oopen on the active hosts? and what operating sytems are running on the active hosts? Answer - Network Mapping.

- Network mapping in the context of pentesting refers to the process of discovering and identifying devices, hosts, and network infrastructure elements within a target network.
- Pentesters use network mapping as a crucial initial step to gather information about the network's layout, understand its architecture, and identify potential entry points for further exploitation.

Examples - Why Map a Network
- A company asks for you/your company to perform a pentest, and the following address block is considered in scope: 200.200.0.0/16.
- A sixteen-bit long netmask means the could contain up to 216 (65536) hosts with IP addresses in the 200.200.0.0 - 200.200.255.255 range.
- The first job for the pentester will involve determining which of the 65536 IP addresses are assigned to a host, and which of those hosts are online/active.
![grafik](https://github.com/user-attachments/assets/cc4db97d-41e7-4410-a839-2c7498dd2bad)
![grafik](https://github.com/user-attachments/assets/20849e27-f1e0-4273-b36b-27ebaa7ab6de)

### Network Mapping Objective
- **Discovery of Live Hosts:** Identifying active devices and hosts on the network. This involves determining which IP addresses are currently in use.
- **Identification of Open Ports and Services:** Determining which ports are open on the discovered hosts and identifying the services running on those ports. This information helps pentesters understand the attack surface and potential vulnerabilities.
- **Network Topology Mapping:** Creating a map or diagram of the network topology including routers, switches, firewalls, and ohter network infrastructure elements. Understanding the layout of the network assists in planning further pentesting activites.

- **Operating System Fingerprining:** Determining the operating systems running on discovered hosts. Knowing the operating system helps pentesters tailor their attack strategies to target vulnerabilities specific to that OS. **example:** If you perform a blackbox pentest and you discover that the target network is a windows environment or AD domain, you can focus your attention on Windows/AD specific attacks.
- **Serice Version Detection:** Identifying specific versions of services running on open ports. This informtion is crucial for pinpointing vulnerabilities associated with particular service versions.
- **Identifying Filtering and Security Measures:** Discovering firewalls, intrusion prevention systems, and other security measures in place. This helps pentesters understand the network's defenses and plan their approach accordingly.

### Nmap (Network Mapper) & Nmap Functionality
- **Usage:** Used for discovering hosts and services on a computer network, finding open ports, and identifying potential vulnerabilites.
- **Host Discovery:** Nmap can identify live hosts on a network using techniques such as ICMP echo requests, ARP requests, or TCP/UDP probes.
- **Port Scanning:** It can perform various types of port scans to discover open ports on target hosts.
- **Service Version Detection:** Nmap can determine the versions of services running on open ports. This info helps in understanding the software stack and potential vulnerabilites associated with specific versions.
- **Operating System Fingerprinting:**: Nmap can attempt to identify the operating system od target hosts based on characteristics observed during the scanning process.

### NMAP Host Discovery Techniques
- In pentesting, host discovery is a crucial phase to identify live hosts on a network before further exploration and vulnerability assessment.
- Various techniques can be employed for host discovery, and the choice of technique depends on factors such as network characteristics, stealth requirements, and the goals of the penetration test.

- **Ping Sweeps (ICMP Echo Requests):** Sending ICMP Echo Requests (ping) to a range of IP addresses to identify live hosts.
- **ARP Scanning:** Using Address Resolution Protocol (ARP) requests to identify hosts within the same broadcast domain.
- **TCP Syn Ping (Half-Open Scan):** Sending TCP SYN packets to a specific port (often port 80) to a check if a host is alive. If the host is alive, it respends with a TCP SYN-ACK. This technique is stealthier than ICMP ping. 
- **UDP Ping:** Sending UDP packets to a specific port to check if a host is alive. This can be effective for hosts that do not respond to ICMP or TCP probes.
- **TCP Ack Ping:** Sending TCP Ack packets to a specific port to check if a host is alive. This technique expects no response, but if a TCP RST (reset) is recieved, it indicates that the host is alive.
- **SYN-ACK Ping (Sends SYN-ACK packets):** Sending TCP SYN-ACK packets to a specific port to check if a host is alive. If a TCP RST is recieved, it indicates that the host is alive

- To enumerate the best host discovery technique for your needs, there are some considerations you need to keep in mind:
  - **ICMP Ping:**
    - Pros: ICMP ping is a widely supported and quick method for identifying live hosts.
    - Cons: Some hosts or firewally may be configured to block ICMP traffic, limiting its effectiveness. ICMP ping can also be easily detected.
  - "**TCP SYN Ping:**
    - Pros: TCP SYN ping is stealthier than ICMP and may bypass firewalls that allow outbond connections.
    - Cons: Some hosts may not respond to TCP SYN requests, and the results can be affected by firewalls and security devices.
   

## Ping Sweeps
- A ping sweep is a network scanning technique used to discover live hosts (computers, servers, etc) within a specific IP range on a network.
- the basic idea is to send a series of ICMP Echo Request (ping) messages to a range of IP's and observe the responses to determine which addresses are acitve or reachable (response).
- **Windows blocks ICMP requests**
- Ping sweeps work by sending one or more specially crafted ICMP packets (Type 8 - echo request) to a host.
- Destination replies with ICMP echo reply (Type 0) packet = host is alive.
- In context of ICMP, ICMP echo Request and Echo Reply messages are used for purpose of ping. These messages have specific ICMP type and code values associated with them.

- ICMP Echo Request:
  - Type: 8
  - Code: 0
    **- if host online, =**
- ICMP Echo Reply:
  - Type: 0
  - Code: 0

- "Type" field in the ICMP header indicates the purpose/function of the ICMP message, and the "Code" field provides additional information or context related to the message type.
- In case of ICMP Echo Request and Echo Reply, the Type value 8 represents Echo Request and the Type value 0 represents Echo Reply.*
- So, when a device sends an ICMP Echo Request, it creates an ICMP packet with Type 8, Code 0.
- When the destination devices recieve the Echo Request and responds with an Echo Reply, it creates an ICMP pacet with Type 0, Code 0.

*ICMP Echo Request and Echo Reply:
- Type value 8 = Echo Request
- Type value 0 = Echo Reply

- When Host is offline, ICMP echo Request sent by ping utility will not recieve a IMCP Echo Reply.
- No response doesn't mean that the host is permanently offline; it also could be network congestion, temporary unavailability, or firewall setting that block ICMP traffic.
- ping provides a simple way to check the reachability of a host.
  ![grafik](https://github.com/user-attachments/assets/063e20e9-cf6f-4525-af7a-d25048dfaf21)

### Pracitcal Ping Sweeps

- Target IP address: 10.2.25.156
- Tools: ping utility, fping

1. `ping 10.2.25.156` = no response
2. Terminal: `ping -c 5 10.2.25.156` = no response
3. Windows: `ping -n 5 10.2.25.156`
4. **Reason:** Host is offline or ICMP Echo Request could be blocked (network configuration, firewall, OS on host)
5. `sudo wireshark`, `ifconfig`
6. run wireshark with primary eth: `sudo wireshark -i eth1`
7. `ping 10.2.25.156`
8. No ICMP echo reply. Type 8 and Code 0, we should get a response. Host offline?
9. `ping -c 5 10.2.25.156`

**Scan every IP in subnet**

1. `ping -c 1 10.10.18.0`
2. `ping -b -c 1 10.10.18.0`
*pinging other subnet eth0*
3. `ping -b -c 10.1.0.0`
4. IP is in fact online, ac Alexis Ahmed

**FPING**
`fping -a -g 10.10.18.0/24` gives all of the online/offline hosts // fping still uses ICMP
  - `-fping -h` `man fping`
  - `set source address` = stealth, spoof source IP, make it look like ICMP echo request comes from another IP address
  - `fping -a -g 10.10.18.0/24 2>/dev/null` shows only online IP's in that subnet
10.10.18.1
10.10.18.3 (local machine)
*if windows hosts are there, they are blocking*

  - `fping -a 10.2.25.156 // target IP` no response. Because target system is Windows.
  - `nmap -Pn 10.2.25.156 // -Pn skips host discovery` Host is up, available.

same ICMP echo Ping sweep with nmap:
  - `nmap -sn 10.2.25.156` down, because host discovery


# Host Discovery With Nmap

**- Target IP Address: 10.2.18.206**
**- Mission: identify every IP in eth1 subnet should be scanned if they are active

*`nmap scanoptions target`*
*`nmap -sn 192.168.1.1 --script`*
*`nmap -help`*
*`man nmap`*, /-sn for command search

-  `ifconfig`,
-  `nmap sn [subnet.0/24]`, `nmap sn [subnet.0-range]`: scans every host in this subnet
what is being sent by nmap when we use -sn?
-  `sudo wireshark -i eth1`
- `nmap -sn *eth*/24`
Wireshark: 
- when you are connected to a physical connected network, sn / ping scan will utilize ARP protocol to perform Host discovery.

- `nmap sn [subnet.0/24] --send-ip`: hosts that are active in this subnet
Wireshark:
- now icmp echo requests should also been sent
- TCP should been sent from the kali system, SYN flag should be set
**Problem: ICMP**.

Ping Scan Combined with Custom Port Specifications:

A ping scan in Nmap (-sn) can be combined with other host discovery options that allow for specifying custom ports. This means that instead of relying on the default ports, you can choose which ports Nmap uses to send its TCP-SYN or TCP-ACK packets.
Default Behavior:

    By default, when performing a ping scan, Nmap sends:
        TCP-SYN packets to port 443.
        TCP-ACK packets to port 80.

These defaults can be overwritten with custom port specifications.
How to Specify Custom Ports:

You can change the ports used for the TCP-SYN and TCP-ACK packets with options like -PS (for SYN) and -PA (for ACK).
Example Command:

Suppose we want to check if hosts are active by sending TCP-SYN packets to port 22 (SSH) and TCP-ACK packets to port 25 (SMTP) in the subnet 192.168.1.0/24.

bash

nmap -sn -PS22 -PA25 192.168.1.0/24

    Explanation:
        -sn: Perform a ping scan (disable port scanning).
        -PS22: Send TCP-SYN packets to port 22.
        -PA25: Send TCP-ACK packets to port 25.
        192.168.1.0/24: The target subnet.

When to Use This:

    ICMP Blocked:
        When ICMP echo requests (default ping) are blocked by a firewall or security configuration, using TCP packets can bypass these restrictions.

    Specific Services:
        If you know that certain services (e.g., SSH, HTTP, SMTP) are more likely to be open, you can target those ports specifically.

    Stealth and Precision:
        By specifying ports commonly associated with legitimate services, you may reduce the chances of detection and increase the accuracy of host discovery.

How It Works:

    TCP-SYN Packets:
        Nmap sends a SYN packet (part of the TCP handshake) to the specified port (e.g., port 22). If the host is active and the port is open, it responds with a SYN-ACK.

    TCP-ACK Packets:
        Nmap sends an ACK packet to the specified port (e.g., port 25). If the host is active, it responds with a RST (reset).

    Result Interpretation:
        Nmap interprets the responses (SYN-ACK or RST) to determine if the host is alive.

Example Scenario:

Let's say you're scanning a subnet where ICMP is blocked, and you know that some servers offer SSH and SMTP services. You can use the following command to check for active hosts:

bash

nmap -sn -PS22 -PA25 192.168.1.0/24

    This command sends TCP-SYN packets to port 22 and TCP-ACK packets to port 25 for each IP address in the subnet 192.168.1.0/24.
    If any host responds to these packets, Nmap marks them as active.

By customizing the ports, you can effectively discover active hosts even in environments with restrictive network configurations.

# Host Discovery With Nmap Part II

scan multipe IP's
`nmap -sn [target ip] [target ip]`

- `vim targets.txt` wq
*here you can insert IP's without typing manually*
- `nmap -sn -iL targets.txt`

TCP SIN PING:
- By default, it will send a tcp syn packet to port 80 on the target system. If port closed, host responses with RSD packet. if port is open, host response with TCP syn-ack packet = connection established. after that, an RSD packet is sent to reset that connection.
- In some cases, firewalls are configured to drop RSD packets, custom ports need to be specified. this is a way to perform port scanning with multiple IP
- `nmap -sn -PS`: -sn = no port scan, -PS = override packets that the ping sends, specify TCP SYN ping. This command will send a SYN packet to the target on port 80. If host is online and port 80 is open, it will respond with a SYN-ACK. if closed, port will response with a RSD packet. If no response, its offline.
- Using nmap -sn -PS [target ip] is more effective in environments where ICMP traffic is restricted but TCP traffic is allowed. It provides a way to discover hosts that may not respond to standard ICMP echo requests.

-Start Wireshark capture and run scan
- SYN to Port 80 on target
- Target response with a SYN-ACK, Source Port 80
- Attacker (We) sends RST
- NMAP need a RST or SYN Ack response, to know if host is up. No response = host is offline
- Its also possible, to give a port range to -PS or a (few) specific Port.


### TCP ACK PING

NMAP will send a TCP Packet with ACK flagset to Port 80 of the target system. If it is acitve, it will return a RST packet.
- `nmap -sn -PA [target IP]`: 0 hosts up.
change port, still not up  
ACK Ping gets blocked by systems. not reliable.
ACK Scan is good for utilize if theres a firewall

### ICMP SPECIFIC PING SCAN

- `nmap -sn -PE [target IP]`
- `nmap -sn -PE [target IP] --send-ip // if on local ethernet`
1. ping scan 2. TCP SYN ping Scan

1. nmap -sn -v -T4 [target IP]
2. nmap -sn -PS21,22,25,80,445,3389,8080 -T4 [target IP] | Alexis' method
3. 2. nmap -sn -PS21,22,25,80,445,3389,8080 -PU137,138 -T4 [target IP] | Alexis' method
  
# Port Scanning


`nmap [target IP]`: SYN port scan (1. Host Discovery, 2. SYN packet to 1000 most common ports
`nmap -Pn [target IP]`: Skips host discovery
`nmap -Pn -F [target IP]`: -P scans most common 100 ports
`nmap -Pn -p 80 `: Specify specific (80)
`nmap -Pn -p80,445,3389,8080`: multiple ports (filtered: Windows firewall. No firewall: closed)
`nmap -F [target IP]` 
`nmap -Pn -p-`: scan all tcp ports

SYN (stealth) port scan:
`sudo wireshark - eth1`: SYN packet to target port. If target port is open, response with a SYN-ACK packet. firewall blocks RSD response, SYN-ACK gets dropped
Port 80 gives SYN ACK, so port 80 is open. nmap sends back RST to terminate 3-way-handshake before its established (saving time).

conclusion: nmap will send a SYN packet to target port, if target port is open, response SYN-ACK packet. If closed: RST packet. IF nmap doesnt recieve a SYN-ACK or RST, theres a firewall or filtered. Port still can be open.

if you are a non-proviliged user. `nmap -Pn -sS -F [target IP]`
`nmap -Pn -sT [target IP] `: TCP connect scan, default port scanning if no root or sudo. Loud on a network, gets detected easily. Completes the 3-way-handshake.

Scan for udp ports:
`nmap -Pn -sU -p [target IP]`

## Service Version & OS Detection

1. Host Discovery: `ifconfig`, pentest on eth1. 24subnet. `ip a s`
2. `nmap -sn [subnet.0/24]. First we want to see if any hosts are available in this subnet.
3. target-1 is our primary target.
4. nmap -sS [target ip]. all closed, so we need to scan the entire tcp port range:
5. nmap -sS -p- [target IP]
![grafik](https://github.com/user-attachments/assets/7995ead8-cd00-457d-b365-5a0cf556fa04)
6. serivce version detection scan: nmap -T4 -sS -sV -p- [target IP]
![grafik](https://github.com/user-attachments/assets/59d1d734-2ea5-49f3-92c8-90eeba8e5734)
7. How tell what operating system is used: nmap -T4 -sS -sV -O -p- [target IP]
8. identify OS aggressively and see kernel OS: nmap -T4 -sS -sV -O --osscan-guess -p- [target IP]. can also be done with service version detection: -sV --version-intensity (0-9).

Host Discovery: Identify Network Interface

    Check Network Interface: Identify the active network interface and IP address.

    `ifconfig`
    `ip a s`

2. Ping Sweep: Identify Active Hosts

    Ping Sweep the Subnet: Check which hosts are up in the target subnet.

    `nmap -sn [subnet.0/24]`

        Purpose: Quickly identify which hosts are online within the subnet.

3. Primary Target Identification

    Select Primary Target: Choose a host from the ping sweep results for further analysis.
        Example: Assume target-1 with IP 192.80.212.3 is the primary target.

4. Initial TCP SYN Scan

    Perform TCP SYN Scan: Check for open ports on the primary target.

    `nmap -sS [target IP]`

        Example: `nmap -sS 192.80.212.3`
        Purpose: Identify open ports quickly and stealthily.

5. Full TCP Port Range Scan

    Scan Entire TCP Port Range: If initial scan shows all ports closed, scan all 65535 ports.

    `nmap -sS -p- [target IP]`

        Example: `nmap -sS -p- 192.80.212.3`
        Purpose: Ensure no open port is missed.

6. Service Version Detection

    Service Version Detection Scan: Identify versions of services running on open ports.

    `nmap -T4 -sS -sV -p- [target IP]`

        Example: `nmap -T4 -sS -sV -p- 192.80.212.3`
        Purpose: Gather detailed information about the services to identify potential vulnerabilities.

7. Operating System Detection

    OS Detection: Identify the operating system of the target.

    `nmap -T4 -sS -sV -O -p- [target IP]`

        Example: `nmap -T4 -sS -sV -O -p- 192.80.212.3`
        Purpose: Determine the operating system for further targeted attacks.

8. Aggressive OS Detection and Kernel Identification

    Aggressive OS Detection: Perform a more aggressive scan to guess the OS and see kernel information.

`nmap -T4 -sS -sV -O --osscan-guess -p- [target IP]`

    Example: `nmap -T4 -sS -sV -O --osscan-guess -p- 192.80.212.3`
    Purpose: Obtain detailed OS and kernel information, useful for exploiting OS-specific vulnerabilities.
    Alternative: Use version intensity for service detection.

`nmap -sV --version-intensity 9 [target IP]`

    Example: `nmap -sV --version-intensity 9 192.80.212.3`
    Purpose: Increase the depth of service version detection.

## NMAP Scripting Engine (NSE)

`ifconfig`, eth1
`nmap -sn 192.224.77.0/24`
`nmap -sS -sV -O -p- -T4 [target IP]`: Sin scan
`ls -al /usr/share/nmap/scripts/`
`ls -al /usr/share/nmap/scripts/ | grep -e "http"`: HTTP (Webserver) specific scripts. http-enum.nse performs basic http enumeration
In the enumeration phase of a pentest, we don't want to exploit vulnerabilites yet.
`nmap -sS -sV -sC -p- -T4 [target IP]`:Default nmap script scan. Provides us OS, kernel etc. Now, i could look for vulnerabilites that affect the version of mongoDB or ubuntu (target OS)
check, which other mongoDB scripts are available. `nmap --help-help=mongodb-databases`
`nmap -sS -sV --script=mongodb-info -p- -T4 [target IP]`
`nmap --script=category`: specify script category
memcached service is running, so we check for memcached scripts: `ls -al /usr/share/nmap/scripts/ | grep -e "memcached"`
Lets see what it does: `nmap --script-help=memcached-info`
run script: `nmap -sS -sV --script=memcached-info -p- -T4 [target IP]`
Authentication is not required, so theres a potential vulnerability.

How to combine:
- serivce version detection scan
- operating system detection scan
- default nmap script scan

`nmap -sS -A -p- -T4 [target IP]`

# Evasion, Scan Performance & Output
## Firewall Detection & IDS Evasion 
### Firewall Detection
How to detect the presence of a firewall:
1. `nmap -help`
2. `nmap -sA` sends a packet with the ACK flagset
3. `nmap -sn [target IP]`
4. `nmap -Pn -sS -F [target IP]` since 92 ports are closed, it doesn't look like a firewall is active.
5. `nmap -Pn -sA -p445,3389 [target IP]`: ports are unfilitered, so there is no firewall which will intervere.

### IDS Evasion
1. `nmap -Pn -sS -sV -F [target IP]`
2. `sudo wireshark -i eth1`
3. nmap sends a SYN, we get back a SYN-ACK or RST.
4. `nmap -Pn -sS -sV -p80,445,3389 -f [target IP]`: packets will now be fragmented. Fragment offset is set to 0 on first fragment, on 2nd its 8.
5. `nmap -Pn -sS -sV -p80,445,3389 -f --mtu [target IP]`

Spoofing:
On every network wihtin the subnet / network is reserved for the gateway. For that, we need to be connected to the network.
1. `nmap -Pn -sS -sV -p445,3389 -f --data-length 200 -D [kali linux IP (Gateway)], [target IP]`
2. In Wireshark we can see:
   - fragmentation
   - source is decoy ip we specified
3. We want to change the source port to make it look less suspicious:
4. `nmap -Pn -sS -sV -p445,3389 -f --data-length 200 **-g 53** -D [kali linux IP (Gateway)], [target IP]`

## Optimizing Nmap Scans






























  


