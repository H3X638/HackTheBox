## Foothold 

This website gave me a good chuckle. Truly relates to the name of the box. At first glance I thought that the vulerability would be uploading afile to get a reverse shell. After a bit of research my hunch turn out to be correct. There was an exploit with apk file upload using metasploit. Metasploit generated a malicious file that I was able to upload and generate a reverse shell with. 

![payload](/scriptkiddie/images/payload.png)

## User 

After generating the reverse shell and some quick enumeration, I discorder that I was already "user" and was able to gain access to the user.txt. There was another user called pwn, I assumed that I had to gain access them inorder to gain root. After furter enumerating the box I found that there was a log file that pwn would visit. I had a hunch that I could use this to my advantage. I echoed a bash reverse shell into the log file and got a reverse shell as pwn.

![User](/scriptkiddie/images/user.png)

## Root

Root was super cool. Through enumeration I found that its possible to run msfconsole with sudo. Since I ran it as sudo I was able to access the root direcotry through the console, even though it gave me a ton of erros it would still list everything in root allowing me to grab to flag. 

![Root](/scriptkiddie/images/root.png)
