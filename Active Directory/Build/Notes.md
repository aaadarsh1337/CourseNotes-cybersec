```md

[*] Building Active Directory

[+] Lab

1. Windows Server(2019)
2. 2 Windows 10 Enterprise

[+] Requirements

1. 60 GB Disk Space
2. 16 GB RAM

[*] Necessary ISO's

[+] Download The Following:

https://www.microsoft.com/en-in/evalcenter/evaluate-windows-10-enterprise
https://www.microsoft.com/en-in/evalcenter/evaluate-windows-server-2019 (In ISO Format)

[*] Setting Up Domain Controller

[*] Open VMware Or VirtualBox
[*] Select The Server ISO(No Problem If It Detects 2016)
[*] Select The Standard Variant
[*] Let Everything Be Blank
[*] Click Next
[*] Do The Further Steps
[*] Assign About 60 GB Of Virtual Disk Storage
[*] Do NOT Power On After Setup Is Finished!
[*] Hit Finish
[*] Edit Virtual Machine Settings
[*] In Hardware, Remove Everything Related To Floppy Disk As It Can Cause Problems
[*] Make Sure The Network Is NAT. 
[*] Select Minimum Of 2GB Memory
[*] Play The Virtual Machine
[*] Press Any Key Fast
[*] Fill The Details
[*] Press Install Now
[*] Select Windows Server 2019 Standard Evaluation(Desktop Experience)
[*] Hit Next
[*] Agree The License
[*] Hit Next
[*] Use Custom Install
[*] Click Drive 0
[*] Click On New
[*] Click On Apply
[*] Click OK
[*] Select Drive 0 Partition 4(With About 50GB RAM)
[*] Hit Next
[*] Now, Wait Forever. (As It Takes A Lot Of Time To Install)
[*] Set A Password(If You Dont Want To Think A Lot, Set Your Password As: P@$$w0rd!)
[*] It Should Boot Up!
[*] Ya Not Full Screen But If You Want, You Can Download Additional Plugins For That :(
[*] Now Rename Your Server. 
[*] Goto To The Start Bar And Type computer And You Should Get An Option For View Your PC Name. 
[*] From There Hit Rename This PC(Something Like: HYDRA-DC)
[*] Click Restart Now
[*] Other Unplanned Option Is Fine
[*] Hit Continue
[*] Login Again
[*] Server Manager Should Automatically Open
[*] Click On Manage And Then On Add Roles And Features
[*] Role-Based Or Feature-Based Installation And Hit Next
[*] Hit Next Until You See A Roles List
[*] In The Roles List, Select Active Directory Domain Services
[*] Click On Add Features
[*] Hit Next For Next 3 Times And Hit Install. 
[*] Let It Install
[*] After Completition, Hit Close
[*] Now Click On The Flag(With Alert Symbol)
[*] Click Promote This Server To A Domain Controller
[*] Select Add A New Forest
[*] In Root Domain Name, Call It Whatever You Want To Call But It Should Have .local At The End(For Example. MARVEL.local)
[*] Click Next
[*] Type In A Passoword(Again Can Be: P@$$w0rd!)
[*] Hit Next
[*] Hit Next
[*] Wait For A Minute And Hit Next
[*] Let Everything Be Default And Hit Next
[*] Hit Next Again
[*] Wait Some More Time
[*] Click Install And Let Everything Work
[*] Now, On The Login Screen, You Should See MARVEL\Administrator. This Means Our Process Was Successful

[*] Setting Up User Machines

[*] I Wont Lead You. You Just Have To Install Enterprise Normally As A Virtual Machine(Make Sure While Signing In To Microsoft While Setup, Click Domain Join Instead. You Also Have To Rename This PC. This Should Boot It Up)
[*] Do This Once Again(As We Want Two User Machines)

[*] Setting Up Users, Groups And Policies

[*] Boot Up And Login To The 2019 Server(Domain Controller)
[*] Goto The Server Manger
[*] Click On Tools
[*] Click On Active Directory Users And Computers
[*] Click On USERNAME.local #Your Username
[*] Click On Users Tab
[*] Right Click Username.local And Select New > Organisational Unit
[*] Name It Whatever You Want
[*] Click On Ok
[*] Now Drag And Drop All Users(Except Administrator And Guest) To The New Group
[*] Now, We Have To Create 4 Users In The Users Group. 
[*] 2 = Normal(Just Make One And Right-Click And Copy)
[*] 2 = Domain Admin(Right Click On Administrator And Copy) And (Name One Of These Users SQLService And In The User's Description, Type: My Password Is <Password>)
[*] Be Sure To Check That For Every User, The Password Never Expires

[*] Now Click On File And Storage Services And Click On Shares
[*] Click On Tasks And Click New Share
[*] SMB Share - Quick
[*] Click Next 2 Times
[*] Give A Random Name(Like: hackme)
[*] Click On Next 3 Times And Hit Create And Then Close
[*] Now Open CMD As Administrator
[*] Type:

setspn -a <Domain Controller Name/<Service Username>.<Root Domain Name>.local:60111 <Root Domain Name>\<Service Username>

[*] Note: \ Doesnt Mean Or. You Have To Type It For Example:

setspn -a HYDRA-DC/SQLService.MARVEL.loacl:60111 MARVEL\SQLService

[*] Now Lets Check If The Changes Are Made. 

setspn -T <Root Domain Name>.local -Q */*

[*] Note: Again It Should Be Like:

setspn -T MARVEL.local -Q */*

[*] Now In The List You Should See Something Similar To The Command. 
[*] Success!

[*] Now We Will Have To Turn Off Windows Defender. Because Antivirus Evasion Is A Bit Advanced. 

[*] Now Click On The Windows Logo And Type: Group Policy Management
[*] Right Click On And And Run It As Administrator
[*] Click On Forest:<Root Domain Name>.local
[*] Click On Domains
[*] Right Click On <Root Domain Name>.local And Click On Create A GPO In This Domain, And Link It Here
[*] And Now In The Name Type: Disable Windows Defender
[*] Hit Ok
[*] Now Right Click On The Disable WIndows Defender Option And Select Edit
[*] Click On Computer Configuration
[*] Click On Policies And Then On Administrative Templates
[*] Click On Windows Components
[*] Scroll To The Bottom And Select Windows Defender Antivirus
[*] In The Right Column, There Should Be An Option: Turn off Windows Defender Antivirus
[*] Double-Click On It And Click On Enabled, Apply And OK

[*] Joining Our Machines To The Domain(Do This To Both The Windows 10 Enterprise Machines)

[*] In The User Computer:

1. Goto This PC
2. Goto C:\
3. Create A Folder Called Share
4. Right Click The Folder And Click On Properties
5. Goto The Sharing Tab And Click On Share
6. Click On Share Again
7. Click On Yes, turn on network discovery(If Needed)
8. Click Done And Close

[*] On The Domain Controller

1. Open CMD
2. Type ipconfig And Copy The IPv4 Address

[*] On The User Computer

9. Right Click On Internet Access And Open Network And Internet Settings
10. Click On Change Adapter Options
11. Right Click Ethernet0 And Click On Properties
12. Double-Click On Internet Protocol Version 4
13. Select Use The Following DNS Server Addresses
14. Now Type In The Domain Controller IP Address
15. Click OK
16. Now In The Start Search Bar, Search Domain And You Should Get An Option: Access Work Or School
17. Click On Connect
18. Click On Join this device to a local Active Directory domain
19. Now Type

<Root Domain Name>.local

[*] Like: MARVEL.local

20. Now Type User: Administrator And Password: <Your Root Domain Password>. In This Case: P@$$w0rd!
21. Click On OK
22. Click On Skip
23. Now, Reboot
24. Now Instead Of Logging In As The User, Click On Other User And Type Your <User Logon Name>(You Types In Your Domain Controller While Creating Users) And Type Your Password(Again What You Set While Making The User)
25. It May Take A Second To Load
26. Success But We Want To Make Some More Changes
27. Sign Out
28. Now Sign In As <Root Domain Name>\administrator
29. It Will Take A Minute
30. Now Right-Click On The WIndows Logo And Click On Computer Management
31. Click On Local Users And Groups
32. Click On Groups
33. Double-Click On Administrators
34. Click On Add
35. Type The User Logon Name And Click Check Names
36. Click On OK
37. Click On Apply And On OK
38. Now Setup The Other User Machine By Following The Same Steps

[*] After Setting Up The Second User Machine:

[*] Login As Administrator "From The Other Machine". Now Here, You Have To Make The Both Users Administrator

[*] Last Check:

[*] Login To The Server
[*] Goto The Users And Groups(Shown Earlier)
[*] Click On Computers
[*] Click On Refresh And You Should See Both The Computers There. 

[*] Active Directory Build Done!
