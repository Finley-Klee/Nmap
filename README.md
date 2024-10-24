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
  <img src="https://github.com/user-attachments/assets/04b22750-5b63-4d53-9cc9-cdab1fabcc54" height="80%" width="80%" alt="image one"/>
  <br />
  <img src="https://github.com/user-attachments/assets/b2638613-dd28-4fc7-aa1e-1147d625fd0f" height="80%" width="80%" alt="image two"/>
  <br />
  <img src="https://github.com/user-attachments/assets/440ef56b-7e96-4b36-8089-03bb2faa230a" height="80%" width="80%" alt="image three"/>
  <br />
  <img src="https://github.com/user-attachments/assets/517d1cac-baa5-438f-a302-9734688278a3" height="80%" width="80%" alt="image four"/>
  <br />
  <img src="https://github.com/user-attachments/assets/eb5be6f3-69db-47d7-99df-5201c3cba47f" height="80%" width="80%" alt="image five"/>
  <br />
  <img src="https://github.com/user-attachments/assets/32069e7d-6cb4-4c0d-8922-152fd66e3dcc" height="80%" width="80%" alt="image six"/>
</p>
