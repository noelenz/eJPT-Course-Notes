# Introduction to the Metasploit Framework

- The Metasploit Framework (MSF) is an open-source, robust penetration testing and exploitation framework that is used by penetration testers and security researchers worldwide.
- The Metasploit Framework provides penetration testers with an robust infrastructure required to automate every stage of the penetration testing life cycle.
- It is also used to develop and test exploits
- Designed to be modular, allowing for new functionality to be implemented with ease.
- The Metasploit is available on GitHub.

## Essential Terminology

- Interface - Methods of interacting with the Metasploit Framework.
- Module - Piece of code that perform a particular task, an example of a module is an exploit.
- Vulnerability - Weakness or flaw in a computer system or network that can be exploited.
- Exploit - Piece of code/module that is used to take advantage of a vulnerability within a system, service or application.
- Payload - Piece of code delivered to the target system by an exploit with the objective of executing aribtrary commands or providing remote access to an attacker.
- Listener - A utility that listens for an incoming connection from a target.

## Metasploit Framework Interfaces

**msfconsole:** command center, all-in-one interface
**Metasploit Framework CLI:** command line utility that is used to facilitate the creation of automation scripts that utilize Metasploit modules. Can be used to redirect output from other tools in to msfcli and vice versa.
**Metasploit Community Edition:** web based GUI front-end for the Metasploit Framework that simplifies network discovery and vulnerability identification
**Armitage:** free Java based GUI front-end for the Metasploit Framework that simplifies network discovery, exploitation and post-exploitation.
