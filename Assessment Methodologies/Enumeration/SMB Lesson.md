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

nmap [target IP .3]

Explanation: Performs a basic Nmap scan on the target IP to identify open ports and running services.
2. Nmap Service Version Detection

`nmap [target IP] -sV -p 139, 445`

Explanation: Scans ports 139 and 445 to detect versions of services running on these ports, which are commonly associated with SMB.
3. Nmap UDP Scan

`nmap [target IP] -sU --top-ports 25 --open -sV`

Explanation: Conducts a UDP scan on the top 25 ports and attempts to identify the service versions running on those open ports.
4. SMB OS Discovery

`nmap [target IP] -p 445 --script smb-os-discovery`

Explanation: Uses the smb-os-discovery script to gather OS information from the SMB service on port 445.
5. Start Metasploit Framework

`msfconsole`

Explanation: Launches the Metasploit Framework for further exploitation.
6. Use SMB Version Auxiliary Module

`use auxiliary/scanner/smb/smb_version`

Explanation: Selects the SMB version scanner module within Metasploit to determine the SMB version on the target.
7. Set Target IP for Metasploit Module

`set rhosts [target IP]`

Explanation: Configures the target IP address for the SMB version scanner module.
8. Show Metasploit Module Options

`options`

Explanation: Displays the current configuration options for the SMB version scanner module.
9. Run Metasploit Module

`run`

Explanation: Executes the SMB version scanner module to identify the SMB version on the target.
10. Exploit (If Applicable)

`exploit`

Explanation: Attempts to exploit the target using the current module (in this context, it may run the same as run for auxiliary modules).
11. NetBIOS Name Service Lookup

`nmblookup -A [target IP]`

Explanation: Performs a NetBIOS name service lookup to retrieve the NetBIOS names and MAC address of the target machine.
12. List SMB Shares Without Authentication

`smbclient -L [target IP] -N`

Explanation: Lists available SMB shares on the target without requiring authentication, showing resources that might be accessible. The -L option lists the shares on the specified server, and the -N option tells smbclient not to prompt for a password, effectively attempting a null session.
13. Connect to SMB with RPC

`rpcclient -U "" -N [target IP]`

Explanation: Connects to the SMB service on the target using the rpcclient tool with null session (no username and no password).

### Summary of Commands

1. `nmap [target IP .3]`: Basic scan to identify open ports and services.
2. `nmap [target IP] -sV -p 139,445`: Service version detection on SMB ports.
3. `nmap [target IP] -sU --top-ports 25 --open -sV`: UDP scan on top 25 ports with service version detection.
4. `nmap [target IP] -p 445 --script smb-os-discovery`: OS discovery via SMB on port 445.
5. `nmap --script nbstrat -p 137 192.218.102.3`: Extracts netbios nam
6. `msfconsole`: Launches Metasploit Framework.
7. `use auxiliary/scanner/smb/smb_version`: Selects the SMB version scanner in Metasploit.
8. `set rhosts [target IP]`: Sets the target IP for the Metasploit module.
9. `options`: Displays configuration options for the module.
10. `run`: Executes the SMB version scan.
11. `exploit`: Attempts exploitation with the current module.
12. `nmblookup -A [target IP]`: Retrieves NetBIOS names and MAC address.
13. `smbclient -L [target IP] -N`: Lists SMB shares without authentication.
14. `rpcclient -U "" -N [target IP]`: Connects to SMB with RPC using null session. rpcclient is a tool used to execute client-side Microsoft RPC calls to an SMB server. It is particularly useful for enumerating information about the server.

Questions

    1. Find the default tcp ports used by smbd.
    2. Find the default udp ports used by nmbd.
    3. What is the workgroup name of samba server?
    4. Find the exact version of samba server by using appropriate nmap script.
    5. Find the exact version of samba server by using smb_version metasploit module.
    6. What is the NetBIOS computer name of samba server? Use appropriate nmap scripts.
    7. Find the NetBIOS computer name of samba server using nmblookup
    8. Using smbclient determine whether anonymous connection (null session)  is allowed on the samba server or not.
    9. Using rpcclient determine whether anonymous connection (null session) is allowed on the samba server or not.

    1. 139, 445
    2. 137, udp 
    3. RECONLABS (Command 3)
    4. Samba 4.3.11-Ubuntu (Command 4)
    5. Windows 6.1 (Samba 4.3.11-Ubuntu)
    6. SAMBA-RECON
    7. SAMBA-RECON
    8. Yes: public, john, aisha, emma, everyone, IPC$
    9. Yes

# SMB Server Reconnaissance: Samba 2
`ip a`
   - Displays network interfaces and their IP addresses on the local machine.

2. `nmap [target IP .3]`
   - Performs a basic scan to identify open ports and services on the target IP.

3. `nmap [target IP] -sV -p 445`
   - Detects the version of services running on port 445, typically used for SMB.

4. `rpcclient -U "" -N [targetIP]`
   - Connects to the target IP with a null session to interact with SMB services.

