nmap -p- -A -O -sC -sV --script vuln --reason --traceroute -T4 10.10.1.0/24 -oN full_scan.txt
