echo '"\e\177": backward-kill-word' >> ~/.inputrc && bind -f ~/.inputrc

echo '"\ed": kill-word' >> ~/.inputrc && bind -f ~/.inputrc

sudo apt update && sudo apt install -y cifs-utils && sudo mkdir -p /home/attacker/Desktop/winshare && sudo mount -t cifs "//WIN_IP/SHARE" /home/attacker/Desktop/winshare -o username=WINUSER,password='WINPASS',vers=3.0,uid=$(id -u),gid=$(id -g),iocharset=utf8,file_mode=0777,dir_mode=0777

nmap -p- -A -O -sC -sV --script vuln --reason --traceroute -T4 10.10.1.0/24 -oN full_scan.txt

nmap -p 137,389,445 --script smb-os-discovery,ldap-rootdse,nbstat 192.168.0.0/24

docker run -d -p 9392:9392 --name openvas immauss/openvas