5. `srvinfo`
   - Queries the SMB server for detailed information about its configuration and operating system.

6. `enum4linux -o [targetIP]`
   - Enumerates information from an SMB server, including user and group details.

7. `smbclient -L [targetIP] -N`
   - Lists available SMB shares on the target machine without requiring authentication.

8. `nmap [targetIP] -p 445 --script smb-protocols`
   - Uses Nmap’s smb-protocols script to determine the SMB protocols supported by the target.

9. `msfconsole`
   - Launches the Metasploit Framework for advanced security testing.

10. `msfconsole: use auxiliary/scanner/smb/smb2`
    - Selects the SMB2 scanner module in Metasploit for detailed SMB2 testing.

11. `msfconsole: set RHOSTS [target IP]`
    - Sets the target IP address for the Metasploit module.

12. `msfconsole: options`
    - Displays the configuration options for the selected Metasploit module.

13. `msfconsole: run`
    - Executes the SMB2 scan to gather information or test for vulnerabilities.

14. `msfconsole: exit`
    - Exits the Metasploit Framework after testing is complete.

15. `nmap [target IP] -p 445 --script smb-enum-users`
    - Uses Nmap’s smb-enum-users script to enumerate users from the SMB server.

16. `enum4linux -U [target IP]`
    - Enumerates SMB users from the target server.

17. `rpcclient -U "" -N [target IP]`
    - Connects to the target SMB server with a null session for further interaction.

18. `rpcclient: enumdomusers`
    - Enumerates domain users from the SMB server using rpcclient.

    `rpcclient: lookupnames admin`
    - Looks up information about the specified user (e.g., 'admin') on the SMB server.


Questions

    Find the OS version of samba server using rpcclient.
    Find the OS version of samba server using enum4Linux.
    Find the server description of samba server using smbclient.
    Is NT LM 0.12 (SMBv1) dialects supported by the samba server? Use appropriate nmap script.
    Is SMB2 protocol supported by the samba server? Use smb2 metasploit module.
    List all users that exists on the samba server  using appropriate nmap script.
    List all users that exists on the samba server  using smb_enumusers metasploit modules.
    List all users that exists on the samba server  using enum4Linux.
    List all users that exists on the samba server  using rpcclient.
    Find SID of user “admin” using rpcclient.


First, we do a ping on our target address 192.35.143.3 to ensurse that its online.
`ping 192.35.143.3`

Then, we want to find out the OS version of the samba server using rpcclient:
`rpcclient -U "" -N 192.35.143.3`

We do a srvinfo to find out the OS:
`srvinfo`

**OS Version of Samba Server using rpcclient: 6.1**

We want to find the os version again with enum4linux:
`enum4linux -o 192.35.143.3`
**OS Version of Samba Server using enum4linux: 6.1**

Now we want to enumerate the server description using smbclient:
`smbclient -L 192.35.143.3 -N`: -L lists available shares on the server. -N means no password is used, attempting an anonymous connection.
**Server description: Workgroup: Reconlabs, Master: SAMBA-Recon

We want to find out if NT LM 0.12 (SMBv1) dialects is supported by the samba server. We use a script:
`nmap 192.35.143.3 -p 445 --script smb-protocols`
**NT LM 0.12 (SMBv1) is supported**

Is SMB2 protocol supported by the samba server? we use a smb2 metasploit module:
`msfconsole`
    msf5:`use auxiliary/scanner/smb/smb2`
    msf5:`set RHOSTS 192.35.143.3`
    msf5:`options`
    msf5:`run`
**We can see, that the samba server does support SMB (dialect 255.2)**

We want to list all users that exist on the samba server using a nmap script:
`nmap 192.35.143.3 -p 445 --script smb-enum-users`
**admin, aisha, elie, emma, john, shawn**

Now we wanna do the same again, but this time with the smb_enummuers metasploit modules:
`msfconsole`
    msf5:`search smb_enumusers`
    msf5:`use auxiliary/scanner/smb/smb_enumusers`
    msf5:`set RHOSTS 192.168.1.100`
    msf5:`show options`
    msf5:`run`
**john, elie, aisha, shawn, emma, admin**

We want to enumerate the users again, using enum4linux:
`enum4linux -U 192.35.143.3`: -U: This flag specifies that enum4linux should enumerate and display the user accounts on the target system
**john, ellie, aisha, shawn, emma, admin**

We want to find all users using rpcclient:
`rpcclient -U "" -N 192.35.143.3`
    rpcclient: `enumdomusers`
**john, elie, aisha, shawn, emma, admin**

We need to find the SID of user "admin" using rpcclient:
    rpcclient: `lookupnames admin`
**S-1-5-21-4056189605-2085045094-1961111545-1005**


## SMB: Samba 3

**Enumerate SMB Shares with Nmap**:

    `nmap [target IP] -p 445 --script smb-enum-shares`
