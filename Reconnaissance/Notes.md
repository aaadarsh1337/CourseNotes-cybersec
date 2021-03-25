# Active Reconnaissance Is Information Gathering Which Is Indirect. Ex. LinkedIn, Facebook, etc.
# Passive Reconnaissance Is Information Gathering Which Is Directly Done On The Sources. Ex. For Tesla, tesla.com

# Email Gathering Can Be Done Using hunter.io

# Data Breaches Happen When The Data Of The Company(Mostly Credentials) Are Leaked Out To The Internet. Heath Adams Has A Good Tool Called Breach Parse Through Which We Can Get Breached Credentials

https://github.com/hmaverickadams/breach-parse

# theharvester Is Another Important Tool Which Even Find Subdomains And Information Of The Target. It Comes Pre-Installed In Kali Linux. 
# Example Command:

theharvester -d <Domain> -l <Number Of Searches> -b <Source>

# Hunting Subdomains Is Very Important During Web-Exploitation. 
# For Example If The Target Is tesla.com, Then There Might Be dev.tesla.com Or admin-login.tesla.com
# sublist3r Is Good For This Purpose
# Example Command:

sublist3r -d <Domain>

# crt.sh Is Good For Certificate FingerPrinting. It Can Use This To Return Subdomains. 
# OWASP Amass Is Another Good Tool. But It Is A Bit Slow. But It Finds Much More Subdomains. 

https://github.com/OWASP/Amass

