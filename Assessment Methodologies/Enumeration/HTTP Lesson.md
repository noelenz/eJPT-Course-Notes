# HTTP IIS

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


