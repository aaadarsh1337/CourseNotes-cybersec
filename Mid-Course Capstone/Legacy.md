[*] Notes On Legacy Box On HackThe Box

[+] Scanning And Enumeration

[+] Command:

nmap -sC -sV -A -p- -T4 <IP>

[+] Open Ports:

139/tcp
445/tcp

[*] Both Are Related To SMB. 
[*] Tried To Connect Using smbclient. Failed

[*] Did Some Enumeration On Google
[*] Found SMB Version Using Metasploit(auxiliary/scanner/smb/smb_version)
[*] Found Windows SP3

[+] Exploitation

[*] Searched Google For Smb Windows SP3 Exploit
[*] Used exploit/windows/smb/ms08_067_netapi In Metasploit
[*] Got A Shell

[*] Done! 