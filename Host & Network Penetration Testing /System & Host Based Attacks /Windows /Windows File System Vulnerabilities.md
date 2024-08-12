# Alternate Data Streams

## Alternate Data Streams (ADS)
- **Alternate Data Streams (ADS)**: An NTFS file attribute designed to maintain compatibility with the MacOS HFS (Hierarchical File System).
  - **Data Stream**: The default stream that contains the file's data.
  - **Resource Stream**: Typically contains the file's metadata.
- ADS can be used by attackers to hide malicious code or executables within legitimate files to evade detection by basic signature-based antivirus (AV) solutions and static scanning tools.

## Demonstration

1. **Create and Inspect a Text File**

   - **Open Temp Directory**: 
     `cd Desktop`  
     - Changes the current directory to Desktop where the file will be created.

   - **Create a Text File**: 
     `notepad test.txt`  
     - Opens Notepad to create a new file named `test.txt`.

   - **Enter Basic Data**: 
     - Enter some basic data in the file (data stream).

   - **Check File Properties**:
     - Go to **Properties** -> **Details** to view the file's metadata (resource stream).

   - **Delete the File**: 
     `del test.txt`  
     - Deletes `test.txt` to clean up.

2. **Create and Access an Alternate Data Stream**

   - **Create a Hidden File**: 
     `notepad test.txt:secret.txt`  
     - Creates a new hidden file called `secret.txt` within `test.txt`. The content is "this is hidden".

   - **Access the Hidden File**: 
     `notepad test.txt:secret.txt`  
     - Opens the hidden file to view its contents.

   - **List Alternate Data Streams**: 
     `dir /r`  
     - Lists files in the current directory along with their alternate data streams. Useful for verifying ADS presence.

   - **Display Alternate Data Streams**: 
     `type test.txt:secret.txt`  
     - Displays the content of the hidden stream `secret.txt` inside `test.txt`.

3. **Using winPEAS for Local Enumeration**

   - **Put Payload in Temp Directory**:
     `put payload.exe in Temp`  
     - Move or copy `payload.exe` to the `Temp` directory.

   - **Change Directory to Temp**: 
     `cd Temp`  
     - Navigate to the `Temp` directory.

   - **List Files in Temp**: 
     `dir`  
     - Lists all files in the `Temp` directory to verify `payload.exe` is present.

   - **Redirect Payload to a Log File**: 
     `type payload.exe > windowslog.txt:winpeas.exe`  
     - Redirects the contents of `payload.exe` into `windowslog.txt` under the name `winpeas.exe`, effectively hiding it.

   - **Open the Log File**: 
     `notepad windowslog.txt`  
     - Opens `windowslog.txt` to enter legitimate file data, making the file appear normal.

4. **Create a Symbolic Link**

   - **Change to System32 Directory**: 
     `cd \`  
     - Navigate to the root directory.

     `cd Windows\System32`  
     - Change directory to `System32` within Windows.

   - **Create Symbolic Link**: 
     `mklink wupdate.exe C:\Temp\windowslog.txt:winpeas.exe`  
     - Creates a symbolic link named `wupdate.exe` in `System32` pointing to the hidden file `winpeas.exe` inside `windowslog.txt`. This makes it appear as a regular executable in the `System32` directory.

   - **Behavior of `wupdate.exe`**:
     - Executes the hidden payload (`winpeas.exe`) from the symbolic link when `wupdate.exe` is run, leveraging the alternate data stream.

5. **Verify Alternate Data Stream Existence and Content**

   - **Check ADS with `streams` Tool**:
     `streams -d C:\Temp\windowslog.txt`  
     - Use the `streams` tool to display all alternate data streams associated with `windowslog.txt`. This helps in verifying if the payload is correctly hidden.

   - **Examine the Payload**:
     `certutil -decode payload.exe decoded_payload.exe`  
     - Decode a base64-encoded payload if necessary to reveal the content. This is useful for validating the payload integrity.

