nmap -p- -A -O -sC -sV --script vuln --reason --traceroute -T4 10.10.1.0/24 -oN full_scan.txt

docker run -d -p 9392:9392 --name openvas immauss/openvas
