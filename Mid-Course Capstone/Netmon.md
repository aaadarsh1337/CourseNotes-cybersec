```md

[*] Walkthrough For Netmon From HackTheBox

[*] Scanning And Enumeration

[+] Open Ports

21/tcp(Anonymous Login Allowed)
80/tcp
135/tcp
139/tcp
445/tcp

[*] We Have An Exploit For The WebServer But The Exploit Should Be Authenticated. 
[*] Tried Default Credenials
[*] Didnt Work
[*] Lets Find The DataBase Location
[*] Found It! And We Can Get There Using Anonymous FTP
[*] There Is A Backup File. 
[*] Find In File The Default Username And There We Got A Credential!
[*] Login Successful

[*] Turn On Intercept Using Burp As We Require The Cookie For The Exploit To Work
[*] Just Refresh The Page And You We Get The Cookie In The Burp Intercept Window

https://www.exploit-db.com/exploits/46527

[*] Lets Use Impacket For Further Exploitation

https://github.com/SecureAuthCorp/impacket

[*] Lets Connect To The Target Using Impacket
[*] Usage: 

PsExec is a command-line tool that lets you execute processes on remote systems and redirect console applications' output to the local system so that these applications appear to be running locally. 

[*] Command:

psexec.py pentest:'P3nT3st!'@<IP>

[*] And We Got A Shell As Authority System!

[*] Done!
