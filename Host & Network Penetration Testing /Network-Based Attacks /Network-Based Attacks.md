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

nmap -Pn -sS -sV -p445,3389 -f --data-length 200 -D 10.10.23.1,10.10.23.2 <Ziel-IP>


