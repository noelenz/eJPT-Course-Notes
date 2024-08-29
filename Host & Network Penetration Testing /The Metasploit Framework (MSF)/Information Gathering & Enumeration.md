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



