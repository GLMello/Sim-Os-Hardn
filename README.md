<h1>Simulation - Applying OS hardening techniques</h1>

 ### You can also read this in: [Português](https://github.com/GLMello/Prot-So-Sim)

<h2>Description</h2>
This simulation puts me in the shoes of a cybersecurity analyst responsible for investigating and documenting a security issue that website visitors reported.

<br />


<h2>Scenario</h2>
You are a cybersecurity analyst for yummyrecipesforme.com, a website that sells recipes and cookbooks. A disgruntled baker has decided to publish the website’s best-selling recipes for the public to access for free. 

The baker executed a brute force attack to gain access to the web host. They repeatedly entered several known default passwords for the administrative account until they correctly guessed the right one. After they obtained the login credentials, they were able to access the admin panel and change the website’s source code. They embedded a javascript function in the source code that prompted visitors to download and run a file upon visiting the website. After running the downloaded file, the customers are redirected to a fake version of the website where the seller’s recipes are now available for free.

Several hours after the attack, multiple customers emailed yummyrecipesforme’s helpdesk. They complained that the company’s website had prompted them to download a file to update their browsers. The customers claimed that, after running the file, the address of the website changed and their personal computers began running more slowly. 

In response to this incident, the website owner tries to log in to the admin panel but is unable to, so they reach out to the website hosting provider. You and other cybersecurity analysts are tasked with investigating this security event.

To address the incident, you create a sandbox environment to observe the suspicious website behavior. You run the network protocol analyzer tcpdump, then type in the URL for the website, yummyrecipesforme.com. As soon as the website loads, you are prompted to download an executable file to update your browser. You accept the download and allow the file to run. You then observe that your browser redirects you to a different URL, greatrecipesforme.com, which is designed to look like the original site. However, the recipes your company sells are now posted for free on the new website.  

The logs show the following process:

The browser requests a DNS resolution of the yummyrecipesforme.com URL.

The DNS replies with the correct IP address. 

The browser initiates an HTTP request for the webpage.

The browser initiates the download of the malware.

The browser requests another DNS resolution for greatrecipesforme.com.

The DNS server responds with the new IP address.

The browser initiates an HTTP request to the new IP address.

A senior analyst confirms that the website was compromised. The analyst checks the source code for the website. They notice that javascript code had been added to prompt website visitors to download an executable file. Analysis of the downloaded file found a script that redirects the visitors’ browsers from yummyrecipesforme.com to greatrecipesforme.com. 

The cybersecurity team reports that the web server was impacted by a brute force attack. The disgruntled baker was able to guess the password easily because the admin password was still set to the default password. Additionally, there were no controls in place to prevent a brute force attack. 

Your job is to document the incident in detail, including identifying the network protocols used to establish the connection between the user and the website.  You should also recommend a security action to take to prevent brute force attacks in the future.

<h2>Resources </h2>

 ### [TCP/HTTP log](https://docs.google.com/document/d/1mLq-qSedt4ZS8SSAQMWuOQ2djibob38wkUJZS3zTCrw/template/preview?usp=sharing&resourcekey=0-yvXQeSsKts64mfpFG8Jm3Q)

<h2>Walk-through</h2>

<p align="left">
By analyzing the log I noticed the following connection attempts:
  <br/><br />
<img src="https://i.imgur.com/mb3ijXT.png" height="55%" width="55%" alt="Abnormal connections"/>
<br /><br />
This behavior goes on until the web server gets overloaded and ends up unable to respond to any connections.
<br /><br />
<img src="https://i.imgur.com/GbTdY1T.png" height="55%" width="55%" alt="Agravação"/>
<br /><br />
Following that, I decided to analyze the abnormal logs individually.
I was then able to notice two common factors between them: The origin IP address and the kind of packet that was sent. 
  <br/><br />
<img src="https://i.imgur.com/4EzNKAl.png" height="55%" width="55%" alt="Padrão"/>
<br /><br />
Henceforth, I was able to deduce that the attack was of the DoS SYN flood attack, since it originated from a single IP address and used exclusevely SYN requests.
<br/><br />
The final step was to come up with a report by using the deducted data along with the scenario information.
<br /><br />
<img src="https://i.imgur.com/yr793sv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<h2>Note</h2>

 This project was part of the course [Google Cybersecurity Professional Certificate.](https://www.coursera.org/professional-certificates/google-cybersecurity) <br />
