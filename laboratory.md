## Nmap 

![namp](/laboratory/images/nmap.png)

## Foohold

This box was an absloute headache since I wasnt familer with some of the services that were running on the system. I started off by running a basic namp scan. After the scan completed I navigated to the main webpage for enumeration. The site didnt seem to offer much, there wasnt anything usefull in the source either. But I did take not of the comments on the page. It appeared that the CEO "dexter" posted on there. well take note of that for later.

Moving on. After I finished my enumeration on the main webpage I navigated to its subdomain git.laboratory.htb, it dirtcted me to a registration/login page.

![registration](/laboratory/images/register.png)

This was familer to me since another box I was working on had a similar page to the one im on. I pulled up the exploit that I previously used since it was good for multiple version of gitlab. after inputting the proper information I executed the script. It successfully created a revese shell, but this shell was horrific, and I was trapped in the current directory, moreover I couldnt upgrade my current shell. After some poking around I decided to start researching gitlabs since I wasnt familer with the service, I found a few useful things. Turns out your able to change the password of users, so I noted that for later. I rember from the other box that one of the links inside an exploit led to a hackerone post discussing a vulerbility related to this service.

After researching for a bit, I started to mess around witht the commands. I had to spawn a gitlab-rails console inorder to take advantage of the exploit. After I succesfully got the console up and running I attmpted to change the root users password, but that didnt work. This was due to the bad shell that I had. I then went back to reading about the original exploit, it was possible to get a reverse shell through a malicious cookie that needed to be crafted. After attempting to due this exploit multiple times I had to go back to google. I stumbled across and article with someone attempting to do the same thing that I was, but the only difference is that they were using a docker enviorment. After installing docker I started to craft the payload that would be input into the console and return the malcious cookie to me. 

![Rails](/laboratory/images/rails.png)
![payload](/laboratory/images/properpayload.png)
 
Now that I had my cookie I need a way to get onto the box, so I created a bash script that would give me a reverse shell when it was called. After that I started a simple python server in the directoy of my shell and started a listner on the port specifed in the script. 

![Server](/laboratory/images/pythonserver.png)

once I sent a curl request with my cookie to the website my reverse shell was activated. But this didnt mean that I had user yet, I now had a usbale and stable shell to work in. From there I repeated the exploit that I was previosuly attempting to complete, I was able to change D's password. Once their password was changed I could login to their account on the website. 

## User

![Dexter](/laboratory/imagesdexterlogin.png)

Once logined as Dexter I enumerated his account and found a private shh key, I was able to login as him and obtain the user flag.

![User](/laboratory/images/user.png)
