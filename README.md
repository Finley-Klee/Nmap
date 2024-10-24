# Nmap

<h2>Description</h2>
Nmap is an important enumeration tool and this TryHackMe room is dedicated to learning the basics of port scanning with nmap.

<h2>Utilities Used</h2>

- <b>nmap</b> 

<h2>Environments Used </h2>

- <b>Linux Ubuntu</b>

<h2>Project walk-through:</h2>

- <b>Introduction</b>
<p>The introduction section provides foundational information about to map the "landscape" of a system using a port scan. When a computer runs a network service, it opens a port to receive the connection. Ports allow your computer to make multiple network requests and run multiple network services by establishing connections to remote webservers using different ports on the machine. Services listen on a predetermined open port, for example HTTPS "listens" on port 443, and a user's computer opens a random port to communicate with the service. Computers have a total of 65,535 available ports of which 1024 are standard or "well known", and the rest can be used by your computer at random to establish a connection.</p>
<br>
<p align="center">
  <img src="https://github.com/user-attachments/assets/490f7255-64f7-418c-8d4c-af88fb36abb1" height="80%" width="80%" alt="Question and answer section of the try hack me room. The background is white with the questions written in black text above gray rounded rectangle answer slots and to the right of the answers are lime green rectangles which read check mark correct. First question: What networking constructs are used to direct traffic to the right application on a server? Answer: ports. Second question: How many of these are available on any network-enabled computer? Answer: 65535. Third question: [Research] How many of these are considered "well-known"? (These are the "standard" numbers mentioned in the task) Answer: 1024."/>
</p>
<br />
<br />
- <b>Nmap Switches</b>
<p>Using the nmap help window, I researched some of the many command switches available for nmap.</p>
<br>
<p align="center">
  <img src="https://github.com/user-attachments/assets/04b22750-5b63-4d53-9cc9-cdab1fabcc54" height="80%" width="80%" alt="white background with questions in black font and the answers below in a gray rounded rectangle with a lime green rectangle to the right which reads checkmark correct answer. Q: What is the first switch listed in the help menu for a 'Syn Scan' (more on this later!)? A: -sS Q: Which switch would you use for a UDP scan? A: -sU Q: If you wanted to detect which operating system the target is running on, which switch would you use? A: -O."/>
  <br />
  <img src="https://github.com/user-attachments/assets/b2638613-dd28-4fc7-aa1e-1147d625fd0f" height="80%" width="80%" alt="white background with questions in black font and the answers below in a gray rounded rectangle with a lime green rectangle to the right which reads checkmark correct answer. Q: Nmap provides a switch to detect the version of the services running on the target. What is this switch? A: -sV Q: The default output provided by nmap often does not provide enough information for a pentester. How would you increase the verbosity? A: -V Q: Verbosity level one is good, but verbosity level two is better! How would you set the verbosity level to two? (Note: it's highly advisable to always use at least this option) A: -vv."/>
  <br />
  <img src="https://github.com/user-attachments/assets/440ef56b-7e96-4b36-8089-03bb2faa230a" height="80%" width="80%" alt="white background with questions in black font and the answers below in a gray rounded rectangle with a lime green rectangle to the right which reads checkmark correct answer. Q: We should always save the output of our scans -- this means that we only need to run the scan once (reducing network traffic and thus chance of detection), and gives us a reference to use when writing reports for clients. What switch would you use to save the nmap results in three major formats? A: -oA Q: What switch would you use to save the nmap results in a normal format? A: -oN Q: A very useful output format: how would you save results in a grepable format? A: -oG"/>
  <br />
  <img src="https://github.com/user-attachments/assets/517d1cac-baa5-438f-a302-9734688278a3" height="80%" width="80%" alt="white background with questions in black font and the answers below in a gray rounded rectangle with a lime green rectangle to the right which reads checkmark correct answer. Q: Sometimes the results we're getting just aren't enough. If we don't care about how loud we are, we can enable aggressive mode. This is a shorthand switch that activates service detection, operating system detection, a traceroute and common script scanning. How would you activate this setting? A: -A Q: Nmap offers five levels of timing template. These are essentially used to increase the speed your scan runs at. Be careful though: higher speeds are noisier, and can incur errors! How would you set the timing template to level 5? A: -T5"/>
  <br />
  <img src="https://github.com/user-attachments/assets/eb5be6f3-69db-47d7-99df-5201c3cba47f" height="80%" width="80%" alt="white background with questions in black font and the answers below in a gray rounded rectangle with a lime green rectangle to the right which reads checkmark correct answer. Q: We can also choose which port(s) to scan. How would you tell nmap to only scan port 80? A: -p 80 Q: How would you tell nmap to scan ports 1000-1500? A: -p 1000-1500"/>
  <br />
  <img src="https://github.com/user-attachments/assets/32069e7d-6cb4-4c0d-8922-152fd66e3dcc" height="80%" width="80%" alt="white background with questions in black font and the answers below in a gray rounded rectangle with a lime green rectangle to the right which reads checkmark correct answer. Q: A very useful option that should not be ignored: How would you tell nmap to scan all ports? A: -p- Q: How would you activate a script from the nmap scripting library (lots more on this later!)? A: --script Q: How would you activate all of the scripts in the vuln category? A: --script=vuln"/>
</p>
