## Nmap

![Nmap](/time/images/nmap.png)

## Foothold

The first thing that popped into my head when I first visited the site was ill the exploit has to do with a lack of sanitization and some malicious code. After trying various inputs I managed to get an error. 

"Validation failed: Unhandled Java exception: com.fasterxml.jackson.core.JsonParseException: Unrecognized token 'dsadsa': was expecting ('true', 'false' or 'null')". 

Took a bit of googling but I found a few CVE's that possible could lead to RCE, now I just needed to find and exploit or something explaining how to utilize this vulnerability. Searching for CVE-2019-12384 lead me to a GitHub page with a possible way to exploit the target. The repo had some useful links, even a demonstration on how to set everything up.

![CVE](/time/images/CVE.png)

If everything worked properly I should be able to get RCE from this. I noted that they were demonstrating how to use the exploit locally, so I had to do a few modifications to the payloads for it to work properly. For this, to work I had to serve up a malicious file that would give me a reverse shell when its executed.  

![Payload](/time/images/payload.png)
![malicious](/time/images/malcious.png)

## User

once the payload was crafted I went back to the main website and pasted the payload into the validator, and clicked on validate. Once the request went through I had a reverse shell. Didn't need to do much enumeration for this box. Once I was in I was already the user.  

![User](/time/images/payload.png)

## Root

Root was super easy aswell, I could write to a file that was run frequently as root. So I added my public key to known hosts and used ssh to login as root. 

![Root](/time/images/root.png)

