## Foothold

Following a basic enumeration, I found two pages that grabbed my attention. Struggling to make headway with conventional site exploration, I decided to kickstart Burp and keep an eye on the requests while registering a new user. While intercepting the request, I noticed a way to tweak it and sidestep the login process.

![Burp](/academy/images/burp.png)

After forwarding several requests in Burp, I managed to log in using the user I had created earlier. Surprisingly, instead of accessing the regular user account, I found myself with admin privileges. Once inside, I started exploring and came across a checklist pointing out various corrections needed. Towards the end of the list, I discovered a subdomain, leading me to a page with a lot of valuable information that required careful enumeration 

![Academy](/academy/images/academylogin.png)

Upon enumerating the webpage, I identified Laravel as the underlying service hosting the entire system. Despite attempting manual exploits, I eventually turned to Metasploit for assistance. A singular exploit caught my attention, providing a means to establish a reverse shell.  

![metasploit](/academy/images/metasploit.png)

## User/Root

Cracking the user portion of this box involved thorough enumeration. Surprisingly, linpeas wasn't as helpful in this context. I eventually uncovered essential user information conveniently stored in plain text within an environment file.

![User](/academy/images/user.png)

Rooting this box also required thorough enumeration. The information I was after happened to be in an audit file, and finding it felt like a stroke of luck. With the newly acquired credentials, I transitioned to the next user with sudo permissions, paving the way for a privilege escalation to root.

![Exploit](/academy/images/rootexploit.png)
![Root](/academy/images/root.png)
