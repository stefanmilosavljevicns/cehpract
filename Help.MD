//Config Parrot-a


#1#


sgpt "Analiziraj ovaj nmap output i reci mi najbitnije nalaze" <<< "$(cat full_scan.txt)"

curl -fsSL https://raw.githubusercontent.com/stefanmilosavljevicns/cehpract/main/secret.txt.gpg -o /tmp/secret.txt.gpg && export $(gpg -d /tmp/secret.txt.gpg) && rm -f /tmp/secret.txt.gpg && mkdir -p ~/.config/shell_gpt && sed -i 's/^DEFAULT_MODEL=.*/DEFAULT_MODEL=gpt-4o-mini/' ~/.config/shell_gpt/.sgptrc 2>/dev/null || echo 'DEFAULT_MODEL=gpt-4o-mini' >> ~/.config/shell_gpt/.sgptrc

#2#


echo '"\e\177": backward-kill-word' >> ~/.inputrc && bind -f ~/.inputrc && echo '"\ed": kill-word' >> ~/.inputrc && bind -f ~/.inputrc && apt install -y cifs-utils

//Ako bude problema
smbclient -L //172.25.0.11 -U Admin

echo -e "username=Admin\npassword=Pa$$w0rd" | sudo tee /etc/smb-credentials >/dev/null && sudo chmod 600 /etc/smb-credentials

echo "//172.25.0.11/Users/Admin/Desktop/Share /home/attacker/Desktop/Share cifs credentials=/etc/smb-credentials,vers=3.0,uid=1000,gid=1000,iocharset=utf8,_netdev 0 0" | sudo tee -a /etc/fstab  && sudo mount -a && systemctl daemon-reload

________________________________________________________________
//NMAP

nmap -p- -A -O -sC -sV --script vuln --reason --traceroute -T4 10.10.1.0/24 -oN full_scan.txt

nmap -p 137,389,445 --script smb-os-discovery,ldap-rootdse,nbstat 192.168.0.0/24

nmap -sS -sV -p- <IP> -oN results.txt

docker run -d -p 9392:9392 --name openvas immauss/openvas


//DNS

dnsrecon -d site.com -a


//HYDRA

hydra -l /putanja-do-username-a -P /putanja-do-sifri ftp://<ip-adresa>



//KERBEROS ROASTING sa impacket-om

python3 GetNPUsers.py CEH.com/ -no-pass -usersfile /root/ADtools/users.txt -dc-ip 10.10.1.22.

john --wordlist=/home/attacker/rockyou.txt hashes.txt

//Analiza fajlova

file <path do fajla> // cesto ce lagati za ekstenziju

virustotal.com -> dobar za analizu .exe fajlova 

https://github.com/horsicq/DIE-engine/releases/download/3.10/die_3.10_Parrot_5.3_amd64.deb DIE

//STEG

steghide extract -sf stealth.jpeg -p sifra@123

//VULN Scan
OpenVas ali i OWASP Zap radi posao sasvim ok

//Aircrack
1. aircrack-ng capture.pcap
2. aircrack-ng -w rockyou.txt capture.pcap


# Crypto 

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
| admin:password                  | Credentials (plain) | Već čitljivo                             | N/A                          | Nema potrebe za decode                    |
