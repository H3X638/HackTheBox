## Nmap 

![namp](/laboratory/images/nmap.png)

## Foohold

This box was an absolute headache since I wasn't familiar with some of the services that were running on the system. I started off by running a basic Nmap scan. After the scan completed I navigated to the main webpage for enumeration. The site didn't seem to offer much, there wasn't anything useful in the source either. But I did take note of the comments on the page. It appeared that the CEO "dexter" posted on there. well, take note of that for later.

Moving on. After I finished my enumeration on the main webpage I navigated to its subdomain git.laboratory.htb, it directed me to a registration/login page.
![registration](/laboratory/images/register.png)

This was familiar to me since another box I was working on had a similar page to the one I'm on. I pulled up the exploit that I previously used since it was good for multiple versions of gitlab. after inputting the proper information I executed the script. It successfully created a reverse shell, but this shell was horrific, and I was trapped in the current directory, moreover, I couldn't upgrade my current shell. After some poking around I decided to start researching gitlabs since I wasn't familiar with the service, I found a few useful things. Turns out you have the ability to change the password of users, so I noted that for later. I remember from the other box that one of the links inside an exploit led to a hackerone post discussing a vulnerability related to this service.

After researching for a bit, I started to mess around with the commands. I had to spawn a gitlab-rails console in order to take advantage of the exploit. After I successfully got the console up and running I attempted to change the root user's password, but that didn't work. This was due to the bad shell that I had. I then went back to reading about the original exploit, it was possible to get a reverse shell through a malicious cookie that needed to be crafted. After attempting to do this exploit multiple times I had to go back to google. I stumbled across an article with someone attempting to do the same thing that I was, but the only difference is that they were using a docker environment. After installing docker I started to craft the payload that would be input into the console and return the malicious cookie to me. 

![Rails](/laboratory/images/rails.png)
![payload](/laboratory/images/properpayload.png)
 
Now that I had my cookie I need a way to get onto the box, so I created a bash script that would give me a reverse shell when it was called. After that, I started a simple python server in the directory of my shell and started a listener on the port specified in the script. 

![Server](/laboratory/images/pythonserver.png)

once I sent a curl request with my cookie to the website my reverse shell was activated. But this didn't mean that I had user yet, I now had a stable shell to work in. From there I repeated the exploit that I was previously attempting to complete, I was able to change D's password. Once their password was changed I could log in to their account on the website. 

## User

![Dexter](/laboratory/images/dexterlogin.png)

Once logined as Dexter I enumerated his account and found a private shh key, I was able to login as him and obtain the user flag.

![User](/laboratory/images/user.png)

## Root

Root was easy compared to the rest of the box, I leared about path hyjacking during this process. Im deffiently going to have to come back and re visit this box in the future. I fell that there still is more that I can learn from this box. Overall was a fun and challenging learning experience. 

![Root](/laboratory/images/path.png)
