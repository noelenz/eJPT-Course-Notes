# HTTP - IIS

`nmap 10.2.19.52`

`nmap 10.2.19.52 -sV -O`

Open webgoat.net

`whatweb 10.2.19.52` provides details about the site's characteristics (web technologies)

`http 10.2.19.52`, we find out what our server is

`dirb http://10.2.19.52/`: looking for directories. instert directories in browser

`browsh --startup-url http://10.2.19.52/Default.aspx`


# HTTP - IIS Nmap Scripts

`nmap [target IP]`

`nmap [target IP]-sV`: HTTP is open, website is reachable (on Default.aspx)

`nmap [target IP] -sV -p 80 --script http-enum`: shows us some interesting directories on the IIS server (similar to dirb)

`nmap [target IP] -sV -p 80 --script http-headers`: get the IIS server header information:

    ● IIS Server version is 10.0
    ● ASP.NET Version is 4.0.30319
    ● XSS Protection is 0
    ● The default page of the target web application is /Default.aspx
    
`nmap [target IP] -sV -p 80 --script http-methods --script-args http-methods.url-path:/webdav/10.2.19.52`: We get all the allowed methods on /webdav directory

`nmap [target IP] -sV -p 80 --script http-webdav-scan --script-args http-methods.url-path:/webdav/10.2.19.52`: identify webDAV installations. Script uses OPTIONS and PROPFIND methods to detect it.


Objective: 

    Identify IIS Server
    Get webserver header details
    Enumerated HTTP methods
    Detect WebDAV configuration - etc.

# HTTP - Apache

Tools used:
- nmap
- msf:     A penetration testing framework for finding, exploiting, and validating vulnerabilities.
- curl:    A command-line tool for transferring data with URLs, supporting various protocols like HTTP, HTTPS, FTP, and more.
- wget:    A command-line utility for downloading files from the web using HTTP, HTTPS, and FTP protocols.
- browsh:  A text-based web browser that renders modern web pages in a terminal, supporting HTML5, CSS3, and JavaScript.
- lynx:    A text-based web browser for navigating web pages via a command-line interface.
- dirb:    A web content scanner that searches for hidden web objects and directories on a web server.

`ip a`

We want to fnd out which ports are open:
`nmap 192.22.67.3`: Port 80 open

We need to find out what service is running on port 80:
`nmap 192.22.67.3 -p80 -sV`: Service: http, version: apache httpd 2.4.18

`nmap 192.22.67.3 -p 80 -sV -script banner`: http-server-header: Apache/2.4.18 (Ubuntu)

`msfconsole`

    msf5: `use auxiliary/scanner/http/http_version`
    
    msft: `set rhosts 192.22.67.3`
    
    msf5: `options`
    
    msf5: `run`

    msf5: `exit`
    
    **Apache/2.4.18 (Ubuntu)**

`curl 192.22.67.3 | more`: gives us code and information. Apache2 is used 

`wget "http://192.22.67.3"`: retrieves web files, Apache2 is used

`browsh --startup-url 192.22.67.3`: gives us a browser GUI. Apache2 is used

`lynx http://192.22.67.3`: Apache2

`msfconsole`

    msf5: `use auxiliary/scanner/http/brute_dirs`

    msf5: `show options`
    
    msf5: `set rhosts 192.22.67.3`
    
    msf5: `options`
    
    msf5: `exploit`
    
    msf5: `exit`
    
metasploit brute_dirs gives us following output:

Found http://192.22.67.3:80/dir/ 200

Found http://192.22.67.3:80/src/ 200

`dirb http://192.22.67.3 /usr/share/metasploit-framework/data/wordlists/directory.txt`
+ http://192.22.67.3//data (CODE:301|SIZE:309)          
+ http://192.22.67.3//dir (CODE:301|SIZE:308)

`msfconsole`

    msf5: `use auxiliary/scanner/http/robots_txt`
    
    msf5: `set rhosts 192.22.67.3`
    
    msf5: `options`
    
    msf5: `run`
    
BadBot is banned

    msf5: `curl http://192.22.67.3/cgi.bin/ | more`

1. Which web server software is running on the target server and also find out the version using nmap.
2. Which web server software is running on the target server and also find out the version using suitable metasploit module.
3. Check what web app is hosted on the web server using curl command.
4. Check what web app is hosted on the web server using wget command.
5. Check what web app is hosted on the web server using browsh CLI based browser.
6. Check what web app is hosted on the web server using lynx CLI based browser.
7. Perform bruteforce on webserver directories and list the names of directories found. Use brute_dirs metasploit module.
8. Use the directory buster (dirb) with tool/usr/share/metasploit-framework/data/wordlists/directory.txt dictionary to check if any directory is present in the root folder of the web server. List the names of found directories.
9. Which bot is specifically banned from accessing a specific directory?













