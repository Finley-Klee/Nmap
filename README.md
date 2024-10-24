# Nmap

<h2>Description</h2>
Nmap is an important enumeration tool and this TryHackMe room (https://tryhackme.com/r/room/furthernmap) is dedicated to learning the basics of port scanning with nmap.

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
- <b>Scan Types: Overview</b>
<p>In this section I was introduced to the six different types of scans that nmap can run.</p>
<br>
<p align="center">The three basic scans are TCP, SYN, and UDP. In the screenshot below you can see the nmap flag for each scan type. <br/>
  <img src="https://github.com/user-attachments/assets/9ec09dd0-041e-4afe-9066-5da564d7951e" height="60%" width="60%" alt="white background with black bullet points and black text. In parantheses the command flags are shown on a dark blue background with white text. The bullet points read TCP connect scans -sT, SYN half open scans -sS, and UDP scans -sU."/>
  <br />
  <br />
 There are also three less common scans. These are the TCP Null scan, the TCP FIN scan, and the TCP Xmas scan. In the screenshot below you can see the nmap flag for each scan type. <br />
  <img src="https://github.com/user-attachments/assets/e057f978-646f-483c-b0bc-378a5d196f87" height="60%" width="60%" alt="white background with black bullet points and black text. In parantheses the command flags are shown on a dark blue background with white text. The bullet points read TCP Null scans -sN, TCP FIN scans -sF, and TCP Xmas scans -sX."/>
</p>
- <b>Scan Types: TCP Connect Scans</b>
<p>This section goes into greater detail about the inner workings of the first scan type: TCP connect scans.</p>
<br>
<p align="center">The TCP connect scan works by performing the three-way handshake with each target port in turn. Depending on the response nmap receives, it determines whether the port is open, filtered, or closed. In the screenshot below you can see a diagram of the three-way handshake process and a section of a packet capture showing what the handshake looks like when intercepted by Wireshark. <br/>
  <img src="https://github.com/user-attachments/assets/214f3504-2af8-40c5-ae46-a54af26cad5b" height="80%" width="80%" alt="at the top left of the screenshot is a diagram with diagonal arrows pointing from a client line on the left to and from a server line of the right. The first diagonal line goes from the client to the server with the SYN packet, the middle diagonal line goes from the server to the client with the SYN/ACK packet, and the final diagonal line goes from the client to the server with the ACK packet. Below this diagram is a section of a Wireshark packet capture showing a table with the packet number, the time, the source ip address, the destination ip address, the protocol, the length, and the information contained in the packet. There are three rows in the table, the first row shows the SYN packet, the second row shows the SYN/ACK packet, and the third row shows the ACK packet."/>
  <br />
  <br />
  There are three possible responses nmap can get from the target port based on if it is open, closed, or filtered by a firewall. If the port is open, when nmap sends the SYN request it will receive the SYN/ACK back. If the port is closed, the port will respond to the SYN with RST (reset), however if the port is filtered by a firewall, most are configured to drop incoming packets, so nmap won't receive a response. The firewall can, however, be configured to respond to the SYN packet with a RST TCP packet, so it is not always clear whether the port is closed or filtered. <br />
  <br />
 After reading about TCP connect scans, I answered the questions at the end of the section: <br />
  <img src="https://github.com/user-attachments/assets/16063214-f50c-451f-9ac7-81beaf079272" height="80%" width="80%" alt="white background with questions in black font and the answers below in a gray rounded rectangle with a lime green rectangle to the right which reads checkmark correct answer. The first questions asks Which RFC defines the appropriate behaviour for the TCP protocol? The answer is RFC 9293. The second question asks If a port is closed, which flag should the server send back to indicate this? The answer is RST."/>
</p>
- <b>Scan Types: SYN Scans</b>
<p>The next section details SYN scans and how they differ from TCP connect scans, and what the pros and cons of using them are.</p>
<br>
<p align="center">Both TCP connect scans and SYN scans use the TCP three-way handshake to gather information about target ports, however the SYN scan does not successfully complete the third part of the handshake. Instead, in the SYN scan, nmap responds to the SYN/ACK packet with a RST (reset) packet. The screenshot below shows a diagram of the process as well as what the packet capture looks like:<br/>
  <img src="https://github.com/user-attachments/assets/0f59af3d-75ca-4681-bd58-fad2425d4c20" height="80%" width="80%" alt="at the top left of the screenshot is a diagram with diagonal arrows pointing from a client line on the left to and from a server line of the right. The first diagonal line goes from the client to the server with the SYN packet, the middle diagonal line goes from the server to the client with the SYN/ACK packet, and the final diagonal line goes from the client to the server with the RST packet. Below this diagram is a section of a Wireshark packet capture showing a table with the packet number, the time, the source ip address, the destination ip address, the protocol, the length, and the information contained in the packet. There are three rows in the table, the first row shows the SYN packet, the second row shows the SYN/ACK packet, and the third row shows the RST packet which has a red background distinguishing it from the previous packet capture."/>
  <br />
  <br />
  Pros of using a SYN scan inlude the ability to bypass older Intrusion Detection Systems, which is why they are often refered to as "stealth" scans. Also, many applications only log completed connections on the port, so a SYN scan can often go unrecorded, which also helps with stealth. And lastly, since the three-way handshake does not have to be completed and then disconnected from, SYN scans are typically faster than TCP connect scans.<br />
  <br />
  There are a couple of disadvantages to SYN scans including that they require sudo permissions in order to work correctly in Linux, and unstable services could potentially be brought down by SYN scans, which is a problem if a client provides a production environment for their test. <br />
  <br />
According to TryHackMe, all in all the pros of the SYN scan outweigh the cons, and for that reason nmap will default to running a SYN scan if it has sudo permissions, and will default to running a TCP scan if it lacks sudo permissions.<br />
  <br />
I finished up the section by answering the questions about SYN scans:<br />
  <img src="https://github.com/user-attachments/assets/4b9dd5af-07f1-4dd2-832a-12fb9286f39d" height="80%" width="80%" alt="white background with questions in black font and the answers below in a gray rounded rectangle with a lime green rectangle to the right which reads checkmark correct answer. The first questions asks There are two other names for a SYN scan, what are they? The answer is Half-Open, Stealth. The second question asks Can Nmap use a SYN scan without Sudo permissions (Y/N)? The answer is N."/>
</p>
- <b>Scan Types: UDP Scans</b>
<p>The UDP section explains how nmap is able to scan UDP ports.</p>
<br>
<p align="center">UDP protocol is used in situations where speed is more important than quality, such as for video calls. As such, UDP is a stateless protocol, meaning that UDP packets are simply sent to an open port and are unacknowledged. This makes determining whether a UDP port is open, filtered, or closed more difficult. When nmap runs a UDP scan it sends a packet and if it receives no response two times, it will mark the ports as open | filtered because it may or may not be behind a firewall and the behavior would remain the same. In the rare case that nmap receives a response, it can mark the port as open. Nmap can identify closed UDP ports because they respond with an ICMP (ping) packet containing a message that the port is unreachable.<br/>
  <br />
Compared to TCP and SYN scans, UDP scans are quite slow, so it is recommended to limit the scan to the top ports only.<br />
  <br />
 After reading about UDP scans, I answered the questions for this section:<br />
  <img src="https://github.com/user-attachments/assets/f494e035-823a-4689-ac33-e938c83db1bc" height="80%" width="80%" alt="white background with questions in black font and the answers below in a gray rounded rectangle with a lime green rectangle to the right which reads checkmark correct answer. The first questions asks If a UDP port doesn't respond to an Nmap scan, what will it be marked as? The answer is open|filtered. The second question asks When a UDP port is closed, by convention the target should send back a port unreachable message. Which protocol would it use to do so? The answer is ICMP."/>
</p>
- <b>Scan Types: NULL, FIN and XMAS</b>
<p>In this section I learned about three less common, but even more stealthy scan options: the NULL scan, the FIN scan, and the XMAS scan.</p>
<br>
<p align="center">
  <img src="https://github.com/user-attachments/assets/6a97874c-83cf-48b1-80bd-cd8618250645" height="80%" width="80%" alt="black text on a white background that reads as the name suggests, NULL scans (-sN) are when the TCP request is sent with no flags at all. As per the RFC, the target host should respond with a RST if the port is closed. Below the text is a screenshot from wireshark showing two packets. The first is the null TCP packet with a blue background and the second is the RST packet with a red background. Below those lines is a deeper inspection of the null packet where you can see zeros in all of the flag lines."/>
  <br />
  <br />
  <img src="https://github.com/user-attachments/assets/66dfb70b-4b44-4bb2-958d-164c32849148" height="80%" width="80%" alt="black text on a white background that reads FIN scans (-sF) work in an almost identical fashion; however, instead of sending a completely empty packet, a request is sent with the FIN flag (usually used to gracefully close an active connection). Once again, Nmap expects a RST if the port is closed. Below the text is a screenshot from wireshark showing two packets. The first is the FIN packet with a blue background and the second is the RST packet with a red background. Below those lines is a deeper inspection of the FIN packet where you can see a 1 in the last line indicating that the FIN flag is set."/>
  <br />
  <br />
  <img src="https://github.com/user-attachments/assets/4aabc4c9-b625-43ff-904e-5f266ee1e3f9" height="80%" width="80%" alt="black text on a white background that reads As with the other two scans in this class, Xmas scans (-sX) send a malformed TCP packet and expects a RST response for closed ports. It's referred to as an xmas scan as the flags that it sets (PSH, URG and FIN) give it the appearance of a blinking christmas tree when viewed as a packet capture in Wireshark. Below the text is a screenshot from wireshark showing two packets. The first is the Xmas packet with a blue background and the second is the RST packet with a red background. Below those lines is a deeper inspection of the Xmas packet where you can see a 1 in the lines for the urgent, push, and fin flags."/>
   <br />
  <br />
  Like with the UDP scan, the expected response to these packets is the same if the port is either open or filtered. If the port is open or filtered then the port should not send a response according to RFC 793, but if it is closed it will send a RST packet. Although the RFC specifies that open ports should not respond to malformed TCP packets, in practice Microsoft Windows and many Cisco network devices respond with RST packets regardless of whether the port is open, filtered, or closed.
   <br />
  <br />
  The purpose of using these scan types is firewall evasion. Many firewalls are configured to drop incoming TCP requests to blocked ports if the packet has the SYN flag set, so these scan types are able to bypass those firewalls. However, most modern IDS solutions have caught up to recognize these scans, so they may not be 100% effective against modern systems, but they are still stealthier options than the main scan types.
   <br />
  <br />
 I finished up the section by answering the questions:<br />
  <img src="https://github.com/user-attachments/assets/28ee172d-347d-42ef-af92-bb9663dea294" height="80%" width="80%" alt="white background with questions in black font and the answers below in a gray rounded rectangle with a lime green rectangle to the right which reads checkmark correct answer. The first question asks Which of the three shown scan types uses the URG flag? The answer is xmas. The second question asks Why are NULL, FIN and Xmas scans generally used? The answer is firewall evasion. The third question asks Which common OS may respond to a NULL, FIN or Xmas scan with a RST for every port? The answer is Microsoft Windows."/>
</p>
- <b>Scan Types: ICMP Network Scanning</b>
<p>The next section describes how to use nmap to perform a "ping sweep" of a target network to map which ip addresses are live.</p>
<br>
<p align="center">When you first connect to a target network on a black box assignment you want to determine which hosts in the network are active. To do this, nmap sends an ICMP packet to each possible ip address for the target network. If an ip address responds, it is marked as being alive. While this is not always acurate, it provides a good baseline.
  <br />
  <br />
 A ping sweep is run using the -sn switch followed by an IP range written either with a hyphen, or in CIDR notation. Below is an example of two different ways to write the ping sweep command for the same network: <br />
  <img src="https://github.com/user-attachments/assets/4119ce1f-0bda-43ea-be15-b77727769d4e" height="50%" width="50%" alt="white background with black bullet points and or between them. Each command has a dark blue background with white text. The top command reads nmap -sn 192.168.0.1-254. The bottom command reads nmap -sn 192.168.0.0/24."/>
  <br />
  <br />
 To answer the section question I generated a command for a ping sweep using CIDR notation:<br />
  <img src="https://github.com/user-attachments/assets/735f3d97-a0a6-4dc5-90dd-3ac9b5cc450c" height="80%" width="80%" alt="white background with the question in black font and the answer below in a gray rounded rectangle with a lime green rectangle to the right which reads checkmark correct answer. The question reads How would you perform a ping sweep on the 172.16.x.x network (Netmask: 255.255.0.0) using Nmap? (CIDR notation) and the answer is nmap -sn 172.16.0.0/16"/>
</p>
- <b>NSE Scripts: Overview</b>
<p>This section gives a brief introduction to the Nmap Scripting Engine (NSE).</p>
<br>
<p align="center">NSE scripts extend the functionality of nmap and can be used to do things such as scan for vulnerabilities, automate exploits, etc. They are written in the Lua programming language, and the script library is quite extensive.<br/>
  <img src="https://github.com/user-attachments/assets/02189908-c213-46d2-8c14-796fa495d5c6" height="80%" width="80%" alt="white background with black text that reads There are many categories available. Some useful categories include: followed by a bulleted list. Bullet 1 safe:- Won't affect the target, bullet 2 intrusive:- Not safe: likely to affect the target, bullet 3 vuln:- Scan for vulnerabilities, bullet 4 exploit:- Attempt to exploit a vulnerability, bullet 5 auth:- Attempt to bypass authentication for running services (e.g. Log into an FTP server anonymously), bullet 6 brute:- Attempt to bruteforce credentials for running services, bullet 7 discovery:- Attempt to query running services for further information about the network (e.g. query an SNMP server)."/>
  <br />
  <br />
  <img src="https://github.com/user-attachments/assets/653fb284-908e-4167-8400-183afae3aac1" height="80%" width="80%" alt="white background with the questions in black font and the answers below in a gray rounded rectangle with a lime green rectangle to the right which reads checkmark correct answer. The first question reads What language are NSE scripts written in? and the answer is Lua. The second question reads Which category of scripts would be a very bad idea to run in a production environment? and the answer is intrusive."/>
</p>
- <b>NSE Scripts: Working with the NSE</b>
<p>In this next section I learned how to run NSE scripts using the --script switch for nmap.</p>
<br>
<p align="center">All of the applicable scripts form a category can be run using the --script=[category name] switch. For example, in the nmap switches section I wrote out the switch to run all of the scripts in the "vuln" category, which is --script=vuln. We could also do this with all of the scripts in the "safe" category by writing --script=safe.
  <br />
  <br />
 To run a specific script we use the --script switch with the file name like this: --script=http-fileupload-exploiter. You can also run multiple scripts separated by commas. For example: --script=smb-enum-users,smb-enum-shares.
  <br />
  <br />
  For scripts that require arguments you use the --script-args switch, like this: --script http-put --script-args http-put.url='/dav/shell.php',http-put.file='./shell.php'
   <br />
  <br />
 To answer the question about scripts I used the help page for the ftp-anon.nse script:<br />
  <img src="https://github.com/user-attachments/assets/363ee448-eb4c-4eb8-be4a-56223c271c1b" height="80%" width="80%" alt="white background with the question in black font and the answer below in a gray rounded rectangle with a lime green rectangle to the right which reads checkmark correct answer. The question reads What optional argument can the ftp-anon.nse script take? and the answer is maxlist."/>
</p>
- <b>NSE Scripts: Searching for Scripts</b>
<p>To round out the discussion of NSE, this section teaches how to search for scripts and install new scripts to your attacking machine.</p>
<br>
<p align="center">You can search for scripts either by searching the nmap website, or by searching through the locally stored scripts which are found in /usr/share/nmap/scripts<br/>
  <br />
 There are a few different methods to search through the scripts file. You can use grep with the search term, for example to search for scripts that contain "ftp" you could use grep "ftp" /usr/share/nmap/scripts/script.db and below is a screenshot of the output:<br />
  <img src="https://github.com/user-attachments/assets/c74086d5-27e0-4177-90a9-a2f0d1a4ea2f" height="80%" width="80%" alt="a white background with mostly black text. The first line has the username muri@augury in red and the file location /usr/share/nmap/scripts in blue followed by the command in black grep ftp /usr/share/nmap/scripts/script.db. The following 9 lines all show scripts that contain ftp in the file name, for example ftp-anon.nse."/>
  <br />
  <br />
Another way to search is by using wildcard asterisks on either side of the search term in the file path of an ls -l command like this:<br />
  <img src="https://github.com/user-attachments/assets/ab4edf8a-0e75-4485-8a25-2488178612a4" height="80%" width="80%" alt="a white background with mostly black text. The first line has the username muri@augury in red and the file location /usr/share/nmap/scripts in blue followed by the command in black ls -l /usr/share/nmap/scripts/*tfp* the following 9 lines list the individual script files that contain ftp in the name."/>
   <br />
  <br />
  To download scripts, you should be able to get any missing scripts by running an nmap update, however you can also download scripts manually using the sudo wget -O /usr/share/nmap/scripts/<script-name>.nse https://svn.nmap.org/nmap/scripts/<script-name>.nse command. This must be followed by running the nmap --script-updatedb command.
   <br />
  <br />
 Finally, I checked my NSE knowledge by answering the section questions:<br />
  <img src="https://github.com/user-attachments/assets/27ff1841-0608-4d9f-a2f8-9ae7bd52f5ef" height="80%" width="80%" alt="white background with the questions in black font and the answers below in a gray rounded rectangle with a lime green rectangle to the right which reads checkmark correct answer. The first question reads Search for smb scripts in the /usr/share/nmap/scripts/ directory using either of the demonstrated methods. What is the filename of the script which determines the underlying OS of the SMB server? and the answer is smb-os-discovery.nse. The second question reads Read through this script. What does it depend on? and the answer is smb-brute."/>
</p>
- <b>Firewall Evasion</b>
<p>Description</p>
<br>
<p align="center">Step One: <br/>
  <img src="" height="80%" width="80%" alt="image one"/>
  <br />
  <br />
  Step Two: <br />
  <img src="" height="80%" width="80%" alt="image two"/>
  <br />
  <br />
  Step Three: <br />
  <img src="" height="80%" width="80%" alt="image three"/>
   <br />
  <br />
  Step Four: <br />
  <img src="" height="80%" width="80%" alt="image four"/>
   <br />
  <br />
  Step Five: <br />
  <img src="" height="80%" width="80%" alt="image five"/>
</p>
- <b>Practical</b>
<p>Description</p>
<br>
<p align="center">Step One: <br/>
  <img src="" height="80%" width="80%" alt="image one"/>
  <br />
  <br />
  Step Two: <br />
  <img src="" height="80%" width="80%" alt="image two"/>
  <br />
  <br />
  Step Three: <br />
  <img src="" height="80%" width="80%" alt="image three"/>
   <br />
  <br />
  Step Four: <br />
  <img src="" height="80%" width="80%" alt="image four"/>
   <br />
  <br />
  Step Five: <br />
  <img src="" height="80%" width="80%" alt="image five"/>
</p>

