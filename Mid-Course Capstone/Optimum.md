[*] Walkthrough For Optimum From HackTheBox

[*] Scanning And Enumeration

[+] Open Ports

80/tcp

[*] It Is An HFS File Server. 

[*] Exploitation

[*] SearchSploit HSF Or Rejetto(Developer Of HFS)
[*] Found A Vulnerability
[*] Exploited Using Metasploit
[*] Got A Shell
[*] Low-Privileged User

[*] Privilege Escalation

[*] Sherlock Is A Good Tool For Windows Privilage Escalation Of Windows. 

https://github.com/rasta-mouse/Sherlock

[*] Windows Exploit Suggester Is Also Good. 

https://github.com/AonCyberLabs/Windows-Exploit-Suggester

[*] But First Lets Search: Windows 2012 r2 Build 9600 Privilage Escalation. 
[*] Got A Vulnerability. (MS16-032)
[*] Didn't Work
[*] Lets Use Windows Exploit Suggester. 
[*] Found ms16-098. 
[*] Had Some Problems And Had To Download Some More Stuff. 
[*] Transferred To Target Using certutil
[*] Worked!
[*] Root Shell

[*] Done! 