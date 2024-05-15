###### Written by Tyler Weiss
#### Assignment
Perform the different namp scans against 'scanme.nmap.org' and your home network. Briefly explain each scan and it's results.
### Exercise 1

#### Task 1 - Install
Install nmap the Linux server using the following command:
```
sudo apt install nmap 
```
![[Pasted image 20240412150521.png]]
#### Task 2 - Basic Single-Target Use
Using the following link: 
https://www.freecodecamp.org/news/what-is-nmap-and-how-to-use-it-a-tutorial-for-the-greatest-

Via the CLI in your Ubuntu Server you will be conducting internet scans vs a single host. 
Read step by step the above website tutorial and conduct the specific simple scanning listed below via nmap against scanme.nmap.org 
1. Basic Scan 
2. Stealth Scan 
3. Version Scan 
4. Port Scan
5. OS Scan 
6. Aggressive Scan 
Make sure the target of your scans are scanme.nmap.org
##### Basic Scan
Using no options and a single target or range of targets will perform a SYN scan of the top 1000 well-known ports. Using the '-sn' or '-sp' performs a default ping scan for host discovery, without scanning any ports, and reports if the host is up.
![[Pasted image 20240412160854.png]]
![[Pasted image 20240413004311.png]]
The results of the first scan show all TCP ports that replied, their current state and associated service. The second scan results show the associated IPv4 and IPv6 addresses of 'scanme.nmap.org' along with the 'Host is up' status. 
##### Stealth Scan
By using the '-sS' we can perform a SYN or Stealth scan. This will scan a host's ports and if a SYN\ACK is returned reports that the port is open. The Stealth scan does not complete the 3-way-handshake.
![[Pasted image 20240412161540.png]]
The results of the SYN scan are the same as the default nmap scan because it is the same scan.
##### Version Scan
A Version scan will attempt to identify service and versions running on particular ports. It is not completely accurate but it will make the best guess based in the information it receives. CVEs can be discovered based off service versions. To perform a Version scan use the '-sV' option.
![[Pasted image 20240412162322.png]]
The Version scan produces the same output as the previous ones but also adds a version column. Nmap sends specialized, protocol specific, packets to different ports in order to determine services and versions. The above results show that openssh 6.6.1p1, apache httpd 2.4.7, and nping echo are running on the target system. 
##### Port Scan
Most of the discovery scans performed by nmap scan ports but to be more specific you can use the '-p' option followed by a port range or list. By default namp only scans TCP ports. You can specify port UDP or TCP by using either 'T:\<PORTS\>' or 'U:\<PORTS\>'. You can also use '-p-' for all ports, '-sU' for UDP ports or '--top-ports' followed by the number of ports.
![[Pasted image 20240412170501.png]]
This Port scan, tough not displayed, checked all 65535 ports over TCP. The result is the same as before because no other ports are open.
##### OS Scan
OS scans can use TCP/IP fingerprinting to resolve a host's OS and uptime. The scan results will display the percent of accuracy of the OS discovery. An OS scan can be performed using the '-O' option.
![[Pasted image 20240412164107.png]]
The scan results are the as the basic TCP SYN scan except that nmap also sent specialized packets to discern the OS. Below the port scan results are the potential OS versions and the percent of reliability of these guesses.
##### Aggressive Scan
The Aggressive scan performs OS detection, version detection, script scanning, and traceroute. It is extremely noisy but provides better results. An Aggressive scan can be performed using the '-A' option.
![[Pasted image 20240412165155.png]]
![[Pasted image 20240412165224.png]]
The Aggressive scan also used a basic SYN scan for the ports but has yielded slightly more information. An SSH host key, http header, OS version, and traceroute results were produced using this scan.
#### Task 3 - Discovery Scans
Conduct a discovery scan of your host network and note the outcome.
##### ICMP Echo (Ping) Scan
A Ping scan or performs host discovery when used with a range of IP address. By using the network ID with CIDR notation a the entire network range will be scanned for replies from ICMP echo requests. The '-sn' flag can be used to perform a Ping scan.
![[Pasted image 20240412204732.png]]
The results of the standard Ping scan show that 4 hosts are up and retrieves their IPv4, IPv6, MAC address and host name. Remember that a Ping scan does not send packets to verify open ports.
##### TCP SYN Scan
As described earlier, a SYN or Stealth scan will send wait for a SYN/ACK response to determine open ports. When using a network range the scan will discover open ports on hosts that respond.
![[Pasted image 20240412210058.png]]
![[Pasted image 20240412210122.png]]
The standard SYN or Stealth scan produces the  same results as the Ping scan except the port, state and service is displayed under each host. A host is considered 'up' if nmap is receiving any type of reply to it's SYN packets.
##### TCP ACK Scan
The ACK scan is different from the previous scans because it does not show open ports. It is used to map firewall rules. If a RST response is received a port is unfiltered and if no response or an ICMP unreachable error is received then the port is filtered. The '-sA' flag can be used to perform an ACK scan.
![[Pasted image 20240412211955.png]]
Notice that the ACK scan does not produce the same output as a SYN scan because the response to the ACK packets responses do not provide the information necessary to derive a state other than filtered or unfiltered. The results show that 2 ports are filtered out of 4 hosts.
##### UDP Scan
A UDP scan will send UDP packets, usually empty, and if a port responds then it is open. It is common to receive no response from open ports using UDP and thus no response is considered 'open|filtered'. If an ICMP unreachable response is received the port is closed. In order to determine 'open|filtered' are actually open nmap would need to send the proper service probes. The Service scan employs these service probes and thus using '-sV', with the UDP flag '-sU', would help resolve open ports.
![[Pasted image 20240412223009.png]]
![[Pasted image 20240412223032.png]]
The UDP scan results show the port, state and service of 3 hosts on the network. The 4th host may not be present because of the lack of information that UDP packet responses produce. UDP scan also takes a much longer time to complete than TCP oriented scans.
##### TCP Connect Scan
TCP scan completes a full 3-way-handshake over each port to determine if it is open. This behavior causes this scan to be loud and will set off IDS/IPS or be logged. SYN scans are a better choice achieving the same result. The only time a TCP scan is preferred when scanning IPv6 networks or when you don't have permission to create raw packets. The '-sT' can be used to perform a TCP scan.
![[Pasted image 20240412223146.png]]
The TCP connect scan results are a slightly different than the SYN scan, showing only ports where a full 3-way-handshake was completed. Notice that 2 other hosts are not present  because the full TCP connection was not completed for one reason or another on any ports. Also notice that sudo was not used in this command thus the program may not have the proper permission to send the packets that necessary to discover the the other 2 hosts. This was done because simulate an actual situation where a TCP connect scan would be used. 
##### ARP Scan
ARP scan uses ARP requests to discover hosts on the network. This scan is used on LANs yields better results than a standard ping scan because although ICMP ping requests may be blocked, ARP requests are probably not. The '-PR' flag can be used to perform an ARP scan.
![[Pasted image 20240413111140.png]]
![[Pasted image 20240413111152.png]]
The ARP scan produces that same results as the SYN scan except that ARP requests were used to derive this information instead. Using ARP request may allow nmap scans to bypass certain firewall rules.
#####  Host Discovery
Host Discovery is performed using a ping scan. there are many ping scan options including TCP, ACK, UDP, ICMP echo, Protocol and so on. Ping scan options are use the '-P' flag. The '-sn' flag specifies that port discovery be disabled and by default sends ICMP echo request, TCP SYN to port 443, TCP ACK to port 80, and an ICMP timestamp request. The nmap command 'sudo nmap -sn 192.168.1.0/24' could also be represented as 'sudo nmap -sn -PE -PS443 -PA80 -PP 192.168.1.0/24'. For more information of the different ping flags refer to https://nmap.org/book/man-host-discovery.html. 
![[Pasted image 20240413001512.png]]
The Host Discovery scan is the exact same as the Ping scan. The description above explains in-depth the what the scan is doing and gives a reference for other options that may be introduced to this type of scan. 