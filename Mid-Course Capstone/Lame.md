[+] Scanning And Enumeration

[*] Started NMAP

[+] Open Ports:

21/tcp
22/tcp
139/tcp
445/tcp
3632/tcp

[*] Try To Login Using SMB

smbclient \\\\<IP>\\

[*] Found Shared
[*] There Is A tmp Share

smbclient \\\\<IP>\\tmp

[*] Login Successful
[*] But Got A Dead End

[*] Exploitation

[*] Search For Smb Version Exploit

[*] Version: 3.0.20-Debian
[*] Found An Exploit Using Metasploit(exploit/multi/samba/usermap_script)
[*] Successful

[*] Can Also Be Done Using FTP Exploit

[*] Done!