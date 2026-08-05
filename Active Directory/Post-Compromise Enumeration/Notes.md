```md

[*] Post-Compromise Enumeration(Powerview And Bloodhound)

[*] Installing Powerview

https://github.com/PowerShellMafia/PowerSploit/blob/master/Recon/PowerView.ps1

[*] Now Copy This Script To One Of The User Machine And Run It(In Real-Life Will Will Have To Run It Using A Shell But For Simplicity Lets Run It Directly On The Windows Machine)

[*] Domain Enumeration Using Powerview

1. Open Command Prompt
2. Type:

powershell -ep bypass

3. Load Powerview:

. .\PowerView.ps1

4. Hit Enter.(Nothing Will Show Up)
5. Now We Can Run Commands

Get-NetDomain

[*] This Will Display Some Information

Get-NetDomainController

[*] This Will Display Some Information About Domain Controller

Get-DomainPolicy

[*] This Will Show The Policies In The Domain

(Get-DomainPolicy)."system access"

[*] This Will Display Some Information About Password Policy

Get-NetUser

[*] This Command Will Display Usernames, Descriptions, etc. Here Also, We Could See The Service Account's Decription With Password. (Pretty Long Output)

Get-NetUser | select cn

[*] This Will Display Only The Usernames

Get-NetUser | select samaccountname

[*] This Will Display Sam File's Account Names

Get-UserProperty

[*] This Will Display All User Properties

Get-UserProperty -Properties pwdlastset

[*] This Will Display The Time When A User Set His/Her Password

Get-UserProperty -Properties logoncount

[*] This Will Display The Number Of Times A User Has Logged In

Get-UserProperty -Properties badpwdcount

[*] This Will Display How Many Users Use Bad Passwords

Get-NetComputer

[*] This Will List Out The Computers In The Domain

Get-NetComputer -FullData

[*] This Will List Out A Lot Of Information About The Computers In The Domain

[*] Note: select Is Like grep In Linux

Get-NetGroup

[*] This Will Display Groups In The Domain

Get-NetGroupMember -GroupName "Domain Admins"

[*] This Will Display The Members Of The Domain Admins Group

Invoke-ShareFinder

[*] This Will Find All The Shared Folder On The System

Get-NetGPO

[*] This Will List All The Group Policies

Get-NetGPO | select displayname, whenchanged

[*] This Will Display The Policy And When It Was Made/Changed

[*] Refrence:

https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993

[*] Blood Hound

[*] Installation:

apt-get install bloodhound

[*] Blood Hound Uses neo4j, Lets Set It Up:

neo4j console

[*] This Should Output A Link. Open The Link In Your Browser

[*] Login Using:

User = neo4j
Password = neo4j

[*] Now Enter New Password
[*] Close The Browser
[*] Do NOT Close The Terminal. Open A New One And Type:

bloodhound

[*] Now Login Using 

Username: neo4j
Password: <YourPassword>

[*] Grabbing Data With Invoke-Bloodhound

https://github.com/BloodHoundAD/BloodHound/blob/master/Collectors/SharpHound.

[*] Note: All Users Should Be Logged In Order For BloodHound To Pull The Data Of Those Users

[*] Copy This File To The Windows Machine
[*] Running It:

powershell -ep bypass
. .\SharpHound.ps1

[*] Nothing Should Show Up But Its Running. Lets Run Our Commands:

Invoke-BloodHound -CollectionMethod All -Domain <DomainName>.local -ZipFileName File.zip

[*] This Should Create A .zip File
[*] Move The Zip File From The Machine To Our Kali Machine
[*] Now Open BloodHound
[*] Click On Upload Data Button On The Right Side And Upload The .zip File
[*] Now Click On The Three Lined Button On The Top-Left And You Should See Some Information About The Target
[*] Now Click On Queries
[*] You Can Play Around With It And Find Some Useful Data. 
