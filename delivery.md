# Foothold

Ran a Nmap scan along with a gobuster scan. The gobuster scan didn't give me anything useful, the nmap scan showed that there was something running on a higher port. I decided to poke around the website, there were a few different links, one of them ended up bringing me to a help desk section where you could submit a ticket. My original thought was that I could upload a malicious attachment to my ticket, but that turned out to be a dead end. After further enumeration I came across a mattersmost login page, I remembered that in the source code of the page there was a section mentioning that once you register you'll get access to the website. I created a new user and register with a random email ending in @delivery.htb. Then submitted a help ticket requesting that my email be registered. After refreshing the page I was provided with a link to activate my account. Once I was inside, there were various post containing information about credentials. The first set of credentials I chose allowed me to ssh in as maildeliverer.


![Registration.png](/delivery/images/registration.png)

![SSH](/delivery/images/user.png)

## Priv Esc.

After enumerating maildeliverer I found that I was able to cat the mysql.conf file that contained the password for mysql. Once i had access to mysql I took a look at the databases and was able to pull all the user information from it. 

![SQL](/delivery/images/sqlsettings.png)

![SQL-Login](/delivery/images/sqllogin.png)

## Root

Root was super simple, there was a hint eariler on the website that stated we shouldnt use RockYou and that if we got the hases we could use hashcat to get the password. I extracted the hash from the data base via mysql. And ran it through hashcat to get the password.

![Hashcat](/delivery/images/hashcat.png)
