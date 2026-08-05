```md

[*] Walkthrough For Nibbles From HackTheBox

[*] Scanning And Emumeration

[*] Open Ports

22/tcp
80/tcp

[*] Website Just Has A Hello World. 
[*] Gobuster For Directory Listing

gobuster dir -u <IP> -w <Path To Wordlist>

[*] Found A Comment In Source Code. 
[*] The Comment Is A Directory!
[*] Go To The Website
[*] Nothing Much

[*] Exploitation

[*] searchsploit Nibble
[*] Got 2 Exploits
[*] Gobuster Found An Admin Login Page!
[*] Found Credentials

admin:nibbles

[*] Version Is 4.0.3
[*] Vulnerable!
[*] searchsploit nibble
[*] Found The Exploit
[*] Run It Using Metasploit
[*] Got A Shell

[*] Privilage Escalation

[-] Not Root
[*] Lets Do sudo -l
[*] We Can Run monitor.sh Without Password
[*] Make The Following Directories: personal And In personal Make stuff And In stuff Make monitor.sh
[*] Just Put 'bash -i' In monitor.sh. (Without Quotes)
[*] chmod +x monitor.sh
[*] And Run It As Sudo.(With Full Path)
[*] Got Root Shell

[*] Done!
