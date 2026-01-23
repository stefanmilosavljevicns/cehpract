nmap -p- -A -O -sC -sV --script vuln --reason --traceroute -T4 10.10.1.0/24 -oN full_scan.txt

nmap -p 137,389,445 --script smb-os-discovery,ldap-rootdse,nbstat,nbns-lookup 192.168.0.0/24

docker run -d -p 9392:9392 --name openvas immauss/openvas

sudo apt update && sudo apt install -y qterminal zsh curl && chsh -s /bin/zsh && sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

echo '"\e\177": backward-kill-word' >> ~/.inputrc && bind -f ~/.inputrc

echo '"\ed": kill-word' >> ~/.inputrc && bind -f ~/.inputrc
