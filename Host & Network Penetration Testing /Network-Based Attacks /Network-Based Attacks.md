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


  




