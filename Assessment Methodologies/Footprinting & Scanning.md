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

###










