```md

[*] Installing Golang

https://golang.org/doc/install?download=go1.16.3.linux-amd64.tar.gz (Linux, 64Bit)

[*] In The Terminal

tar -xvf <FileName> -C /usr/local

[*] Changing Permission

chown -R root:root /usr/local/go

[*] Changing The Path

nano ~/.profile

[*] Now Add At The Bottom

export GOPATH=$HOME/go
export PATH=$PATH:$GOPATH/bin

[*] Save It And Apply It Using:

. ~/.profile

[*] Now:

echo $PATH

[*] You Should See go In There

[*] Finding Subdomains Using Assetfinder

go get -u github.com/tomnomnom/assetfinder

[*] This Should Install It
[*] Usage:

assetfinder <Target>.com

[*] If You Want Subdomains Only, 

assetfinder --subs-only <Target>.com

[*] Lets Automate It
```
```bash
#!/bin/bash

url=$1

if [ ! -d "$url"];then
    mkdir $url
fi

if [ ! -d "$url/recon"];then
    mkdir $url/recon
fi

echo "[*] Harvesting Subdomains With Assetfinder"
assetfinder $url >> $url/recon/assets.txt
cat $url/recon/assets.txt | grep $1 >> $url/recon/final.txt
rm $url/recon/assets.txt
```
```md
[*] Finding Subdomains Using Amass

https://github.com/OWASP/Amass

[*] Installation Instructions Are Provided On The Github Site
[*] Command:

amass enum -d <Target>.com

[*] Lets Modify The Automate Script
```

```bash
#!/bin/bash

url=$1

if [ ! -d "$url"];then
    mkdir $url
fi

if [ ! -d "$url/recon"];then
    mkdir $url/recon
fi

echo "[*] Harvesting Subdomains With Assetfinder"
assetfinder $url >> $url/recon/assets.txt
cat $url/recon/assets.txt | grep $1 >> $url/recon/final.txt
rm $url/recon/assets.txt

echo "[*] Harvesting Subdomains With Amass"
amass enum -d $url >> $url/recon/f.txt
sort -u $url/recon/f.txt >> final.txt
rm $url/recon/f.txt
```
```md
[*] Finding Alive Domains Using httprobe

https://github.com/tomnomnom/httprobe

[*] Instructions On The Site
[*] Usage:

cat <SubdomainList> | httprobe

[*] Better Usage:

cat <SubdomainList> | httprobe -s | sed 's/https\?:\/\///'

[*] Modified Scripts
```
```bash
#!/bin/bash

url=$1

if [ ! -d "$url"];then
    mkdir $url
fi

if [ ! -d "$url/recon"];then
    mkdir $url/recon
fi

echo "[*] Harvesting Subdomains With Assetfinder"
assetfinder $url >> $url/recon/assets.txt
cat $url/recon/assets.txt | grep $1 >> $url/recon/final.txt
rm $url/recon/assets.txt

echo "[*] Harvesting Subdomains With Amass"
amass enum -d $url >> $url/recon/f.txt
sort -u $url/recon/f.txt >> final.txt
rm $url/recon/f.txt

echo "[*] Probing For Alive Domains"
cat $url/recon/final.txt | sort -u | httprobe -s | sed 's/https\?:\/\///' >> $url/recon/a.txt
sort -u $url/recon/a.txt > $url/recon/alive.txt
rm $url/recon/a.txt
```
```md
[*] Getting Screenshots Using Gowitness

https://github.com/sensepost/gowitness

[*] Installation On Page
[*] Usage:

gowitness single --url=<URL>

[*] Final Modification To Our Script

```bash
#!/bin/bash

url=$1

if [ ! -d "$url"];then
    mkdir $url
fi

if [ ! -d "$url/recon"];then
    mkdir $url/recon
fi

if [ ! -d "$url/recon/screenshots"];then
    mkdir $url/recon/screenshots
fi

echo "[*] Harvesting Subdomains With Assetfinder"
assetfinder $url >> $url/recon/assets.txt
cat $url/recon/assets.txt | grep $1 >> $url/recon/final.txt
rm $url/recon/assets.txt

echo "[*] Harvesting Subdomains With Amass"
amass enum -d $url >> $url/recon/f.txt
sort -u $url/recon/f.txt >> final.txt
rm $url/recon/f.txt

echo "[*] Probing For Alive Domains"
cat $url/recon/final.txt | sort -u | httprobe -s | sed 's/https\?:\/\///' >> $url/recon/a.txt
sort -u $url/recon/a.txt > $url/recon/alive.txt
rm $url/recon/a.txt

echo "[*] Taking Screenshots Of Live Domains"
gowitness file -s $url/recon/alive.txt -d $url/recon/screenshots/
```
```md
[*] This Is Our Final Script But The Cyber Mentor Has Written A Way More Better Script Which Is Here:

https://pastebin.com/MhE6zXVt

[*] I Will Also Add My Script That We Just Wrote To This Repository

[*] Done
