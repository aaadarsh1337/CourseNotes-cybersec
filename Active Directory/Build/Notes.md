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

[*] Boot Up The 2019 Server