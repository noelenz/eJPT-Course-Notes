# Linux Kernel Exploits
- Kernel exploits on Linux will typically target vulnerabilites in the Linux kernel to execute arbitrary code in order to run privileged system commands or to obtain a system shell.
- This process will differ based on the Kernel version and distribution being targeted and the kernel exploit being used.
- Privesc on Linux systems will typically follow the following methodology:
  - Identifying kernel vulnerabilities
  - Downloading, compiling and transferring kernel exploits onto the target system.

## Tools & Environment
- Linux-Exploit-Suggester - This tool is designed to assist in detecting security deficiencies for given Linux kernel/Linux-based machine. It assesses (using heuristics methods) the exposure of the given kernel on every publicly known Linux kernel exploit.

## Demo: Linux Kernel Exploits

After we obtained a meterpreter session, we enumerate info:

`sysinfo`

`getuid`

www-data is a service account which is often used on linux system which host a webserver.
`shell`

`/bin/bash -i`

`cat /etc/passwd`

`sudo apt-get update`

We use the Linux Exploit Suggester:

meterpreter: `CD /TMP`

meterpreter: `ls`

meterpreter: `upload ~/Desktop/Linux-Enum/les.sh`

meterpreter: `shell`

meterpreter: `ls`

meterpreter: `chmod +x les.sh`

meterpeter: `ls -alps`

meterpeter: `./les.sh`

Gives us Exploits and OS information. We download the exploit from the website. Navigate to the Exploit download.
