## Summary:
This is a tutorial in which I recreate 3 attacks on an ubuntu machine with DVWA

## Description
With two virtual machines, one with Ubuntu and DVWA and other with kali linux, both connected with a intenal network adapter (In a network 100.100.1.0/24). For this exploits I use BurpSuite as proxy request, nmap for scan, hydra for bruteforce and sqlmap for sql exploit.

## Steps To Reproduce:

  1. Download, install and power on the kali and Ubuntu ova from below.
   - Kali.- user:root pass:root  
   - Ubuntu.- user:iteso  pass:123456.
  2. Open a terminal in kali and use 'nmap 100.100.1.3' to confirm connection. 
  3. Open firefox and go to 100.100.1.3 and use username:admin pass:password to access.
  4. Go to DVWA security tab and set security to low.
  5. Perform SQL injection attack.
     1. Go to firefox connection settings and change to manual proxy '127.0.0.1' and port 8080
     2. Open BurpSuite and go to proxy tab then that in options have the same proxy that puts in firefox.
     3. Go to 100.100.1.3/vulnerabilities/sqli/
     4. Active intercept in burp.
     5. In user ID:put 1 and forward until you see your submit.
     6. Open a terminal and with the things that you get from burp write: sqlmap -u 'http://100.100.1.3/vulnerabilities/sqli/?id=1&Submit=Submit' --cookie= (puts the cookie here)' --string=Surname -D dvwa -T users -C user,password --dump
     7. Now you have the username and encripted password.
  6. Perform BruteForce attack
     1. With the same proxy conf
     2. Go to 100.100.1.3/vulnerabilities/brute/
     3. Active intercept in burp
     4. Go back to firefox and put the username that get previously [admin] and any password
     5. Go back to burp and forward until you see the username and password yo put
     6. Open a terminal and write: hydra 100.100.1.3 -l admin -P /usr/share/wordlists/rockyou.txt.gz http-get-form "/vulnerabilities/brute/index.php:username=^USER^&password=^PASS^&Login:Username and/or password incorrect.: H=Cookier: (And puts the cookie that gets in burp)"
     7. Now you have the password
  7. Perform Upload Vulnerability
     1. Again with the same proxy conf
     2. Go to 100.100.1.3/vulnerabilities/upload/
     3. Create a file and write there a scrip or something and name it like [name].html.jpg
     4. Active intercept in burp
     5. Browse the file and click in upload
     6. Go to burp and forward until you see your upload
     7. There change the name of the file to [name].html and forward
     8. Now you have uploaded the file

## Supporting Material/References:
[[Virtual Machines .ova]](https://iteso01-my.sharepoint.com/:f:/g/personal/si721750_iteso_mx/EmWoa89IGO1BsbMddO7j43IBluuqGNmTLKVSD4PIap5IPw?e=moBewg)

[sqlmap](http://sqlmap.org/)

[nmap](https://nmap.org/)

[BurpSuite](https://portswigger.net/burp)

[Hydra](https://github.com/vanhauser-thc/thc-hydra) 

[Ubuntu](https://ubuntu.com/)

[DVWA](http://www.dvwa.co.uk/)

[Kali](https://www.kali.org/)

