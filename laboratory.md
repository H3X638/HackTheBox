## Nmap 

![namp](/laboratory/images/nmap.png)

## Foohold

Dealing with this box turned out to be quite a challenge, particularly due to my unfamiliarity with some of the services running on the system. I kicked things off with a basic Nmap scan, and upon completion, I proceeded to the main webpage for enumeration. Unfortunately, the site itself didn't yield much, and a thorough inspection of the source code didn't reveal anything of value. However, I made a mental note of the comments on the page, particularly a post by the CEO "dexter" - something to keep in mind for later.

Moving forward, after concluding my enumeration on the main webpage, I redirected my focus to its subdomain, git.laboratory.htb, which led me to a registration/login page.

![registration](/laboratory/images/register.png)

Facing a familiar challenge from a previous box, I used a proven GitLab exploit that generated a somewhat limited reverse shell. In my exploration, I discovered GitLab's functionality to change user passwords and recalled a HackerOne post from a previous exploit. Despite attempting to use the gitlab-rails console to change the root user's password, the limitations of my current shell impeded success. Returning to the original exploit, I learned of a potential solution involving a crafted malicious cookie. Multiple attempts proved futile, prompting further research.

While searching online, I found a helpful article detailing a similar situation in a Docker environment. Installing Docker, I crafted a payload to input into the console, successfully obtaining the elusive malicious cookie. 

![Rails](/laboratory/images/rails.png)
![payload](/laboratory/images/properpayload.png)
 
Now armed with my coveted malicious cookie, I created a bash script to trigger a reverse shell upon execution. Subsequently, I initiated a basic Python server in the script's directory and set up a listener on the designated port to establish the connection.

![Server](/laboratory/images/pythonserver.png)

Executing a curl request with my crafted cookie activated the reverse shell, providing me with a stable working environment. However, this didn't grant me user access yet—it merely established a reliable shell. Building on this foundation, I revisited the earlier exploit and successfully changed the password for user "D." With the updated credentials, I logged into their account on the website.

## User

![Dexter](/laboratory/images/dexterlogin.png)

After gaining access as Dexter, I conducted a thorough enumeration of his account and stumbled upon a private SSH key. Leveraging this key, I successfully logged in as Dexter, ultimately obtaining the coveted user flag.

![User](/laboratory/images/user.png)

## Root

Rooting the system turned out to be relatively straightforward compared to the challenges encountered earlier. Along the way, I gained insights into path hijacking, a valuable lesson in itself. I'm inclined to revisit this box in the future, as I sense there's more to learn from it. Overall, it was a rewarding and challenging learning experience, contributing to my growth in this field.

![Root](/laboratory/images/path.png)
