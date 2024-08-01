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
   
- ## Practical Host Discovery




  








