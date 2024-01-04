# Foothold

I initiated a Nmap scan alongside a gobuster scan. While the gobuster results proved unfruitful, the Nmap scan revealed activity on a higher port. Intrigued, I explored the website, discovering several links, one of which led me to a help desk section where tickets could be submitted. Initially, I considered uploading a malicious attachment to my ticket but hit a dead end. Further enumeration led me to a Mattermost login page. Recalling a snippet in the page's source code suggesting access upon registration, I created a new user using a random email ending in @delivery.htb. I submitted a help ticket requesting email registration and, upon refreshing the page, received a link to activate my account.

Once inside, I found numerous posts containing valuable information, including credentials. Opting for the first set of credentials, I successfully SSHed in as "maildeliverer."


![Registration.png](/delivery/images/registration.png)

![SSH](/delivery/images/user.png)

## Priv Esc.

Upon enumerating "maildeliverer," I discovered the ability to access the "mysql.conf" file and retrieve the password for MySQL. With MySQL access secured, I delved into the databases, extracting comprehensive user information. 

![SQL](/delivery/images/sqlsettings.png)

![SQL-Login](/delivery/images/sqllogin.png)

## Root

Rooting the system proved surprisingly straightforward. An earlier hint on the website cautioned against using RockYou and suggested utilizing hashcat if the hashes were obtained. Extracting the hash from the database through MySQL, I ran it through hashcat, successfully obtaining the password.

![Hashcat](/delivery/images/hashcat.png)
