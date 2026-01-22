nmap -p- -A -O -sC -sV --script vuln --reason --traceroute -T4 10.10.1.0/24 -oN full_scan.txt

nmap -p 137,389,445 --script smb-os-discovery,ldap-rootdse,nbstat,nbns-lookup 192.168.0.0/24

docker run -d -p 9392:9392 --name openvas immauss/openvas
