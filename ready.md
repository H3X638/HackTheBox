## Nmap 

![nampg](/ready/images/nmap.png)

## Foothold

I found that getting user was a fun learning experience. It renforced various skills that ive used on previous boxes. I started off by navigating to the website that directed me to a login site, before begining my research I fired up burp to see if I could just bypass the login page. But the site was not vulnerable to this. After some research I found a public  exploit for gitlab, after examing the code to gain a better understaing of the exploit. I created a new user, and used burp tp grab the cookie and authtoken from that session since it was needed in the exploit. In the photos my ports will be different becuase I tried this exploit multiple times and took screen shots at different points, appolgies. 

![Exploit](/ready/images/exploit.png)

## User

Leading off of what I previous said I let up a lister on the port depicted in the picture below. Once I ran the exploit it created a new project in the database containg a malicious payload. Once that went through I successfull generated a reverse shell. After some quick enumeration I leared that I was already "user" I grabbed the flag and continued my enumeration. I saw a directory called root password, but nothing is every that easy.

![User](/ready/images/user.png)

![Stable Shell](/ready/images/stableshell.png)

## Root

Root was realtivly easy, learned about escaping a docker. Turns out that I had root password the whole time, through my enumeration I came accrous while grepping through some config files, but I didnt think much of it untill I gave the box a break and came back to it. After logging in as root I attempted to find the root flag but it wasnt in the root directory. I found this odd, so after a bit of digging around on google I came to the conclusion that I needed to escape the enviorment that I was in. 

![Docker](/ready/images/dockerescape.png)
