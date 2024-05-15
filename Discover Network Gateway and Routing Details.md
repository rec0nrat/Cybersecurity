###### Written by Tyler Weiss 20 FEB 2024

#### Assignment Instructions
For this assignment you’ll be delving into the intricacies of network configurations using Command Line Interface (CLI) tools. Your tasks involve discovering your network’s gateway and routing details directly from the CLI. The purpose of this exercise is threefold: firstly, to identify key network configurations through specific CLI commands; secondly, to interpret the significance of these network configurations; and lastly, to analyze and elucidate the output provided by these CLI commands.

Your assignment submission should include screenshots demonstrating how you identified your default gateway and default route using the CLI. Accompany these screenshots with a written explanation where you’ll describe in your own words the commands you used and their functionality. This narrative should not only cover the steps you took but also your interpretation of what the CLI output signifies in the context of network configurations. This exercise is designed to enhance your understanding of network diagnostics and management through practical, hands-on experience with CLI tools.
#### Exercise
Using the `ipconfig` command will output the information for all the network interfaces on a machine in Windows. Identify the machines network interface below should be the IP address, netmask and default gateway. Shown below it is easy to identify that the default gateway is `192.168.1.1`.  Note that using the option `ipconfig /all` will display more information about each network interface to include DHCP IP, DNS IP, IP lease dates and MAC addresses.
![[Pasted image 20240325092614.png]]

Using the command `route print` will display a list of network interfaces and the local IP routing table. Generally speaking, the local IP routing table tells the interface where to send data packets. The IP routing table can be used top confirm the route to the default gateway of the network. At the top of the routing table is the default route to the network gateway. A majority of the routes that follow are broadcast, loopback and multi-cast addresses. Notice that `192.168.1.1` is the network gateway for the interface `192.168.1.190`, witch is the IP of NIC for the machine. 
![[Pasted image 20240325095219.png]]

The `tracert` command will report the route taken to a specified destination; either and IP address or a URL. The first column is the hop count to the destination in sequence. The center columns display the round trip time in milliseconds and represents network latency. The far right column is the address of each device a packet passes through to reach it's destination. So by tracing the route to `google.com` it's observed that:
1. the first hop is the network gateway. Following that the packet traverses the internet service providers nodes eventually moving outside of that network. This example machine is using TDS as it's service provider.
2.  Finally the packet reaches it's destination at `google.com`.
3. The command `nslookup` queries the DNS record to resolve IP addresses and hostnames. In this example `nslookup google.com` is used to verify the destination address of the previous `tracert google.com` command.
![[Pasted image 20240326131321.png]]

