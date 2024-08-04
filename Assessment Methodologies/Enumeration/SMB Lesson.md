# SMB (Server Message Block) Protocol

## Explanation
The Server Message Block (SMB) protocol is a network protocol primarily used by Microsoft Windows for file and printer sharing services. It allows applications and users to share files and other resources over a network as if they were locally stored on their own computer. SMB operates on layer 5 and above of the OSI model and typically uses port 445 for communication.

### Usage
SMB is used to:
- Share files between computers in a network.
- Access shared printers.
- Perform inter-process communication (IPC).
- Provide and manage authentication information.

### Example
A common example of using SMB is connecting a Windows computer to a network drive. This can be done by entering the network address (e.g., `\\Server\Share`) in the File Explorer.

### Nmap Example for SMB Scanning
To detect SMB services on a target host, Nmap can be used. Here is a sample command:

`nmap -Pn -sS -sV -p445 -T4 [target IP]`

    -Pn: Skips host discovery.
    -sS: Performs a TCP SYN scan.
    -sV: Detects the version of the running services.
    -p445: Scans the SMB port.
    -T4: Sets the timing template to aggressive to speed up the scan.

When to Use SMB Scans

    During Network Reconnaissance: To identify shared resources and potential entry points.
    In Penetration Testing: To find and exploit vulnerabilities in the implementation of SMB, such as with exploits like EternalBlue.
    For Troubleshooting: To ensure SMB services are correctly configured and accessible.

SMB is an essential protocol in many enterprise networks, and understanding its function and methods for investigating it is crucial for successful network security assessments.

## Practice

To connect our vm with the smb file, we need to establish a connection to the server.

`ipconfig`
`nmap -T4 [subnet] --open`nmap scan for open ports and networks
`nmap [server IP] -sV -sC` gives us NetBios Domain name, NetBios Computername, smb-os-discovery

map network drive, server IP, c drive mapped as Z

terminal: 
`net use * /delete`
`net use Z: \\serverIP\\c$ smbserver_771 /user:administrator`

# SMB Nmap Scripts

`ping [target IP]`
`nmap [target IP]`
`nmap -p445 smb-protocols [target IP]`

Enumerate different parameters:
`nmap -p445 --script smb-security-mode [target IP]`
`nmap -p445 --script smb-enum-sessions [target IP]`
`nmap -p445 --script smb-enum-sessions --script-args 
smbusername=administrator,smbpassword=smbserver_771 [target IP]`
`nmap -p445 --script smb-enum-shares [target IP]`
`nmap -p445 --script smb-enum-shares --script-args smbusername=administrator,smbpassword=smbserver_771 [target IP]`
`nmap -p445 --script smb-enum-users --script-args smbusername=administrator,smbpassword=smbserver_771 [target IP]`
`nmap -p445 --script smb-servers-stats --script-args smbusername=administrator,smbpassword=smbserver_771 [target IP]`
`nmap -p445 --script smb-enum-domains --script-args smbusername=administrator,smbpassword=smbserver_771 [target IP]`
`nmap -p445 --script smb-enum-services --script-args smbusername=administrator,smbpassword=smbserver_771 [target IP]`
`nmap -p445 --script smb-enum-shares,smb-ls --script-args smbusername=administrator,smbpassword=smbserver_771 [target IP]`

# SMBMap
## Windows Recon: SMBMa 

1. Verify Target Reachability:

Check if the target IP is reachable.

`ping [target IP]`

2. Discover Open Ports and Services:

Perform a basic scan to identify open ports and services.

`nmap [target IP]`

3. Check SMB Protocols:

Scan port 445 and determine the SMB protocols supported by the target.

`nmap -p445 --script smb-protocols [target IP]`

4. Enumerate SMB Shares as Guest:

Attempt to enumerate SMB shares using the guest account.

`smbmap -u guest -p "" -d . -H [target IP]`

5. Enumerate SMB Shares as Administrator:

Enumerate SMB shares using the administrator account with the provided password.

`smbmap -u administrator -p smbserver_771 -d . -H [target IP]`

6. Execute Remote Commands via SMB:

Execute a command on the target machine to check for SMB vulnerabilities or configurations.

`smbmap -H [target IP] -u administrator -p smbserver_771 -x 'ipconfig'`

7. List Files in a Directory:

List files in a specific directory on the target machine.

`smbmap -H [target IP] -u administrator -p smbserver_771 -x 'ipconfig' -L`

8. Access a Specific Share:

Access the root share (e.g., C$).

`smbmap -H [target IP] -u Administrator -p 'smbserver_771' -r 'C$'`

9. Create a File to Upload:

Create a file that you will upload to the target.

`touch backdoor`

10. Upload a File to the Target:

Upload the file to a specific directory on the target machine.

`smbmap -H [target IP] -u Administrator -p 'smbserver_771' --upload '/root/backdoor' 'C$\backdoor'`

11. Verify File Presence:

Check if the file was uploaded successfully.

`smbmap -H [target IP] -u Administrator -p 'smbserver_771' -r 'C$'`

12. Download a File from the Target:

Download a specific file (e.g., flag.txt) from the target machine.

`smbmap -H [target IP] -u Administrator -p 'smbserver_771' --download 'C$\flag.txt'`

13. View the Downloaded File:

Display the contents of the downloaded file. check `ls` if not file is not available

`cat flag.txt`

Commands Summary

    ping [target IP]: Check if the target IP is reachable.
    nmap [target IP]: Scan for open ports and services.
    nmap -p445 --script smb-protocols [target IP]: Check SMB protocols on port 445.
    smbmap -u guest -p "" -d . -H [target IP]: Enumerate SMB shares with guest credentials.
    smbmap -u administrator -p smbserver_771 -d . -H [target IP]: Enumerate SMB shares with administrator credentials.
    smbmap -H [target IP] -u administrator -p smbserver_771 -x 'ipconfig': Execute remote commands on the target machine.
    smbmap -H [target IP] -u Administrator -p 'smbserver_771' -r 'C$': Access and enumerate a specific share.
    smbmap -H [target IP] -u Administrator -p 'smbserver_771' --upload '/root/backdoor' 'C$\backdoor': Upload a file to the target machine.
    smbmap -H [target IP] -u Administrator -p 'smbserver_771' --download 'C$\flag.txt': Download a file from the target machine.

  
# SMB: Samba 1

1. `nmap [target IP .3]`: nmap only assumes services
2. `nmap  [target IP] -sV -p 139,445`
3. `nmap [target IP] -sU --top-port 25 --open -sV`
4. `nmap [target IP] -p 445 --script smb-os-discovery`
5. `msfconsole`: metasploit framework
6. `use auxiliary/scanner/smb/smb_version -> show options`
7. msf5 auxiliary `set rhosts [target IP]`
8. msf5 auxiliary `options`
9. msf5 auxiliary `run`
10. msf5 auxiliary `exploit`
11. `nmblookup -A [target IP]`
12. `smbclient -L [target IP] -N`: We see IPC, might able to connect to
13. `rpcclient -U "" -N [target IP]`: connected, 


