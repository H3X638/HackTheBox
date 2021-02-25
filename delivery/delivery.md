# Foothold

Ran an Nmap scan along with a gobuster scan. The gobuster scan didnt give me anything usefull, the nmap scan showed that there was a something running on a higher port. I decided to poke around the website, there were a few different links, one of them ended up brining me to a help desk section where you could submit a ticket. My original thought was that I could upload a malicious attachment to my ticket, but that turned out to be a dead end. After Futher enumeartion I came across a mattersmost loginpage, i remembered that in the source code of the page there was a section mentioning that once you register youll get access to the website. I did just that. I went and created a new user with and register with a random email edning in @delivery.htb. Then submitted a help ticket requesting that my email be register. After regreshing the page I was provided with a link to activate my account. Once I was inside, there were varrious post containing information about credentials. The first set of credentials I chose alloud to the ssh in as maildeliverer.

![Registration.png](/delivery/images/registration.png)

![SSH](/delivery/images/user.png)

## Priv Esc.

After enumerating maildeliverer I found that I was able to cat the mysql.conf file that cointed the password for mysql. Once i had access to mysql I took a look at the databases and pull all the user information from it. 

![SQL](/delivery/images/sqlsettings)

![SQL-Login](/delivery/images/sqllogin.png)


