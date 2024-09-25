# eJPT Exam Tools

Here is a list of the necessary tools for each point of the eJPT exam, based on the PTS course and the information from your GitHub notes:

## 1. Assessment Methodologies (25%)

- **Locate endpoints on a network**
  - **Nmap**: For scanning the network for active endpoints.
  - **Netcat (nc)**: For simple connectivity checks to endpoints.

- **Identify open ports and services on a target**
  - **Nmap**: With specific scans to identify open ports and services (e.g., `nmap -sS -sV`).

- **Identify operating system of a target**
  - **Nmap**: Using the `-O` flag to detect the operating system.

- **Extract company information from public sources**
  - **Google Dorking**: Using targeted search queries for information gathering.
  - **LinkedIn**: To search for company profiles and employees.

- **Gather email addresses from public sources**
  - **theHarvester**: To collect email addresses from various sources.
  - **Google Dorking**: To specifically search for email addresses on company websites.

- **Gather technical information from public sources**
  - **WHOIS Lookup**: To collect technical details about the domain and administrative contacts.

- **Identify vulnerabilities in services**
  - **Nessus or OpenVAS**: For scanning vulnerabilities.
  - **Nikto**: For testing web applications against known vulnerabilities.

- **Evaluate information and criticality or impact of vulnerabilities**
  - **CVSS (Common Vulnerability Scoring System)**: To assess the criticality of vulnerabilities.

## 2. Host and Networking Auditing (25%)

- **Compile information from files on target**
  - **cat, less**: For displaying file contents in the terminal.

- **Enumerate network information from files on target**
  - **ifconfig or ipconfig**: For collecting network details on the target system.

- **Enumerate system information on target**
  - **uname -a**: To gather system information.

- **Gather user account information on target**
  - **cat /etc/passwd**: To collect user account information in Unix/Linux.

- **Transfer files to and from target**
  - **scp (Secure Copy) or rsync**: For transferring files between hosts.

- **Gather hash/password information from target**
  - **John the Ripper**: For cracking password hashes.
  - **Hashcat**: For cracking hashes with GPU support.

## 3. Host and Network Penetration Testing (35%)

- **Identify and modify exploits**
  - **Metasploit Framework**: For identifying and modifying exploits.

- **Conduct exploitation with Metasploit**
  - **Metasploit Framework**: For carrying out exploits against target systems.

- **Demonstrate pivoting by adding a route and by port forwarding**
  - **Metasploit**: For setting up pivoting.
  - **SSH**: For setting up port forwarding to redirect traffic.

- **Conduct brute-force password attacks and hash cracking**
  - **Hydra**: For brute-force attacks on login services.
  - **John the Ripper and Hashcat**: For cracking password hashes.

## 4. Web Application Penetration Testing (15%)

- **Identify vulnerabilities in web applications**
  - **Burp Suite**: For testing web applications for vulnerabilities.
  - **OWASP ZAP**: Another tool for identifying security issues in web applications.

- **Locate hidden files and directories**
  - **Dirb**: For scanning hidden directories and files.
  - **Gobuster**: An alternative to Dirb for finding hidden paths.

- **Conduct brute-force login attack**
  - **Hydra**: For brute-force attacks on web logins.
  - **Burp Suite Intruder**: To test credentials against web applications.

- **Conduct web application reconnaissance**
  - **Nikto**: For scanning web applications for vulnerabilities and security issues.
  - **Wappalyzer**: For identifying technologies used on the target website.
