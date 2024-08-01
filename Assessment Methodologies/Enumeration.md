# eJPT Study Notes

## Information Gathering

We need to identify vulnerabilities and web technologies. The more you know about your target, the more successful you will be.

### Types of Information Gathering
- **Passive Information Gathering**: Collecting information without actively engaging with the target.
- **Active Information Gathering**: Actively engaging with the target system to collect as much information as possible (requires authorization).

### Information We Are Looking For

#### Passive Information Gathering
- Identifying IP addresses & DNS information
- Identifying domain names and domain ownership information
- Identifying email addresses and social media profiles
- Identifying web technologies used on target sites
- Identifying subdomains

#### Active Information Gathering
- Discovering open ports on target systems
- Learning about the internal infrastructure of a target network/organization
- Enumerating information from target systems

## Passive Information Gathering

### Website Recon & Footprinting

#### What We Are Looking For
- IP addresses
- Hidden directories from search engines
- Names
- Email addresses
- Phone numbers
- Physical addresses
- Web technologies used

#### Tools and Techniques
1. **Browser**: Visit the target website (e.g., `hackersploit.org`) and copy the IP address.
2. **DNS Lookup**: Use `host hackersploit.org` to resolve the domain name to IP addresses.
3. **Directory and Sitemap**: Check `/robots.txt` and `/sitemap.xml` for hidden directories.
4. **BuiltWith and Wappalyzer**: Browser extensions to identify web technologies.
5. **Terminal**: Use `whatweb <domain>` to analyze web technologies.
6. **Download Website**: Use `sudo apt-get install webhttrack` to download the website for offline analysis.

### WHOIS Enumeration
- Terminal: `whois <domain>` to get domain ownership and nameserver information.
- Example: `whois zonetransfer.me` provides nameserver information, network range (NetRange), and CIDR.

### Website Footprinting With Netcraft
- **Netcraft**: Shows detailed site reports including technology stack and hosting details.
- Example: Visit `Netcraft` and input the target domain to get a comprehensive site report.

### DNS Recon
- **DNSRecon**: A Python script to check all NS records for zone transfers, enumerate general DNS records (MX, SOA, NS, A, AAAA, SPF, and TXT), and perform SRV record enumeration.
  - Example: `dnsrecon -d hackersploit.org`
- **DNSDumpster**: An online tool that provides DNS server details and subdomains.
- Example: `dnsrecon -d hackersploit.org` reveals mail servers and subdomains like `forum.hackersploit.org`.

### WAF Detection with Wafw00f
- Detects Web Application Firewalls (WAFs) by analyzing HTTP responses.
  - Command to list all detectable WAFs: `wafw00f -l`
  - Detect WAF for a specific domain: `wafw00f hackersploit.org`
  - Detect all possible firewalls: `wafw00f zonetransfer.me -a`

### Subdomain Enumeration with Sublist3r
- Sublist3r is a Python tool designed to enumerate subdomains using OSINT from multiple search engines and sources.
  - Example: `sublist3r -d hackersploit.org -e google,yahoo`

### Google Dorks
- Use Google search operators to find specific information.
  - Examples:
    - `site:domain.com`
    - `site:domain.com inurl:admin`
    - `site:*.ine.com` (identifies subdomains)
    - `site:*.ine.com intitle:admin`
    - `site:*.ine.com filetype:pdf`
    - `intitle:index of`
    - `site:bedag.ch intitle:index of`
    - `cache:ine.com` (use Wayback Machine for older versions of websites)
    - `inurl:auth_user:file.txt`
    - `inurl:passwd.txt`

### Email Harvesting with theHarvester
- A simple, yet powerful tool for OSINT gathering to determine a company's external threat landscape.
  - Example: `theHarvester -d hackersploit.org -b google,linkedin`
  - Why hide emails? Found emails can be used for malicious purposes.

### Leaked Password Databases
- Check for compromised accounts: `haveibeenpwned.com`

### DNS Zone Transfer

#### DNS Records
- **A**: Resolves a hostname or domain to an IPv4 address.
- **AAAA**: Resolves a hostname or domain to an IPv6 address.
- **NS**: Reference to the domain's nameserver.
- **MX**: Resolves a domain to a mail server.
- **CNAME**: Used for domain aliases.
- **TXT**: Text record.
- **HINFO**: Host information.
- **SOA**: Domain authority.
- **SRV**: Service records.
- **PTR**: Resolves an IP address to a hostname.

#### DNS Interrogation
- The process of enumerating DNS records for a specific domain to gather important information like IP addresses, subdomains, and mail server addresses.
- Command: `dnsrecon -d zonetransfer.me`
- **DNS Zone Transfer**: Copying zone files from one DNS server to another, which can be abused if misconfigured.

### Host Discovery With Nmap

#### Example Network Scans
- **Interface Query**: `ip a s` to show network interfaces and configurations.
- **Ping Scan**: `sudo nmap -sn 172.20.10.3/28` to discover active hosts in a subnet.
  - Example Output:
    - `Nmap scan report for 172.20.10.1` (Host is online, MAC address)
    - Summary: Covers 16 IP addresses in the subnet, identifies 3 active hosts.

#### Tools for Host Discovery
- **Netdiscover**: Use `netdiscover -help` for ARP requests.

## Port Scanning with Nmap

### TCP Ports
- **Default Scan**: `nmap [target IP]` (SYN scan of 1000 ports, Windows systems block ICMP pings)
- **Full Scan**: `nmap -Pn -p- [target IP]` (scans all 65535 ports)
- **Specific Ports**: `nmap -Pn -p 80,445,3389 [target IP]`
- **Quick Scan**: `nmap -Pn -F [target IP]` (scans top 100 ports)
- **UDP Scan**: `nmap -Pn -sU [target IP]`

### Service and OS Detection
- **Service Version Detection**: `nmap -Pn -sV [target IP]`
- **OS Detection**: `nmap -Pn -O [target IP]`
- **Default Script Scan**: `nmap -Pn -sC [target IP]`
- **Aggressive Scan**: `nmap -Pn -A [target IP]`
- **Output to File**: 
  - Normal output: `nmap -Pn -oN output.txt [target IP]`
  - XML output: `nmap -Pn -oX output.xml [target IP]`

### Adjusting Scan Speed
- **Scan Speed Options**: Use `-T0` (paranoid) to `-T5` (insane) to adjust the speed of scans.
