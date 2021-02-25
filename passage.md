
layout: page
title: "HTB Passage"
permalink: /passage/

# Enumeration 

![CuteNews](/passage/images/CuteNews.png)

Enumeration for the website was a bit odd. I wasnt avle to run any scans. The only scan that I was able to use was Nmap and that only told me that there was a server running on port 80. It turns out that if you ran and excissive scans on the netwrok it would boot you off for 2 mins. After further enumeration I found that website was being hosted by CuteNews. It just so happened that the login pages was located at 10.10.10.206/CuteNews. From the login page I was able to find the version of CuteNews (2.1.2) there was an RCE exploit that I attempted to use, but I ran into an issue with the padding in the code, and couldnt quite figure out how to get around that. But from what I under stood we created a new user and are able to upload a malicious file as their profile picture. Eventually I settled on using metasploit that alloud me to get a shell on the system as wwwdata.

![Foothold](/passage/images/foothold.png)

## Priv Esc. 

After poking around the box and getting nowhere. Decided to start enumeration of the website internally. Made my way to the users direcotry and started to input all the direcotries into the url. Finally came acros a direcotry that had a bunch of things encoded in base64. after trasfering the info over to cyberchef i found a user paul that matches up with the /etc/passwd user paul. Their login info was inside the info decoded in base 64 aswell.

![etcpassword](/passage/images/etcpasswd.png)
![lines](/passage/images/lines.png)
![Paul](/passage/images/paulspassword.png)

# Priv Esc. PT2

This was an absloute facepalm. It was sitting there in front of me the whole time. It turns out that paul and nadav share everthing. including ssh. During enumeration I took a peek at a hiddend ssh directory and saw that their was one key in authorized keys that belonged to  Nadav.  I took pauls private key and used ssh to log into is account from their I used ssh to loginto nadav, didnt require a password since they were known hosts. 

![RSA Key](/passage/images/rsakey.png)
![SSH Paul](/passage/images/paulssh.png)
![SSH Nadav](/passage/images/nadav.png)

# Root

Root was a brain buster. The whole box seems to be based around ssh. Long story short used dbus to create or copy a rsa key over from the root dircotry. Was then able to login as root with no password. I learned some new stuff from this box that I will be keeping in my back pocket, enumeration is alwyas key. overall very fun box. 

![dbus](/passage/images/dbus.png) 
![root](/passage/images/root.png)
