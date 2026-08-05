```md

[*] Testing OWASP Top 10 Vulnerabilities

https://owasp.org/www-project-top-ten/

[*] For This, We Will Use Juice Shop
[*] A Useful Checklist:

https://github.com/tanprathan/OWASP-Testing-Checklist

[*] Installing JuiceShop On Your Machine

[*] For This, We Will Need Docker And Juice Shop

https://linuxhint.com/install_docker_kali_linux/

[*] Install Juice Shop Using The Docker Instructions On The Page

https://github.com/bkimminich/juice-shop

[*] We Will Also Solve Challenges On: By What We Have Learned

https://bkimminich.gitbooks.io/pwning-owasp-juice-shop/content/

[*] Installing FoxyProxy(For Burp)

[*] Install The FoxyProxy Extention For Firefox And Lets Configure It

1. Add A Proxy
2. Name It Anything
3. Make The Proxy Type HTTP
4. Proxy IP = 127.0.0.1
5. Port = 8080
6. Close It
7. Click On The Fox
8. Select Burp
9. You Are Done!

[*] Exploring Burp Suite

[*] Watch The Video As It Is Very Practical :-)

[*] The Score Board

[*] There Is A Hidden Score Board By Juice Shop! Lets Navigate There

http://localhost/#/score-board

[*] You Will Get A List Of The Attacks Here. 

[*] Attacking:

[*] SQL Injection

[*] Resource:

https://owasp.org/www-project-top-ten/2017/A1_2017-Injection.html

[*] Common SQL Verbs:

[+] SELECT
[+] INSERT
[+] DELETE
[+] UPDATE
[+] DROP
[+] UNION
[+] WHERE
[+] AND/OR/NOT
[+] ORDER BY

[*] Special Characters

[+] ' , "
[+] --
[+] /*
[+] #
[+] *
[+] %
[+] ;
[+] =
[+] +
[+] <
[+] >
[+] ()

[*] Theory:

[*] Input: Test
[*] SQL: SELECT * FROM Users WHERE email='test'

[*] Injection

[*] Input: Test'
[*] SQL: SELECT * FROM Users WHERE email='Test''

[*] Here, The SQL Synthax Is Incorrect And Should Throw An Error

[*] Malicious Injection

[*] Input: Test
[*] SQL: SELECT * FROM Users WHERE email='test' OR 1=1; --

[*] Here, This Will Make The Statement True And Then The Password Check Will Be Commented
[*] Success!

[*] Defences:

[+] Parameterized Statements
[+] Sanitizing Input

[*] Broken Authentication

https://owasp.org/www-project-top-ten/2017/A2_2017-Broken_Authentication

[*] We Can Check For This Using Burp. Create An Account And Login And You Should See A Token. When You Log Out, It Vanishes. No Broken Authentication...

[*] Sensitive Data Exposure

https://owasp.org/www-project-top-ten/2017/A3_2017-Sensitive_Data_Exposure

[*] Testing:

[*] Gobuster/Dirbuster The Site. Got A Directory Named ftp ! We Get Some Information!
[*] You Should Also Look For Headers

https://securityheaders.com/

[*] NMAP Can Also Be Used For Checking SSL Ciphers

nmap --script=ssl-enum-ciphers -p 443 <Site>

[*] XML External Entities(XXE):

https://owasp.org/www-project-top-ten/2017/A4_2017-XML_External_Entities_(XXE).html

[*] For This, We Will Use Some XML Payloads:

https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XXE%20Injection

[*] We Will Use:

```
```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
  <!DOCTYPE foo [  
  <!ELEMENT foo ANY >
  <!ENTITY xxe SYSTEM "file:///etc/passwd" >]><foo>&xxe;</foo>
```
```md
[*] Bad News: This Cant Be Executed On Our Docker Juice Shop(But We Will Try To Run)

[*] There Is A Complaint Section On The Page Where We Can Upload A File. Lets Intercept The Request And Lets Upload. It Went But Nothing Came Back :-(
[*] If You Want Practical:

https://www.youtube.com/watch?v=xH8WbuApFXw

[*] Broken Access Control

https://owasp.org/www-project-top-ten/2017/A5_2017-Broken_Access_Control.html

[*] Short Meaning: A User Gets Access Of A Place Which He Shouldn't

[*] Practical:

[*] Signup As A Test User And Login. 
[*] Now We Will Submit A Feedback Form But With Another Name!
[*] Right Click And Inspect Element On The Feedback Page
[*] Now There Should Be An Input id Section And The Text Is Hidden. Double Click It And Delete The hidden Part. Hit Enter. We Got A User ID! Change It To 1 For Admin User And We Are Done!

[*] Security Misconfigurations:

https://owasp.org/www-project-top-ten/2017/A6_2017-Security_Misconfiguration.html

[*] Simple Meaning: Misconfigurations In The Websites Security
[*] Ex: Default Credentials Like admin:admin, cisco:cisco, admin:password, admin:password123

[*] Cross Site Scripting(XSS):

https://owasp.org/www-project-top-ten/2017/A7_2017-Cross-Site_Scripting_(XSS).html

[*] Resources:

https://www.scip.ch/en/?labs.20171214
https://xss-game.appspot.com/

[*] There Are Three Main Types:

1. Reflected
2. Stored
3. DOM(We Wont Cover This In This Course)

[*] Reflected(Practical)

[*] We Wont Do This On Juice Shop. We Will Use xss-game

https://xss-game.appspot.com/

[*] The Command:

<script>alert("xss")</script>

[*] Thats It! We Created A Popup

[*] Stored XSS(On JuiceShop):

[*] Location: On Your Account Username Tab
[*] The Command:

<script>a<script>alert("xss")</script>

[*] Here We Added An Extra script a Because The Server Was Filtering It. We Got A Popup!

[*] Defences:

1. Encoding
2. Filtering
3. Validating
4. Sanitation

[*] Insecure Deserialization

https://owasp.org/www-project-top-ten/2017/A8_2017-Insecure_Deserialization.html

[*] Only Reading Stuff. No Practical Attack Works On Juice Shop. :-(

[*] Using Components With Known vulnerabilities

https://owasp.org/www-project-top-ten/2017/A9_2017-Using_Components_with_Known_Vulnerabilities

[*] Again, No Practicals. Just A High Level Overview...

[*] Insufficient Logging And Monitoring

https://owasp.org/www-project-top-ten/2017/A10_2017-Insufficient_Logging%2526Monitoring.html

[*] Not Again :-( No Practical...

[*] OWASP Top 10 Done!
