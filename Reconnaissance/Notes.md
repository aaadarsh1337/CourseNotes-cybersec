#Active Reconnaissance Is Information Gathering Which Is Indirect. Ex. LinkedIn, Facebook, etc.
#Passive Reconnaissance Is Information Gathering Which Is Directly Done On The Sources. Ex. For Tesla, tesla.com

Passivce Reconnaissance:

#Email Gathering Can Be Done Using hunter.io

#Data Breaches Happen When The Data Of The Company(Mostly Credentials) Are Leaked Out To The Internet. Heath Adams Has A Good Tool Called Breach Parse Through Which We Can Get Breached Credentials

https://github.com/hmaverickadams/breach-parse

#theharvester Is Another Important Tool Which Even Find Subdomains And Information Of The Target. It Comes Pre-Installed In Kali Linux. 
#Example Command:

theharvester -d <Domain> -l <Number Of Searches> -b <Source>

#Hunting Subdomains Is Very Important During Web-Exploitation. 
#For Example If The Target Is tesla.com, Then There Might Be dev.tesla.com Or admin-login.tesla.com
#sublist3r Is Good For This Purpose
#Example Command:

sublist3r -d <Domain>

#crt.sh Is Good For Certificate FingerPrinting. It Can Use This To Return Subdomains. 
#OWASP Amass Is Another Good Tool. But It Is A Bit Slow. But It Finds Much More Subdomains. 

https://github.com/OWASP/Amass

#Identifing Website Technology Is Also Important. 
#builtwith Is A Good Website For Such Pupose

https://builtwith.com

#Wappalyzer Is Another Great Tool(Firefix Extension)
#whatweb Is Also Good(Built-In In Kali Linux)

whatweb https://tesla.com

#In Web-App Peneteration Testing, Burp-Suite Is Very Useful. It Comes Pre-installed In Kali Linux
#Using Burp:

1. Open Burp
2. Open Firefox
3. Go To Preferences
4. Goto To Proxy Setting
5. Ip = 127.0.0.1
6. Port = 8080
7. Goto https://burp
8. Download The CA Certificate
9. Goto Certificates In Firefox
10. Import The File
11. Check Both The Boxes
12. Goto Proxy Tab In Burp
13. Try Intercept
14. Goto Target Tab
15. Goto Site-Map Tab
16. Get Your Information!

#Use Google Dorking Or Google Fu
#Google: google search syntax
#You Will Find Good Resources
#Examples:

filetype:docx
site:tesla.com
intext:login

#There Are Other Syntaxes Too. 

#Social Media Is Very Useful For Passive Reconnaisance. 
#Just Start Playing With Social Media Sites Which Your Target Might Be Using. You Will Get Some Information. 

Active Reconnaissance:

#Choose A Target You Own. 
#I Am Using Kioptrix

https://tcm-sec/kioptrix

#Set It Up In VM-Ware Or VirtualBox

#Start Using NMAP
#Example Command

nmap <IP>

#It's A Basic Scan
#More Advanced Scan:

nmap -sC -sV -A -vv <IP> -oN nmap/initial

#-sC Runs Default Scans
#-sV Will Detect Service Versions
#-A Will Perform Agressive Scan Which Will Also Detect OS
#-O To Just Detect OS
#-vv Is Just Very Verbose
#-oN Will Output The Scan Results
#-p- Will Scan All Ports
#-T4 Runs 4 Threads And Is Best As Its Fast
#-Pn Blocks Ping
#You Can Always Run 'nmap --help' or 'man nmap' For All Syntaxes

#Common TCP Ports:

22 = ssh
80 = http
21 = ftp
23 = telnet
139 And 445 = smb
443 = https/ssl

#Enumerating http Or https:

#Nikto Is A Great Tool For Vulnerablity Scanning
#Example Command

nikto -h <http://Host>

#Directory Listing Is Very Important
#Gobuster And Dirbuster Are Good Tools Out There. 
#Dirbuster Is Pre-Installed In Kali. Gobuster Can Be Installed:

git clone https://github.com/OJ/gobuster
Or
sudo apt-get install gobuster

#Gobuster Example Usage:

gobuster dir -u <http://Host> -w <Your Wordlist's Path> -x <Extensions>

#Common Status Codes:

200 = Ok
400 = Error(Mostly 404)
300 = Redirect
500 = Server Error

#Enumerating SMB:

#You Can Use MetaSploit To Find SMB Version But We Can Get It Using

nmap -sV <IP>

#Usage:

smbclient -L \\\\<IP>\\

#May Lead To File Share Listsing

#Enumerating SSH:

ssh <IP>

#To Find Vulnerabilities, Just GOOGLE The Version Number Exploit!

#Addinational Scanning Tools:

masscan -p1-65535 <IP>

#Metasploit Can Also Be Used. 
#Nessus Is Another Tool
#Download Nessus From Google

dpkg -i <Filename>

#This Will Install It And Follow The Screen Instructions To Go Ahead. 
