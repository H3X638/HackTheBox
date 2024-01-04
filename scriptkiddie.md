## Foothold 

The humor of the website truly resonated with the box's name and gave me a good chuckle. Initially, my suspicion was that the vulnerability might involve uploading a file to gain a reverse shell. After conducting some research, my hunch proved correct. I discovered an exploit involving APK file upload using Metasploit. Utilizing Metasploit, I generated a malicious file, successfully uploaded it, and executed a reverse shell.

![payload](/scriptkiddie/images/payload.png)

## User 

After generating the reverse shell and performing a brief enumeration, I discovered that I already had access as the "user" and obtained the user.txt. Identifying another user named "pwn," I assumed that gaining access to them was necessary for reaching root. Further exploration of the box revealed a log file that pwn would visit. Intuitively, I suspected I could leverage this to my advantage. I echoed a bash reverse shell into the log file, successfully obtaining a reverse shell as pwn.

![User](/scriptkiddie/images/user.png)

## Root

Obtaining root access proved to be a fascinating process. Through enumeration, I discovered the possibility of running msfconsole with sudo privileges. Executing it in this manner granted me access to the root directory through the console. Despite encountering numerous errors, the console still listed everything in the root directory, allowing me to retrieve the root flag.

![Root](/scriptkiddie/images/root.png)
