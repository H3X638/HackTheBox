# Foothold 

After running a few scans came accross a /register and /admin page. I wanted to see the reequest that was being sent when you register a new user, so i fired up Burp. I notied that I could modify a part of the request to bypass the login.

![Burp](/images/burp.png)

After forwarding a bunch of requests in burp I was able to login using the user that I created eariler, but I was logedin as the admin, there was a checklist of things that needed to be done and twoards the end of this list was a sub domain that I had to add to my /etc/hosts file. One I navigated to it I was greeted with a bunch of code and other directories.

![Academy](/images/academylogin.png)

After enumerating the webpage I found that Laravel was the service hosting everything. After trying to manually exploit it I moved on to metasploit. There was a single exploit that you could use to to get a reverse shell. 

![metasploit](/images/metasploit.png)

This box requires heavy enumeration, I dint find linpeas to be all that helpful, the next users information ending being in an enviroment file in plain text

![User](/images/user.png)

After switching to this user again it required hevy enumeration to get to it. The infomartion I was looking for was in the audit direcotry inside an audit file, I have to say I came accross it by luck from trying different grep commands. After that I swited to the next user who had sudo permission for a command that alloud me to priv esc to root.

![Exploit](/images/rootexploit.png)
![Root](/images/root.png)
