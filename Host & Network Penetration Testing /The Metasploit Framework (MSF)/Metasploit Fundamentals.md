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

# Metasploit Framework Architecture 

- A module in the context of MSF, is a piece of code that can be utilized by the MSF.
- The MSF libraries facilitate the execution of modules without having to write the code necessary in order to execute them.
![grafik](https://github.com/user-attachments/assets/57b60297-278a-4dbc-8c0b-93ece700a027)

## MSF Modules

- Exploit - Module that is used to take advantage of vulnerability and is typically paired with a payload.
- Payload - Code that is delivered by MSF and remotely executed on the target after successful exploitation. An example of a payload is a reverse shell that initiates a connection from the target system back to the attacker.
- Encoder - Used to encode payloads in order to avoid AV detection.  For example, shikata_ga_nai is used to encode Windows payloads.
- NOPS - Used to ensure that payloads sizes are consistent and ensure the stability of a payload when executed.
- Auxiliary - A module that is used to perform additional functionality like port scanning and enumeration.

## MSF Payload Types

- There are two types of Payloads:
  1. Non Stages Payload - Payload that is sent to the target system as is along with the exploit
  2. Stages Payload - A staged payload is sent to the target in two parts, whereby:
     The first part (stager) contains a payload that is used to establish a reverse connection back to the attacker, download the second part of the payload (stage) and execute it.

## Stagers & Stages

1. Stagers - Stagers are typically used to establish a stable communication channel between the attacker and target, after which a stage payload is downloaded and executed on the target system.
2. Stage - Payload components that are downloaded by the stager.

## Meterpreter Payload

- The Meterpreter payload is an advanced multi-functional payload that is executed in memory on the target system making it difficult to detect.
- It communicates over a stager socket and provides an attacker with an interactive command interpreter on the target system that facilitates the execution of system commands, file system navigation, keylogging and much more.

## MSF File System Structure

/usr/share/metasploit-framework/

## MSF Module Locatins

- MSF stores modules under the following directory on Linux systems:
    /usr/share/metasploit-framework/modules
- User specified modules are stored under the following directory on Linux systems:
    ~/.ms4/modules

# Penetration Testing with MSF

- We can adopt the PTES (Penetration Testing Execution Standard) as a roadmap to understand the various phases that make up a penetration test and how Metasploit can be integrated in to each phase.

## Penetration Testing Execution Standard

Metholody with the aim of addressing the need for a comprehensive and up-to-date standard for penetration testing.
![grafik](https://github.com/user-attachments/assets/e04a49a2-1e3d-4ad5-8b79-98d75a478dc9)

![grafik](https://github.com/user-attachments/assets/2f8e02b3-1bb7-4765-bbea-505e20818445)

# Installing & Configuring The Metasploit Framework

- The MSF is distributed by Rapid7 and can be downloaded and installed as a standalone package on both on Windows & Linux.
- MSF and its required dependencies come pre-packaged with Kali Linux w