Scans port 445 to enumerate shared directories on the Samba server using the `smb-enum-shares` script.

2. **Use Metasploit to Enumerate SMB Shares**:
    `msfconsole`
    - Launches the Metasploit Framework.
    msf5 > `use auxiliary/scanner/smb/smb_enumshares`
    msf5 `auxiliary(scanner/smb/smb_enumshares) > set rhosts [target IP]`
    msf5 `auxiliary(scanner/smb/smb_enumshares) > exploit`
    - Configures and runs the `smb_enumshares` module to enumerate shared directories on the target.

3. **Enumerate Shares with enum4linux**:
  
    `enum4linux -S [target IP]`
    - Enumerates shared directories on the target using `enum4linux`.

4. **List Shares with smbclient**:
    
    `smbclient -L [target IP] -N`
    - Lists available shares on the target server without authentication.

5. **Enumerate Group Information with enum4linux**:

    `enum4linux -G [target IP]`
    - Retrieves group information from the target using `enum4linux`.

6. **Connect to Samba Server with rpcclient**:
    
    `rpcclient -U "" -N [target IP]`
    - Connects to the Samba server using an anonymous (null session) connection.

7. **Perform a Full Information Scan with enum4linux**:

    `enum4linux -i [target IP]`
    - Performs a comprehensive information scan on the target using `enum4linux`.

9. **Access a Specific Share with smbclient**:
    
    `smbclient //[target IP]/Public -N`
    - Connects to the `Public` share on the target server without authentication.

    Inside the `smbclient` prompt:
    smb: \> cd secret
    smb: \> ls
    smb: \> cat flag
    smb: \> get flag
    ```
    - Navigates to the `secret` directory, lists files, displays the contents of the `flag` file, and downloads it.

10. **View the Downloaded Flag File**:
    `cat flag`
    - Displays the contents of the downloaded `flag` file.

### Commands Summary

- `nmap [target IP] -p 445 --script smb-enum-shares`: Scans for SMB shares on port 445.
- `msfconsole`: Launches Metasploit Framework.
    - `use auxiliary/scanner/smb/smb_enumshares`: Uses the `smb_enumshares` module in Metasploit.
    - `set rhosts [target IP]`: Sets the target IP for the module.
    - `exploit`: Runs the module to enumerate shares.
- `enum4linux -S [target IP]`: Enumerates shares with `enum4linux`.
- `smbclient -L [target IP] -N`: Lists SMB shares without authentication.
- `enum4linux -G [target IP]`: Retrieves group information with `enum4linux`.
- `rpcclient -U "" -N [target IP]`: Connects to the server with `rpcclient` using a null session.
- `enum4linux -i [target IP]`: Performs a comprehensive information scan.
- `smbclient //[target IP]/Public -N`: Connects to a specific share.
    - `cd secret`: Changes directory to `secret`.
    - `ls`: Lists files in the current directory.
    - `cat flag`: Displays the contents of the `flag` file.
    - `get flag`: Downloads the `flag` file.
- `cat flag`: Displays the contents of the downloaded file.


Questions

    List all available shares on the samba server using Nmap script.
    List all available shares on the samba server using smb_enumshares Metasploit module.
    List all available shares on the samba server using enum4Linux.
    List all available shares on the samba server using smbclient.
    Find domain groups that exist on the samba server by using enum4Linux.
    Find domain groups that exist on the samba server by using rpcclient.
    Is samba server configured for printing?
    How many directories are present inside share “public”?
    Fetch the flag from samba server.

First, we do a ping to ensure that our target is reachable:
`ping 192.86.4.3`

After that, we'll do a nmap script scan to enumerate shares:
`nmap 192.86.4.3 445 -p 445 --script smb-enum-shares`
**We see a public, IPC$, everyone, aisha, emma and john share**

Now, we want to use the smb_enumshares Metasploit module for share enumeration:
`msfconsole`
    - `use auxiliary/scanner/smb/smb_enumshares`
    - `set rhosts 192.86.4.3`
    - `exploit`
**We see exactly the same shares again**

Same thing again, but with enum4linux:
`enum4linux -S 192.86.4.3`
**Same shares again**

Same thing again, but with smbclient:
`smbclient -L 192.86.4.3 -N`
**Same shares again**

After that, we want to find domain groups that exist on the samba server by using enum4linux:
`enum4linux -G 192.86.4.3`
**domain groups: Maintainer, Reserved**

Now we want to find domain groups again using rpcclient
`rpcclient -U "" -N 192.86.4.3`
    rpcclient: `enumdomgroups`
**domain groups: Maintainer, Reserved**

We want to find out if samba server is configured for printing: 
`enum4linux -i 192.86.4.3`
**We don't see any printers**

We want to find out how many directories are present inside share "public":
`smbclient //192.86.4.3/Public -N`
**2 directories**

Now we want to get the flag file in that directory:
`cd secret`
`get flag`
`èxit`
`cat flag`
**03ddb97933e716f5057a18632badb3b4**






    
