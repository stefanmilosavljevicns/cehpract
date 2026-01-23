echo '"\e\177": backward-kill-word' >> ~/.inputrc && bind -f ~/.inputrc

echo '"\ed": kill-word' >> ~/.inputrc && bind -f ~/.inputrc

sudo nano /etc/fstab

//172.25.0.11//WINDOWS11/Users/Admin/Desktop/Share /home/attacker/Desktop/Share cifs credentials=/etc/smb-credentials,vers=3.0,uid=1000,gid=1000,iocharset=utf8,_netdev 0 0


nmap -p- -A -O -sC -sV --script vuln --reason --traceroute -T4 10.10.1.0/24 -oN full_scan.txt

nmap -p 137,389,445 --script smb-os-discovery,ldap-rootdse,nbstat 192.168.0.0/24

docker run -d -p 9392:9392 --name openvas immauss/openvas
