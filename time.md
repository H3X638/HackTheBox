## Nmap

![Nmap](/time/images/nmap.png)

## Foothold

Upon first visiting the site, my initial thought was that the exploit might involve a lack of sanitization and some malicious code. After experimenting with various inputs, I encountered an error message: "Validation failed: Unhandled Java exception: com.fasterxml.jackson.core.JsonParseException: Unrecognized token 'dsadsa': was expecting ('true', 'false' or 'null')."

A bit of googling led me to several CVEs that could potentially lead to Remote Code Execution (RCE). Now, the task was to find an exploit or some documentation explaining how to leverage this vulnerability. My search for CVE-2019-12384 led me to a GitHub page with a potential method to exploit the target. The repository contained useful links and even a demonstration on how to set everything up.

![CVE](/time/images/CVE.png)

If everything worked as intended, I should be able to achieve Remote Code Execution (RCE) through this exploit. Noting that the demonstration was for local use, I made a few modifications to the payloads to make them suitable for remote exploitation. To make this work, I had to serve a malicious file that would provide me with a reverse shell when executed. 

![Payload](/time/images/payload.png)
![malicious](/time/images/malcious.png)

## User

Once the payload was crafted, I returned to the main website, pasted the payload into the validator, and clicked on validate. As soon as the request went through,I gained  a reverse shell. Minimal enumeration was needed for this box, as upon entry, I already had the user access. 

![User](/time/images/payload.png)

## Root

Gaining root access turned out to be straightforward as well. I identified a file that was run frequently as root, and since I had the ability to write to it, I added my public key to the known hosts. Utilizing SSH, I logged in as root, securing the root access effortlessly.

![Root](/time/images/root.png)

