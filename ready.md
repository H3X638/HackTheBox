## Nmap 

![nampg](/ready/images/nmap.png)

## Foothold

Obtaining user access proved to be an enjoyable learning experience, reinforcing various skills acquired from previous boxes. I initiated the process by navigating to the website, which redirected me to a login page. In an attempt to expedite the process, I fired up Burp to check for potential login page bypass vulnerabilities, but the site proved resilient.

After conducting research, I stumbled upon a public exploit for GitLab. Upon closer examination of the code to gain a comprehensive understanding, I created a new user. Using Burp, I captured the cookie and auth token from this session, as they were essential for the exploit. Please note that the port numbers may differ in the screenshots due to multiple attempts at the exploit. Apologies for any confusion.

![Exploit](/ready/images/exploit.png)

## User

Building on my earlier steps, I set up a listener on the port depicted in the picture below. Executing the exploit resulted in the creation of a new project in the database, housing a malicious payload. This successful execution led to the generation of a reverse shell. A brief round of enumeration revealed that I already had access as the "user." I swiftly retrieved the flag and continued exploring.

Encountering a directory named "root password," I knew that things are rarely as straightforward as they seem.

![User](/ready/images/user.png)

![Stable Shell](/ready/images/stableshell.png)

## Root

Root access turned out to be relatively straightforward as I learned about escaping a Docker environment. Interestingly, I had the root password all along, as I discovered during my enumeration by grepping through some config files. Initially, I didn't pay much attention to it, but after taking a break and returning to the box, it clicked.

After logging in as root, I attempted to locate the root flag, but it wasn't in the root directory, which struck me as odd. A bit of research on Google led me to the conclusion that I needed to escape the environment I was in.

![Docker](/ready/images/dockerescape.png)
