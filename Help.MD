echo '"\e\177": backward-kill-word' >> ~/.inputrc && bind -f ~/.inputrc

echo '"\ed": kill-word' >> ~/.inputrc && bind -f ~/.inputrc

sudo mkdir -p /home/attacker/Desktop/Windows-File-Transfer && echo -e "username=Admin\npassword=WINDOWS_PASSWORD" | sudo tee /etc/smb-credentials >/dev/null && sudo chmod 600 /etc/smb-credentials
//172.25.0.11/Share /home/attacker/Desktop/Windows-File-Transfer cifs credentials=/etc/smb-credentials,vers=3.0,uid=1000,gid=1000,iocharset=utf8,_netdev 0 0
sudo mount -a

//172.25.0.11/C:\Users\Admin\Desktop\Share /home/attacker/Desktop/Share cifs credentials=/etc/smb-credentials,vers=3.0,uid=1000,gid=1000,iocharset=utf8,_netdev 00 I


nmap -p- -A -O -sC -sV --script vuln --reason --traceroute -T4 10.10.1.0/24 -oN full_scan.txt

nmap -p 137,389,445 --script smb-os-discovery,ldap-rootdse,nbstat 192.168.0.0/24

docker run -d -p 9392:9392 --name openvas immauss/openvas
