## Summary:
This is a tutorial for recreate a scan network with nmap and scan vulnerabilities for wordpress and sql

## Description
With two virtual machines, one with Ubuntu (With mysql and wordpress) and other with kali linux, both connected with a intenal network adapter (In a network 10.0.3.0/24). For this exploits it is use nmap.

## Steps To Reproduce:

1. Download, install and power on the kali,ubuntu wordpress and binamiwordpress .ova (links below)
	- Kali.- user:root pass:root
	- Ubuntu.- user:iteso  pass:root.
	- bitnami wordpress.- user:bitnami pass:bitnami
	- If want to use the commands like example use a Network Nat Adapter in Virtual box with DHCP and network 10.0.3.0/24
2. Open firefox in kali and go to 10.0.3.21/wordpress to confirm connection or  10.0.3.22
3.  For all the commands below you will need to open a terminal in kali linux
4. Scan to scanme.nmap.org
	- For see the port, the DNS and the OS use: 
		- nmap -sV -O --system-dns scanme.nmap.org
	- For see if have a firewall use:
		- nmap -sA scanme.nmap.org
	- And if  it say the the service/port if are filtered that means that have firewall
5. Search all host of a network with ping search
	- Use nmap -sn [network]
		- nmap -sn 10.0.3.0/24
6. For see all ip connected to the network
	- Use nmap -sL [network]
		- nmap -sL 10.0.3.0/24
7. For see all services with open ports and their versions
	- Use nmap -A -sV [network]
		- nmap -A -sV 10.0.3.0/24
8. For see all the OS of all hosts
	- Use nmap -O [network]
		- host nmap -O 10.0.3.0/24
9. For make a mysql brute attack 
	- Write nmap --script=mysql-brute [ip]
		- nmap --script=mysql-brute 10.0.3.21
10. For see mysql vulnerabilities 
	- Can try with nmapp --script=mysql-vuln-cve2012-2122 [ip]
		- nmapp --script=mysql-vuln-cve2012-2122 10.0.3.21
11. For see wordpress plugins 
	- Use nmap --script http-wordpress-enum [ip]
		- nmap --script http-wordpress-enum 10.0.3.22
12. For see users of wordpress 
	- Use nmap --script http-wordpress-users [ip]
		- nmap --script http-wordpress-users 10.0.3.22
13. For make a bruteforce attack on wordpress 
	- Use nmap --script http-wordpress-brute [ip]
		- nmap --script http-wordpress-brute 10.0.3.21

<table>
<tr>
    <td>IP</td>
    <td>OS</td>
    <td>Ports</td>
    <td>Services</td>
    <td>Services Version</td>
    <td>Vulnerabilities CVE</td>
    <td>Found Vulnerabilities</td>
</tr>
<tr>
    <td>10.0.3.1</td>
    <td>Not exact OS</td>
    <td>53/tcp</td>
    <td>domain</td>
    <td>Nominium Vantio CacheServe 7.3.0.2</td>
    <td>None</td>
    <td>None</td>
</tr>
<tr>
    <td>10.0.3.2</td>
    <td>Windows</td>
    <td>135,445,2222,8080</td>
    <td>msrpc,microsoft-ds,ethernetIP-1? http-proxy?</td>
    <td>Microsoft Windows RPC, Microsoft Windows 7-10 microsoft-ds</td>
    <td>[Windows RPC] https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=Windows+RPC and for Microsoft CVE-2002-0597 </td>
    <td>None</td>
</tr>
<tr>
    <td>10.0.3.3</td>
    <td>Too many fingerprints</td>
    <td>No one</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>10.0.3.22</td>
    <td>Linux</td>
    <td>22,80,3306</td>
    <td>Open SSH, Apache,mysql</td>
    <td>OpenSSH 8.2p1,Apache httpd 2.4.41,Mysql 5.5.5-10.3.22-MariaDB-1ubuntu1</td>
    <td>For openSSH see https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=OpenSSH+8.2p1 and for apache are CVE-2020-1934,CVE-2020-1927 and for sql see https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=Mysql+5.5.5-10.3.22-MariaDB-1ubuntu1</td>
    <td>None</td>
</tr>
<tr>
    <td>10.0.3.21</td>
    <td>Linux</td>
    <td>22,80</td>
    <td>Open SSH, Apache</td>
    <td>OpenSSH 8.2p1,Apache httpd 2.4.41</td>
    <td>For openSSH see https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=OpenSSH+8.2p1 and for apache are CVE-2020-1934,CVE-2020-1927</td>
    <td>None</td>
</tr>
<tr>
    <td>10.0.3.22</td>
    <td>Debian</td>
    <td>22</td>
    <td>SSH</td>
    <td>No know</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>10.0.3.20</td>
    <td>Linux</td>
    <td>No one</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</table>
## Supporting Material/References:
[Kali and Ubuntu wordpress .ova](https://iteso01-my.sharepoint.com/:f:/g/personal/si721750_iteso_mx/EmWoa89IGO1BsbMddO7j43IBluuqGNmTLKVSD4PIap5IPw?e=moBewg)

[Binami Wordpress machine](https://bitnami.com/stack/wordpress/virtual-machine)

[CVE](https://cve.mitre.org/cve/search_cve_list.html)

[Ubuntu](https://ubuntu.com/)

[Kali](https://www.kali.org/)