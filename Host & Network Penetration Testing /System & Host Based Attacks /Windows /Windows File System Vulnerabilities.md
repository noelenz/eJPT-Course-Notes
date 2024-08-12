# Alternate Data Streams
## Alternate Data Streams (ADS)
- Alternate Data Streams (ADS) is an NTFS file attribute and was designed to provide compatibility with the MacOS HFS (Hierarchical File System).
- Any file created on an NTFS formatted drive will have two different forks/streams:
  - Data Stream - Default stream that contains the data of the file.
  - Resource stream - Typically contains the metadata of the file.
- Attackers can use ADS to hide malicious code or ececuteables in legitimate files in order to evade detection.
- This can be done by storing the malicious code or executables in legitimate files in order to evade detection.
- This can be done by storing the malicious code or executables in the file attribute resource stream (metadata) of a legitimate file.
- This technique is usually used to evade basic signature based AVs and static scanning tools.

Open Temp
create a txt file
cd Desktop
  notepad test.txt
  enter basic data (data stream)
  properties -> Details (metadata, resource stream) 
  We can hide malicious payload in resource stream
  del test.txt

  Alternate data streams:
  notepad test.txt:secret.txt : we work in the hidden file: this is hidden

  access hidden file: notepad test.txt:secret.txt

winPEAS: program to perform local enumeration

  put payload.exe in Temp
  cd Temp
  dir
  type payload.exe > windowlog.txt:winpeas.exe
  notepad windowslog.txt (enter legitimate file data)

  create symbolic link: 
  cd \
  cd Windows\System32
  mklink wupdate.exe C:\Temp\windowslog.txt:winpeas.exe
  wupdate does: 
  
