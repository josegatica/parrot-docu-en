# Phase 0 Anonymity

# Stage 0: Hiding

# Importance

Our life advances and society in a certain way pressures us to make use of technology. Currently it is difficult to know a close relative who does not use a mobile device or a computer. This technology grows exponentially, which causes us to interact more and more with it. It is this interaction that facilitates the identification and collection of information about our habits, tastes, opinions, ... Above all, our being.

Technology goes deeper and deeper into our lives until we reach the point of being within the personal. We have allowed them to know our habits, our tastes, our ideals and even our opinions.

Without realizing it, we have gone from preventing strangers from accessing our homes to leaving the doors wide open ... And all because we do not realize their presence. The Internet is a great friend, but a great insurmountable friend through whom they can control our entire lives.

Maybe in times past we could take refuge in the lack of control and chaos ... Times change, and like the big corporations, the agencies and our great friend and neighbor the cracker adapts, we must do it too.

Many countries have already considered cyberspace as the fifth dimension in terms of risks to national security. For those who do not know, there are the dimensions of the sea, land, air, space and now ... Cyberspace.

While it is true as some say if we follow a correct ethic, everything is safe. If you do not touch is that it has no failure ...

Let's stop being deluded. Let's stop being asleep. Wake up Let's preoccupy ourselves for our safety. For the safety of those around us.

It is time to mark a before and after. It is time to show that we know how to adapt to this society without being forced by it.

## MAC Address

### ¿What's it?

The MAC address is a globally unique identifier for each device consisting of 48 bits (6 blocks of two hexadecimal characters (4 bits)) that allows the identification of all network devices such as network cards.

Normally the manufacturers once they have mounted the hardware, see a network card, they record in binary format in a ROM of the device the MAC address. This memory is read only, which makes it impossible to modify it directly in the ROM.

According to the above, we can not modify it. It should be noted that what we can not modify is directly the MAC that we have stored in the ROM. So ... what can we modify? When the system is booted, a copy of the MAC address is loaded into our RAM. In this case, what we can do is modify the MAC address that is stored in the RAM. This address will be used in all actions where its use is required.

### Structure

Previously we mentioned that the MAC address is a unique identifier worldwide for each device. These identifiers have an entity that regulates marking standards. Said entity is the IEEE (Institute of Electrical and Electronic Engineering).

A MAC address has the following format:

	*40:AF:E5:F5:FE:50*
	
We must focus mainly on two parts:

On the one hand we have the first part, the left side, which consists of 3 blocks. This side identifies who is the hardware manufacturer. This means that if in our network we see a MAC address that starts with * 40: AF: E5 * this will belong to Sawyer Technologies.

The second part, the one on the right, also consists of 3 blocks. This part of the code is the serial number that identifies the manufactured device. The manufacturer can use the serial number he wants but with the condition that he can only use the same serial number once. That is, the last 3 blocks must be unique for a single device. If another is made, you should not be able to use the ending * F5: FE: 50 *.

### Uses of the MAC Address

1.- The Mac address of a network card can be used for our Router to assign a static IP to our computer.

2.- Power to filter by MAC in our network in such a way that only the MACs that we have specified can access it.

3.- As we mentioned before the Mac address can be used to identify a computer or user within a computer network. Using Nmap (`nmap -sP <IP address>`) or NACC for example we can easily obtain the IP and Mac Address of the equipment connected to the network.

4.- Our mobile phone with the Wifi network activated tends to ask the different routers if they are active. This "question" reflects our MAC address. Remember that our MAC address is a unique address.

5.- There are Internet providers that require MAC Authentication to provide internet to their clients.

6.- If we are in a network and we are the only ones with a device of the Apple brand, it will clearly be known to whom this computer belongs within an establishment or premises.

### Modifying the MAC address

Let's take a stand that the MAC address is a unique address that is given to our device and that this device can make use of it being visible to other users.

#### How do I modify a MAC address?

