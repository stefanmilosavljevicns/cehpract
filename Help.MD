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

docker run -d -p 9392:9392 --name openvas immauss/openvas


//DNS

dnsrecon -d site.com -a


//HYDRA

hydra -l /putanja-do-username-a -P /putanja-do-sifri ftp://<ip-adresa>



//KERBEROS ROASTING sa impacket-om

python3 GetNPUsers.py CEH.com/ -no-pass -usersfile /root/ADtools/users.txt -dc-ip 10.10.1.22.
