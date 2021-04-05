[*] Active Directory

[*] Active Directory Is A Service Developed By Microsoft To Manage windows Domain Network

[*] It Stores Information Related To Objects, Such As Computers, Users, Printers, etc. 

[*] Authenticates Using Kerberos Tickets

[*] Active Directory Is The Most Commonly Used Identity Management Service In The World(95%)

[*] Physical Active Directory Components

[*] Domain Controllers:

[*] A Domain Controller Is A Server With The AD DS Server Role Installed That Has Specifically Been Prompted To A Domain Controller

[+] Host A Copy Of The AD DS Directory Store
[+] Provide Authentication And Authorization Services
[+] Replicate Updates To Other Domain Controllers In The Domain And Forest
[+] Allow Administrative Access To Manage User Accounts And Network Resources

[*] The AD DS Data Store:

[+] Consists Of The Ntds.dit File
[+] It Is Stored By Default In The %SystemRoot%/NTDS Folder On All Domain Controllers
[+] Is Only Accessible Through The Domain Controller Processes And Protocols

[*] Logical Active Directory Components

[*] AD DS Schema = RuleBook
[*] Domains = A Domain Which Functions Like Domain Controller(Used For Small Buisnesses)
[*] Tree = Group Of Domains, But They Are Hiearchy. 
[*] Ex.

        contoso.com
         ^       ^
na.contoso.com  emea.contoso.com

[*] Forests = Group Of Trees
[*] Organizational Units(Ous) = Containers For Users, Groups, Computers And Other Ous
[*] Trusts = 

[*] Directional = From Trusting Domain To Trusted Domain
[*] Transitive = Trust Relationship Is Extended Beyond A Two-Domain Trust Include Other Trusted Domains

[*] Objects = 

[*] User
[*] InetOrgPerson
[*] Contacts
[*] Groups
[*] Computers
[*] Printers
[*] Shared Folders