# HTTP - IIS - reformatted with ChatGPT

## Initial Scans

- `nmap 10.2.19.52`
- `nmap 10.2.19.52 -sV -O`

Open [webgoat.net](http://webgoat.net)

- `whatweb 10.2.19.52`: Provides details about the site's characteristics (web technologies)
- `http 10.2.19.52`: Find out what our server is
- `dirb http://10.2.19.52/`: Looking for directories. Insert directories in the browser
- `browsh --startup-url http://10.2.19.52/Default.aspx`

## HTTP - IIS Nmap Scripts

- `nmap [target IP]`
- `nmap [target IP] -sV`: HTTP is open, website is reachable (on Default.aspx)
- `nmap [target IP] -sV -p 80 --script http-enum`: Shows us some interesting directories on the IIS server (similar to dirb)
- `nmap [target IP] -sV -p 80 --script http-headers`: Get the IIS server header information:
  - IIS Server version is 10.0
  - ASP.NET Version is 4.0.30319
  - XSS Protection is 0
  - The default page of the target web application is /Default.aspx
- `nmap [target IP] -sV -p 80 --script http-methods --script-args http-methods.url-path:/webdav/10.2.19.52`: We get all the allowed methods on the /webdav directory
- `nmap [target IP] -sV -p 80 --script http-webdav-scan --script-args http-methods.url-path:/webdav/10.2.19.52`: Identify WebDAV installations. Script uses OPTIONS and PROPFIND methods to detect it.

### Objective

- Identify IIS Server
- Get webserver header details
- Enumerate HTTP methods
- Detect WebDAV configuration

# HTTP - Apache

## Tools Used

- `nmap`
- `msf`: A penetration testing framework for finding, exploiting, and validating vulnerabilities.
- `curl`: A command-line tool for transferring data with URLs, supporting various protocols like HTTP, HTTPS, FTP, and more.
- `wget`: A command-line utility for downloading files from the web using HTTP, HTTPS, and FTP protocols.
- `browsh`: A text-based web browser that renders modern web pages in a terminal, supporting HTML5, CSS3, and JavaScript.
- `lynx`: A text-based web browser for navigating web pages via a command-line interface.
- `dirb`: A web content scanner that searches for hidden web objects and directories on a web server.

## Initial Setup

- `ip a`

## Port Scans

- `nmap 192.22.67.3`: Port 80 open
- `nmap 192.22.67.3 -p 80 -sV`: Service: http, version: apache httpd 2.4.18
- `nmap 192.22.67.3 -p 80 -sV --script banner`: http-server-header: Apache/2.4.18 (Ubuntu)

## Using Metasploit

- `msfconsole`
  - `use auxiliary/scanner/http/http_version`
  - `set rhosts 192.22.67.3`
  - `options`
  - `run`
  - `exit`
  - Result: **Apache/2.4.18 (Ubuntu)**

## Fetching Information

- `curl 192.22.67.3 | more`: Gives us code and information. Apache2 is used
- `wget "http://192.22.67.3"`: Retrieves web files, Apache2 is used
- `browsh --startup-url 192.22.67.3`: Gives us a browser GUI. Apache2 is used
- `lynx http://192.22.67.3`: Apache2

## Directory Brute Force

- `msfconsole`
  - `use auxiliary/scanner/http/brute_dirs`
  - `show options`
  - `set rhosts 192.22.67.3`
  - `options`
  - `exploit`
  - `exit`
  - Result:
    - Found http://192.22.67.3:80/dir/ 200
    - Found http://192.22.67.3:80/src/ 200

- `dirb http://192.22.67.3 /usr/share/metasploit-framework/data/wordlists/directory.txt`
  - Result:
    - http://192.22.67.3//data (CODE:301|SIZE:309)
    - http://192.22.67.3//dir (CODE:301|SIZE:308)

## Scanning for Robots.txt

- `msfconsole`
  - `use auxiliary/scanner/http/robots_txt`
  - `set rhosts 192.22.67.3`
  - `options`
  - `run`
  - Result: BadBot is banned

  - `curl http://192.22.67.3/cgi.bin/ | more`

## Tasks

1. Identify the web server software and version using `nmap`.
2. Identify the web server software and version using a suitable Metasploit module.
3. Check the web app hosted on the server using the `curl` command.
4. Check the web app hosted on the server using the `wget` command.
5. Check the web app hosted on the server using the `browsh` CLI-based browser.
6. Check the web app hosted on the server using the `lynx` CLI-based browser.
7. Perform a brute-force attack on web server directories and list the names of found directories using the `brute_dirs` Metasploit module.
8. Use `dirb` with the `/usr/share/metasploit-framework/data/wordlists/directory.txt` dictionary to check for directories in the root folder of the web server and list the found directories.
9. Identify which bot is specifically banned from accessing a specific directory.