There are several ways and programs to make such a modification. The most commonly used is (https://github.com/alobbs/macchanger macchanger), available in our Parrot distribution.

Next we will see an easy way of how this modification is done without the use of tools:

> Running ifconfig we can see our different networks. For example, a name commonly used is that of the ethernet network eth0. On the left side of the answer given to the ifconfig command we can see the names.


The first thing we should do is disable the network card to which we are going to change the MAC address:
`ifconfig <network name> down`

Next we modify the MAC of said card for which we want:
`ifconfig <network name> hw ether 00: 00: 00: 00: 00: 00`

> Usually instead of * 00: 00: 00: 00: 00: 00 * 00 *, it is usual to use existing MAC addresses from databases that circulate through the network. It is not very difficult to access these databases.

Finally we reboot the network card we had disabled:
`ifconfig eth0 up`

With these simple steps the MAC address will have been modified. We can check the change by running ifconfig. If you look at the network interface that you wanted to change, it must have a different MAC address than the original one.

> In some places it may be considered illegal to change the MAC address.

## Tunnel ssh

The SSH (secure shell) protocol is used to "tunnel" confidential traffic over the Internet in a secure manner.

For example, a file server can share files using the SMB protocol (Server Message Block), whose data does not travel encrypted. This would allow a third party, who had access to the connection (something possible if the communications are made on the Internet) could thoroughly examine the content of each file transmitted.

In order to mount the file system securely, a connection is established through an SSH tunnel that routes all SMB traffic to the file server within an SSH encrypted connection. Although the SMB protocol is still insecure, traveling within an encrypted connection prevents access to it.

For example, to connect to a web server in a secure way, using SSH, we would make the web client, instead of connecting to the server directly, connect to an SSH client. The SSH client would connect to the tunneled server, which in turn would connect to the final web server. The attractiveness of this system is that we have added an encryption layer without the need to alter the client or the web server.

That is, what is the idea? The idea is to make a connection that is encrypted, making it, even when it is intercepted, secure, preventing it from being able to visualize its content.

Having an encrypted connection prevents someone from sniffing traffic and can view the content of our requests to the network (you can see, for example, the pages we visit). Also prevent that in case of being under attack man in the middle the attacker can modify the packages (to be encrypted an attacker would be in great difficulty to make the modification of the packets). There are other attacks of which we can feel safe making use of an ssh tunnel such as ARP or DNS Spoofing

To establish an SSH tunnel, we will need a computer outside of our local network where security is compromised, which acts as an SSH server.

When the client establishes communication with the SSH server, a communication tunnel will be created between the client on the compromised local network and the SSH server that is outside the compromised local network.

When the client enters an address in the browser, an http request will be sent to the SSH server with the following characteristics:
- The http request will travel through the SSH tunnel that we have established.
- Our request, and all incoming and outgoing traffic will be fully encrypted.

The SSH tunnels are a good solution to ensure communication between 2 machines and to fortify weak protocols such as HTTP, SMTP. FTP, Telnet, etc.

Installing your own SSH server is much easier than installing a VPN server or a proxy server. Remember that things made by oneself are safer ...

### Setting an ssh tunnel

The first step is to have a server to which we will connect by ssh. If we do not have one, we can create one ourselves in our own home, either using a personal computer that will stay at home or a raspberry.

We must make sure that our computer has an installed ssh server. In case of not having it, it would be enough to run by terminal: sudo apt-get install openssh-server openssh-client

> Both parts installed on each computer, both client and server, are needed.

If we want to adapt the server configuration to our requirements, we must modify the sshd_config file located in the path / etc / ssh / sshd_config (command: `sudo pluma / etc / ssh / sshd_config`).

Our computer, which will act as a server, must be accessible from outside. If it is not accessible from the outside we could not create the ssh tunnel. In case of having a fixed IP address there would be no more problem than knowing the IP address. Anonsurf brings us a tool that tells us what our IP address ("IP check") is. It is common for our network provider to assign us a dynamic IP address.


The next thing we should do once we have secure the public IP address of our server, redirect the router requests to the internal IP address of the ssh server.

We observe the internal IP address of the server. We can obtain it by using the `sudo ifconfig` command.

> This IP address must also be fixed. Normally while connected to the router said IP address will not change.

Next we must access the router configuration. It is usually worth to write 192.168.1.1 in the browser. Within the configuration of the router we must find a section that Virtual Servers. Accessing this section we must press the add button (* Add in English *). We must complete with the internal IP address, with the option * Secure Shell Server (SSH) *, with the protocol * TCP * and the port * 22 *.

Once all the completed fields are saved, save the changes.

> It should be noted that in case of having a firewall on the server, we must create a rule that allows incoming and outgoing connections through port 22.

With iptables you just have to execute the commands:
`iptables -A INPUT -i eth0 -p tcp --dport 22 -m state --state NEW, ESTABLISHED -j ACCEPT`
`iptables -A OUTPUT -o eth0 -p tcp --sport 22 -m state --state ESTABLISHED -j ACCEPT`

* -A to indicate entry or exit *
* -port for the destination port of the package *
* -sport for the package source *
* -o for the output network interface *
* -i for the input network interface *
* -m state -state to enable the state module with the respective written states *
* -j to accept the goal *

Until now we would have everything mounted.

### Make the connection

First of all make sure that the client, the computer from which we connect to the server we have created, has installed the openssh-client package.

Once we have everything checked, to make the connection we will execute:
ssh -p 22 -N -D 8081 sawyer@parrotsec.org

* -p to set the listening port *
* -D we specify that a dynamic forwarding of ports or dynamic tunnel is carried out *
* -N allows the ssh tunnel to be established but does not open an interactive session with the ssh server *
* sawyer is the account to which we connect *
* parrotsec.org is the address of the server to which we connect *

### Configuring the browser

We must access the connection options through a proxy. As the proxy server socks will act locally on our computer in the Host or IP address section we have to enter 127.0.0.1. As the SSH tunnel we have opened through port 8081 in the port cell we have to enter the port number 8081. To finish we just have to check the option proxy socks? and select the Socks v5 option since version 5 of the socks protocol is more modern and offers greater security than version 4.

Once all the steps have been completed, click on the OK button. We close the browser and we open it again.


> In case of falling the server, the connection through the browser also falls to us.

We can use the configuration of the connection options section through a proxy of tools such as FoxyProxy (in the case of Firefox) or Proxy Switchy (in the case of chromium).

If you have applications that do not support socks, you can use tsocks.

## Proxy

Put simply: it is a machine through the cueal we can connect to web servers, making us think that we are the machine.

When we are browsing through a proxy, what we are doing is making requests to the proxy server. Then this is in charge of making the request to the server we want to connect to. You could say that a proxy is an intermediary.

> Only http proxy or web proxy servers are going to be commented on. There are other proxy servers such as Proxy socks or Forward Proxy servers.

### Advantage

The main advantage is to hide information from the people who are tracking us. By using a proxy we are not anonymous, we only divert attention.

Our IP address can point us on the map, literally. Using a proxy whose IP address comes from a server in the US, the server we connect to will think that we connect from the US.

To consult all the information that can be obtained through our ip address we can visit pages such as: http://xhaus.com/headers

It may seem like a bullshit, but by providing data like the browser version we are giving a possible attacker the points where he can attack us.

### How to connect to a proxy

Search for a proxy server to connect to: just search in google "proxy list" results will appear. Some of the found ones are www.ip-adress.com/proxy_list/ or http://www.hidemyass.com/

#### Choose the type of proxy well:

- ** Transparent Proxy: ** This type of proxy provides all the data mentioned in the previous section to the web server to which we connect. That is, our IP will be visible at all times.

- ** Anonymous Proxy: ** if we want to use a proxy just to navigate it is more than enough for us. This type of proxy masks the variable http_x_forwarded_for preventing us from giving our IP address. Despite not being able to know our IP address if it can be known that we are making the connection through a proxy.

- ** Proxy Elite: ** this proxy masks the http_x_forwarded_for variable, as well as other variables such as http_via and http_proxy_connection. We will be falsifying the totality of information that we deliver to the web server and also they will not be able to detect that we are connecting through a proxy server.

Data we need to know to connect: IP address and port

How to connect through the browser: each browser is configured in a different way. We just have to use our search engine and consult the configuration guide. Normally it tends to appear in an established configuration - connections. We will always need the IP address of the server to which we are going to connect and the port through which we will make the connection.

### Problems

- Each application must be configured for the data to pass through the proxy
- Tends to have a slow connection
- Not everything is free to trust or everything is good payment.

## Linking of proxies
Commonly, thinking that if after a proxy we hide our identity, we tend to consider the option of doing it after several proxies. This option is possible through the use of tools such as proxychains.

### What is Proxychains?
A tool that redirects all TCP requests and DNS resolutions of the application for us through a list of proxies established by us

### Installation
In our parrot distribution comes installed by default.

### What is the idea?

We, computer A, want to make a direct connection with server B. Said server B, being a direct connection, will know our IP address and will know that we connect from Spain.

Now, we are going to make use of a proxy, called C, located in Morocco. From A we connect to server C, our proxy, and C makes a connection to B. At the moment B receives a request from Morocco.

Up to here everything normal. Well, now let's say we want to put 3 proxies before connecting to B. These proxies will be called D, E, F and they belong to Denmark, Estonia and France respectively. From A, our computer in Spain, we will connect to D, located in Denmark, from D we will connect to Estonia, that is, to computer E, then we will connect from E to computer F located in France, finally, from France we will make a connection to computer B located in Morocco. And finally it will be from this point from which the request will be made to the servant B, which has the web page that we wanted to consult. The trail of the connection goes from Spain, through Denmark, Estonia, France and Morocco. Server B will receive a request from Morocco, who received it from France, who received it from Estonia, who received it from Denmark, who received it from us located in Spain.

### Is it locatable?

Of course, a person can always be located. The bad part comes when you have to call the provider who is doing the service in Morocco, who will tell you the supplier in France, call the supplier in France, who will tell you the supplier in Estonia, etc. All with the difficulty of the call and the time it requires.

> Eye. We can think that it is an ideal form of connection. Not all proxies are safe. Some keep our information and then sell it later. Not everything could be perfect.

## Connection Speed 

If we already had a low connection with only 1 proxy, we can expect a big drop when linking several.

### Configuration
First we must access the configuration file located in /etc/proxychains.conf through any editor and by using the sudo command: sudo nano /etc/proxychains.conf

First of all we must select the type of chain we want to use. We have 3 types:

** Strict: ** will follow exactly the proxy list written in the file. If only one fails, the connection is lost. This option is good in case our proxies are legit and we want to disconnect in case one of them fails.

** Dinamic: ** same functioning as strict. Follow the list of proxies one by one. It differs in that, if one fails, it passes to the next.

** Random: ** will connect randomly to the list of assigned proxies. This is used to modify each address of the system.

To select the option that we want, it is enough to uncomment the line. In the following example we will be using the strict type:
* dynamic_chain *
* strict_chain *
* random_chain *

> Important: dns resolved resolution line to make sure that DNS resolution is done through the proxy servers.

Finally we must enter at the end of the file the proxy list that we will use. To write each proxy, use the structure indicated in the file:


*# ProxyList format*
*#       type  host  port [user pass]*
*#       (values separated by 'tab' or 'blank')*
*#*
*#*
*#        Examples:*
*#*
*#            	socks5	192.168.67.78	1080	lamer	secret*
*#		http	192.168.89.3	8080	justu	hidden*
*#	 	socks4	192.168.1.49	1080*
*#	        http	192.168.39.93	8080	*
*#*		
*#*
*#       proxy types: http, socks4, socks5*
*#        ( auth types supported: "basic"-http  "user/pass"-socks )*
*#*
*[ProxyList]*
*# add proxy here ...*
*# meanwile*
*# defaults set to "tor"*
*socks4 	127.0.0.1 9050*

The last line indicating "defaults set t"
