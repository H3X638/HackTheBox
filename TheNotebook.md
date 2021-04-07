## TheNotebook

## Enumeration
 
![namp](/TheNotebook/images/nmap.png)

My inital scan shows that SSH and HTTP are running on the target along with another service running on a highport. After doing basic enumeration on the website I found nothing of intrest that could lead me twords a foothold on the target. The site itsself didnt really provide anything super usefull either. There was just a login and regisregister page. 

![login](/TheNotebook/images/login.png)

I created an account and poked around for a bit. There was a notes section where you could uploads your thoughts. I tired various attacks against this section but nothing ended up working. There were a few pages that were forbidden so I fired up Burp to see what was going on. After intercepting the request it appeared that there was some sort of auth token that was base64 encoded.

![cookie](/TheNotebook/images/cokie.png)

 Next step was to copy and decode it using cyber chef. After decoding it the majority of it was jibberish, but the first and second line were in plaintext, it showed me that it was a JWT token using RSA256, and the second line consisted of the payload.

## Foothold

After some research, I found that I could create my own token and gain admin access to the website. But first I needed to generate a private and public RSA key. I just used a website for this. They keys that I used are in the git repo for this blog if you want to take a look. You can use jwt.io to decode and modify the JWT token. 

![jwt](/TheNotebook/images/jwt.png)

I modified the header to contain my ip, and changed "admin cap" to 1 to grant admin privlage. After that I added in my public and prive keys and generated my new token. Once that was done I used burp to forward the new token and noted that I now saw an Admin panel on my navigation bar. But I needed to use a cookie modifer to keep the session active otherwise id have to keep forwarding my burp request. After poking around there was a section to upload a file to the server, I uploaded a php revershell, and now have a foot hold on the target. 
![foothold](/TheNOtebook/images/foothold.png)

## Privilege escalation

User didnt require much enumeration, I used linpeas to do some quick enumeration of the system. After looking through it, I found a backup home folder for the user noah. Once inside the folder I was able to grab the private key and ssh in as noah.

![user](/TheNotebook/images/user.png)

Root didnt require much either. You had to escape a docker enviorment, ive done this once before on another box but the escape method was different. After some research I found an exploit and modified the payload to get a reverse shell with root access.

![exploit](/TheNotebook/images/exploit.png)

![root](/TheNotebook/images/root.png)
