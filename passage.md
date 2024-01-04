## Enumeration 

![CuteNews](/passage/images/CuteNews.png)

The enumeration process for the website presented some challenges. Running scans proved difficult, with only Nmap providing information about a server on port 80. I discovered that excessive scans on the network would result in a temporary ban for two minutes. Further investigation revealed that the website was hosted by CuteNews, and its login pages were located at 10.10.10.206/CuteNews. Identifying the CuteNews version as 2.1.2, I attempted an RCE exploit, but encountered issues with the padding in the code, struggling to find a workaround.

Ultimately, I opted for using Metasploit, which allowed me to gain a shell on the system as wwwdata.

![Foothold](/passage/images/foothold.png)

## Priv Esc. 

Facing a dead end on the box, I shifted my focus to internal website enumeration. Navigating to the user's directory, I systematically input various directories into the URL. Eventually, I stumbled upon a directory containing encoded information in base64. After transferring the data to CyberChef for decoding, I uncovered details about a user named Paul, aligning with the /etc/passwd user list. The decoded information also included login credentials for Paul.

![etcpassword](/passage/images/etcpasswd.png)
![lines](/passage/images/lines.png)
![Paul](/passage/images/paulspassword.png)

## Priv Esc. PT2

Sometimes the solution is right in front of us. In a moment of realization, I discovered that Paul and Nadav shared everything, including their SSH keys. While exploring, I took a closer look at a hidden SSH directory and found a key in the authorized keys file belonging to Nadav. Using Paul's private key, I successfully logged into Paul's account using SSH. From there, I leveraged SSH again to access Nadav's account, as it didn't require a password due to being in the known_hosts file.

![RSA Key](/passage/images/rsakey.png)
![SSH Paul](/passage/images/paulssh.png)
![SSH Nadav](/passage/images/nadav.png)

## Root

Root was a brain buster. The whole box seems to be based around ssh. Long story short used dbus to create or copy a rsa key over from the root dircotry. Was then able to login as root with no password. I learned some new stuff from this box that I will be keeping in my back pocket, enumeration is alwyas key. overall very fun box. Rooting the box turned into a bit of a brain teaser. The entire challenge seemed to revolve around SSH. In a nutshell, I utilized dbus to either create or copy an RSA key from the root directory, allowing me to log in as root without requiring a password. This experience taught me some valuable new techniques that I'll be sure to keep in my toolkit. As always, the importance of thorough enumeration became clear. Overall, a very enjoyable and educational box.

![dbus](/passage/images/dbus.png) 
![root](/passage/images/root.png)
