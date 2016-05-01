---
layout: page
title:  "Multiplayer server setup"
categories: [gameplay]
---

<div class="toc" markdown="1">
  * TOC
  {:toc}
</div>

This tutorial will guide you through the process of setting up a Rigs of Rods multiplayer server.

# Assumptions

Ok, so some people probably don't understand a lot of this so I'm going to explain it as simply as possible.

-   Bandwidth Limits: bandwidth is how fast your computer can send and receive data from the internet, it is measured by finding the upload and download speed.
-   Ping and Latency: ping is how long it takes a message from your computer to travel to another computer and back. This is an indication of latency: the delay between a packet being sent and arriving at its destination.
-   Packet Loss: the messages your computer sends over the internet are called packets. If some of them go missing in transit this is called packet loss.
-   Port Forwarding: port forwarding is making the ports on your computer accessible through a router.
-   IP Addresses: IP addresses are like the computer's version of a name. Each computer has a unique name and part of that is the IP address.'' This is the only important part if you are running a LAN server''
-   How to find, change, and test all of the above

## Bandwidth

Before you begin it is important for you to test the speed of your internet connection, most importantly your upload speed.

Head on over to [Speedtest.net](http://speedtest.net) and click on the testing site located closest to you.

When the test is complete, you will see the results in an image similar to the one below:

![](/images/network-speed-test.png)

Take a look at the upload speed. On the image above it displays 361kb/s as an upload speed. This is in kilobits. 
As of RoRnet\_2.1, when starting the server you may append "-speed" as a command. 
Input your upload speed in kilobits and the maximum amount of users will be automatically determined. For example: rorserver -speed 361

## Ping

Ping is also a determining factor as to how enjoyable playing on your server will be. Consider the following:

You are connected via a 100Mb/s connection to a computer across the room. When you ping the other computer, you receive the following replies:

    PING 192.168.0.2 (192.168.0.2) 56(84) bytes of data.
    64 bytes from 192.168.0.2: icmp_seq=1 ttl=64 time=0.151 ms
    64 bytes from 192.168.0.2: icmp_seq=2 ttl=64 time=0.149 ms
    64 bytes from 192.168.0.2: icmp_seq=3 ttl=64 time=0.150 ms
    64 bytes from 192.168.0.2: icmp_seq=4 ttl=64 time=0.153 ms
    64 bytes from 192.168.0.2: icmp_seq=5 ttl=64 time=0.156 ms

    --- 192.168.0.2 ping statistics ---
    5 packets transmitted, 5 received, 0% packet loss, time 4004ms
    rtt min/avg/max/mdev = 0.149/0.151/0.156/0.015 ms

Now, let's pretend that there is some extremely lucky person who lives across the world from you that has a server that sits right on a major OC-768 internet backbone with a connection speed of almost 40 Gbps.

When you ping that server, you receive the following replies:

    PING game.ro (61.250.91.13) 56(84) bytes of data.
    64 bytes from 61.250.91.13: icmp_seq=1 ttl=42 time=236 ms
    64 bytes from 61.250.91.13: icmp_seq=2 ttl=42 time=239 ms
    64 bytes from 61.250.91.13: icmp_seq=3 ttl=43 time=236 ms
    64 bytes from 61.250.91.13: icmp_seq=4 ttl=43 time=238 ms
    64 bytes from 61.250.91.13: icmp_seq=5 ttl=42 time=241 ms

    --- game.ro ping statistics ---
    5 packets transmitted, 5 received, 0% packet loss, time 6594ms
    rtt min/avg/max/mdev = 236.520/238.384/241.252/1.829 ms

Notice how even though the server across the world may be on a much faster connection, the time it takes for the ICMP packet to reply, or "ping latency", is much longer.

Why? Let's consider the traceroute to the computer across the room:

    traceroute to 192.168.0.2 (192.168.0.2), 30 hops max, 46 byte packets
     1  * * *

Now look at the computer with the extremely fast connection that is located across the world:

    traceroute to 61.250.91.13 (61.250.91.13), 30 hops max, 46 byte packets
     1  192.168.0.1 (192.168.0.1)  0.224 ms  0.179 ms  0.170 ms
     2  10.121.160.1 (10.121.160.1)  8.016 ms  7.166 ms  8.146 ms
     3  srp5-0.rlghnca-rtr1.nc.rr.com (24.25.2.161)  6.158 ms  5.832 ms  7.868 ms
     4  gig2-3-0.rlghncrdc-pop1.southeast.rr.com (24.93.64.164)  10.308 ms  6.590 ms  8.062 ms
     5  ge-1-3-0.chrlncsa-rtr6.southeast.rr.com (24.93.64.169)  13.493 ms  13.146 ms ge-0-3-0.chrlncsa-rtr6.southeast.rr.com (24.93.64.173)  14.754 ms
     6  pop1-cha-P7-0.atdn.net (66.185.138.69)  15.374 ms  13.180 ms pop1-cha-P4-0.atdn.net (66.185.132.45)  15.945 ms
     7  bb2-cha-P3-0.atdn.net (66.185.132.38)  14.206 ms  12.320 ms  13.732 ms
         MPLS Label=296 CoS=0 TTL=0 S=1
     8  bb2-ash-P14-0.atdn.net (66.185.152.50)  19.355 ms  20.676 ms  21.891 ms
         MPLS Label=78 CoS=0 TTL=0 S=1
     9  pop1-ash-S1-1-0.atdn.net (66.185.144.35)  19.147 ms  18.850 ms  23.749 ms
    10  BeyondTheNetwork.atdn.net (66.185.148.242)  18.547 ms  20.887 ms  20.849 ms
    11  211.115.201.76 (211.115.201.76)  240.212 ms  240.007 ms  241.266 ms
    12  211.115.197.57 (211.115.197.57)  241.276 ms  240.056 ms  238.505 ms
    13  * * *

See how much farther the packets have to travel to reach the second server than the first server, even though the second server is on a faster connection?

This is important to consider when it comes to deciding if it is realistic for you to be hosting a server on your computer. If you have people physically near you, even if you have a not-so-fast connection, your clients will experience a much more enjoyable game than the clients who are connected to the server that is physically located across the world from them on a faster connection. As a real-world example, think about how in online multiplayer games you rarely see someone from North America playing on a European server.

## Packet Loss

Packet loss is the next important issue we will cover. Think about the words "packet loss". In simple terms, if you experience packet loss, some packets that are being set to/from the client/server are being lost, or dropped. This packet loss can cause a number of things, such as delayed reactions of what the client sees and what the server "sees". Packet loss can be tested by the ping command. Lets look closely again at the ping commands that we performed above:

    --- 192.168.0.2 ping statistics ---
    5 packets transmitted, 5 received, ---&gt;0% packet loss&lt;---, time 4004ms
    rtt min/avg/max/mdev = 0.149/0.151/0.156/0.015 ms

No packets were lost in this transmission. If you see a number larger than say, 1-2%, this is of concern because the symptoms discussed above may occur.

# Port Forwarding

Chances are that if you are on a home connection, then your computer is connected to one of those boxes such as D-Link, Linksys, Netgear, etc., which are often called "Routers," or even ISRs (Integrated Service Routers \[Cisco terminology\]) -- they are a combination of a tiny router, a firewall, and DHCP server, and a switch and a few other components which may be configured by the user, or more formally the network administrator. Anyway, if you are not behind one of these boxes, or your computer that will act as a server is connected directly to the internet, you can probably skip this section.

However, since most people *are* behind one of these boxes, you will need to forward the ports to your computer. You may need to look in the manual for your box to see how to do this. Often times this is done by accessing a web interface. Most Linksys boxes use 192.168.1.1 as the default IP address, and and D-Link uses 192.168.0.1. Netgear I think uses 192.168.1.1. If you do not know what the IP address of your all-in-one box is, it is oftentimes the "Default Gateway" address. Skip down a section to where we talking about the ipconfig /all command and how to use it. Try using the address that is displayed for "Default Gateway".

Due to many different models this section can't be tailored down to a simple process. Please see your equipment manual or this site \[www.portforward.com\] for more instructions.

You need to forward one of the following:

-   The TCP port you specify if you are aware of which port you will be using

--or--

-   TCP Port range 12000-12500.

## How to Open a port on your Router

I will be using a generic D-Link system for this tutorial. Please check your manual or the link above for your own equipment.

1. Make sure you know your PUBLIC IP Address. You can get this [here](http://www.whatismyip.com/)

2. Connect to your router using your default gateway IP address. Usually 192.168.0.1, but check [here](http://www.answersthatwork.com/Download_Area/ATW_Library/Networking/Network__4-List_of_default_Router_Admin_Passwords_and_IP_addresses.pdf) for yours.

3. Poke around in your settings/advanced tabs and look for a tab named Port Forwarding or something along those lines.

4. Enter the desired ports you want to open. This is generally a number between 12000 and 12100

5. Enter **YOUR PUBLIC** IP address into the IP Column.

6. Press save!

You should have successfully opened a port now!

## Troubleshooting

Didn't enter a correct Port number: **port numbers are usually 12000-12500**

Server can't register at master server: **You didn't forward correctly. Try again**

# Creating a Rigs of Rods Server

We're now ready to start setting up the Rigs of Rods server.

## Windows OS

If you are working with Windows, there are two methods to create a server. For both methods, you'll need the server executable and some dll files. If you checked the "Multiplayer Server" checkbox while installing Rigs of Rods, then you should have all the required files in your Rigs of Rods folder (by default C:\\Program Files\\Rigs of Rods).

1.  The <u>first method</u> is only usable for RoR 0.38 and later, but it is the easiest and most user-friendly method, since there's no long command or complicated file editing involved. This method is recommended if you just need a temporary server. We will guide you through the process of setting up your server in 4 steps:
    1.  **step 1:** Navigate to the folder where the server files are. If the server was installed together with Rigs of Rods, then the files will be in main Rigs of Rods folder, which is, by default: **C:\\Program Files\\Rigs of Rods**. There, you should see an executable called, 'servergui.exe'. Just start it by double clicking it. This will bring up a window in which you can change the settings of your server before starting it. The following fields can be edited:
        1.  *Server Name*: This is the name of your server. This name will be shown in the serverlist in the configurator.
        2.  *Mode*: Select 'LAN' if you don't want your server to be in the internet serverlist in the configurator, or select 'internet' if you want your server to be advertised in the configurator.
        3.  *IP*: Click the 'get public IP address' button. This is the IP that you will need to fill in your configurator to join your server.
        4.  *Port*: If you're running multiple servers, then you'll need to make sure, each of them has another number here. The Rigs of Rods server ports are usually between 12000 and 14000.
        5.  *Password*: If you prefer a passworded server, then fill in your desired password here.
        6.  *Slots*: The amount of players that will be able to play on your server at the same time. Please read [this blog post](http://www.rigsofrods.com/entries/55-Server-requirements) to find out more about the influence of this setting on the required connection speed.
        7.  *Terrain*: the terrain that your server will use. Use 'any' to let your players select choose their terrain.
        8.  *Log level*: The amount of information that will be shown in the log tab. 'INFO' is recommended here.
        9.  *Log filename*: The name of the file in which the server will store logmessages.
        10. *Admin user token*: Fill in your user token here. This will ensure that when you join your server, you'll be admin.

    2.  **Step 2:** Start your server by clicking the blue 'Start' button in the top right corner.
    3.  **Step 3:** Check in the log tab for any errors. If an error occurred, please consult the 'troubleshooting' part in this tutorial.
    4.  **Step 4:** Test if your server works by joining it. To do this, you'll need to fill in the IP and portnumber, from step 1, in your configurator.
    5.  *Note: you can kick and ban players by right clicking on a player name in the playerlist.*
    6.  *Note: the servergui.exe that comes with Rigs of Rods 0.37 will not work in Internet mode.*

<!-- -->

1.  The <u>second method</u> is more suited for running a permanent server. This server will use less CPU, is more stable and offers advanced functionality, but this server is a bit harder to set up. We will guide you through the process of setting up this server in 4 steps:
    1.  **Step 1**: Navigate to the folder containing the server files. (by default: **C:\\Program Files\\Rigs of Rods**). There, you should see an executable called, 'rorserver.exe'. Do **not** double click that file.
    2.  **Step 2**: Create a new empty text-file, and name it 'server\_INET.bat'. Make sure the extension is .bat, and not .txt. In that file, put the following text: 
    
        
        rorserver.exe -port 12000 -terrain aspen -maxclients 4 -name Default_Servername pause
        
    
        You can change the parameters to suit your needs. In the example above, the terrain aspen is used. Change the 'aspen' to something else to change the terrain. You can edit the other parameters in the same way. Here's a list of all possible parameters: 
        
        
        Usage: rorserver [OPTIONS] <paramaters>

        Where [OPTIONS] and <parameters>
        -c (-config) <config file>   Loads the configuration from a file rather than
                                     from the commandline
        -name <name>                 Name of the server, no spaces, only
                                     [a-z,0-9,A-Z]
        -terrain <mapname>           Map name (defaults to 'any')
        -maxclients <clients>        Maximum clients allowed
        -lan|inet                    Private or public server (defaults to inet)
        -password <password>         Private server password
        -ip <ip>                     Public IP address to register with.
        -port <port>                 Port to use (defaults to random 12000-12500)
        -verbosity {0-5}             Sets displayed log verbosity
        -logverbosity {0-5}          Sets file log verbositylog verbosity
                                     levels available to verbosity and logverbosity:
                                         0 = stack
                                         1 = debug
                                         2 = verbosity
                                         3 = info
                                         4 = warn
                                         5 = error
        -logfilename <server.log>    Sets the filename of the log
        -script <script.as>          server script to execute
        -webserver                   enables the built-in webserver
        -webserver-port <number>     sets up the port for the webserver, default is
                                     game port + 100
        -script <script.as>          server script to execute
        -version                     prints the server version numbers
        -fg                          starts the server in the foreground (background by
                                     default)
        -resdir <path>               sets the path to the resource directory
        -authfile <server.auth>      Sets the filename of the file that contains
                                     player authorization information
        -motdfile <server.motd>      Sets the filename of the file that contains the
                                     message of the day (the contents of this file is
                                     shown when someone joins)
        -rulesfile <server.rules>    Sets the filename of the file that contains rules
                                     for this server (the contents of this file is
                                     shown when someone says '!rules')
        -vehiclelimit {1-*}          Sets the maximum number of vehicles that a user is
                                     allowed to have (a vehicle is a truck, plane or
                                     boat, but also a load or a trailer)
        -owner <name|organisation>   Sets the owner of this server (this will be shown
                                     when someone says '!owner')
        -website <URL>               Sets the website of this server (this will be shown
                                     when someone says '!website')
        -irc <URL>                   Sets the IRC url for this server (this will be shown
                                     when someone says '!irc')
        -voip <URL>                  Sets the voip url for this server (this will be shown
                                     when someone says '!voip')
        -help                        Show this list
        
        
        As you can see, if you prefer a LAN server, then you can do this by adding ''-lan'' to the .bat file.

    3.  **Step 3**: Save the file, and make sure the extension is .bat, and not .txt. When that's done, double click the server\_INET.bat file. Your server is now running.
    4.  **Step 4**: Take a look at the terminal window that should have appeared, if an error occurred, please consult the troubleshooting part of this tutorial.
    5.  **notes**:
        1.  These server commands along with the MOTD file and admin (authorizations) file do not work with the rorserver.exe that comes with Rigs of Rods 0.37.
        2.  To connect to this server:
            1.  on your own computer: type the local host into the server IP box. The local host is always 127.0.0.1
            2.  on a computer on your home network: on the computer that is hosting the server, open command prompt and type ipconfig and push enter. The address that you are looking for is under IP Address or IPv4 address. This number goes into the server IP box in the configurator.

## Linux

There's no server binary available for the latest rorserver versions, but you can follow the following tutorial to compile one yourself: [Compiling Server](http://ror.avrintech.net/rorwikibackup/index.php/Compiling_Server) After that tutorial, you'll have a working Rigs of Rods multiplayer server.

Note: if the init script doesn't work for your system, then you can also start the server using the following command: (there's a list of all possible parameters in the windows part of this tutorial).

## Source

The Rigs of Rods server is licensed under the [GNU General Public License](http://en.wikipedia.org/wiki/GNU_General_Public_License). This means that the source code is available to you free of charge for any purpose. However, if you want to modify and distribute the server, the modified code must be released as GPL code as well. Any application which makes use of GPL code must also be released as GPL.

That said, feel free to submit patches, bugs, and etc to our [GitHub project page](https://github.com/RigsOfRods/ror-server) and help us improve!

To get the latest code, please follow the [Compiling Server](http://ror.avrintech.net/rorwikibackup/index.php/Compiling_Server) tutorial.

# Frequently Asked Questions

1.  **How to add a welcome message to my server? / How to add a Message of the Day (motd)?**
    The easiest way is to create new text file 'motd.txt' in the same folder as your server executable (or '/motd.txt' for Linux users). The contents of that file will be displayed to every user that joins your server.
    It's possible to change the location of that file to somewhere else. To do that, add, for example, the following command line argument:
        -motdfile "C:/rorserver/resources/my_motd.txt"

    or the following configuration file setting:

        motdfile = C:/rorserver/resources/my_motd.txt

2.  **How do I make myself admin on my server?**
    Make a file 'admins.txt' in the same folder as your rorserver.exe. The contents of this file can be found [here](https://github.com/RigsOfRods/ror-server/blob/master/contrib/example-auth.auth). Follow the instructions in that file and then replace the example admin line by the correct data. You can just add as many lines as admins/moderators that you want. It's also possible to change the location of that file to somewhere else. To do that, add, for example, the following command line argument:
        -authfile "C:/rorserver/resources/my_authorizations.txt"

    or the following configuration file setting:

        authfile = C:/rorserver/resources/my_authorizations.txt

3.  **How do I make a LAN/Internet server?**
    Add the command line argument -lan or -inet <u>at the end of your argument list</u>, or add the following configuration setting in your configuration file: mode = lan for a lan server or mode = inet for an Internet server.
4.  **How to connect to a LAN server?**
    You'll need to connect manually to the server by entering the local IP and port number of the server in the Network tab of your Rigs of Rods Configurator.
5.  **How do I permanently ban someone from my server?**
    At the moment, this is not possible. We advise to ban users using iptables, firewalls or similar programs.

If you have a question that is not answerred here, please post in the appropriate [help/support forum](http://rigsofrods.org/forum-15.html).
If you have received an answer for your question, please add the question and answer to this list.

# Troubleshooting

Many things can go wrong with your server, here's a small selection of problems that may occur:

1.  Common error messages
    1.  **ERROR|error upon registration: error: cannot connect from the master server. Please check your Firewall or leave it as it is now to create a local only server. Your server is NOT advertised on the Master server. You should have a look at <http://docs.rigsofrods.org/gameplay/multiplayer-server-setup>**
        *This usually means that you have to forward your port. Please follow the 'Port Forwarding' part of this tutorial. Another cause may be that you specified the wrong IP address. If you don't know the correct IP address, then don't specify one. The server will search the correct IP address itself.*
    2.  **ERROR|FATAL Listerer: SWInetSocket::bind() error: Address already in use**
        *The port that you filled in is already in use by another program. Please use another port number.*
    3.  **ERROR|error opening admin configuration file '/admins.txt**'
        *This means that you didn't specify an authorizations file. You can safely ignore this error message.*'
    4.  **ERROR Listener: SWBaseSocket::accept() error: Socket operation on non-socket**
        *This happens in the servergui after you've stopped your server. Please ignore this message.*
    5.  **ERROR|Message does not appear to contain a body**
        *Please make sure that your terrain name doesn't contain any spaces. If you're not using the servergui, then also make sure that your server name doesn't contain spaces.*

2.  Problems while setting up your server
    1.  **When I double click the server\_INET.bat file, the file just opens in notepad.**
        *Please make sure that the extension of the file is .bat and not .txt*
    2.  **My servergui.exe crashes or gets stuck when starting my server in Internet mode.**
        *The servergui.exe that comes with Rigs of Rods 0.37 only works for LAN games. You'll need to use the second method to setup a Rigs of Rods 0.37 server.*
    3.  **I cannot start the server because MSVCR100.dll is missing.**
        *You'll need to download the visual c++ redistributable. You can download it from the [official Microsoft site](http://www.microsoft.com/downloads/en/details.aspx?FamilyID=a7b7a05e-6de6-4d3a-a423-37bf0912db84).*

3.  Problems while connecting to your server
    1.  **Network fatal error: server uses a different protocol version**
        *You need to download the correct server version to match your game version.*

If you come across a problem, please post in the appropriate [help/support forum](http://rigsofrods.org/forum-15.html).
If you have a solution for your problem, please add the problem and solution to this list.

# Further Reading

## Server Commands

The server supports several commands by default. Please see the [Server Commands](Server_Commands "wikilink") page for more information.

## GameBot

A special Python-based bot is available for random tasks. Please see the [GameBot](GameBot "wikilink") page. This bot connects to a server as a normal client, and can provide several services to both players and server-administrators.

## Server Side Scripts

You can add scripts to the server, which can perform random tasks as well. More information about these script can be found on the [serverside scripting](serverside_scripting "wikilink") page.


