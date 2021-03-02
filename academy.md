## Foothold

After basic enumeration I managed to find two pages that stood out to me. I wasn't getting anywhere poking around the site, so I decided to fire up burp and monitor the request when registering a new user. After intercepting the request, I noticed that I was able to modify the request to bypass the login.

![Burp](/academy/images/burp.png)

After forwarding a bunch of requests in burp I was able to login using the user that I created earlier, but instead of the other user, I was able to gain access as the admin. Once I was in I started poking around I noticed that there was a checklist of things that needed to be corrected. At the end of the list, I noticed there was a subdomain that I could access. After navigating to the subdomain the page was filled with tons of information that I needed to enumerate. 

![Academy](/academy/images/academylogin.png)

After enumerating the webpage I found that Laravel was the service hosting everything. After trying to manually exploit it I moved on to Metasploit. There was a single exploit that you could use to get a reverse shell.  

![metasploit](/academy/images/metasploit.png)

## User/Root

The user portion of this box required heavy enumeration. Moreover, I didn't find linpeas to be very helpful for this portion of the box. Information for the user ended up being in an environment file in plain text.

![User](/academy/images/user.png)

The root portion of this box required some heavy enumeration as well. The information that I was seeking ended up being in an audit file. I feel like it was almost luck finding this information. After finding new credentials I switched to the next user who had sudo permissions allowing me to priv esc to root.

![Exploit](/academy/images/rootexploit.png)
![Root](/academy/images/root.png)
