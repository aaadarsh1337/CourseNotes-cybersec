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