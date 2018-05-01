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

## Windows

### Pre-built packages

If you don't want to compile the server yourself, you can download the correct pre-compiled build below then skip to the [Configuration](#configuration) section:

[For 0.4.7.0](https://github.com/Michael10055/ror-server-rornet238/releases/download/2.38-v1/rorserver-rornet238-windows.zip)

[For 0.38.67 to 0.4.6RC3](https://github.com/Michael10055/ror-server-rornet237/releases/download/2.37/ror-server-237-windows.zip)


### Building yourself
The programs listed below are required to build the server, restart your computer after installing all the below tools!

- [Visual Studio 2015 Community Edition](https://go.microsoft.com/fwlink/?LinkId=532606&clcid=0x409) C++ tools must be installed:

![vs](/images/VS-server-cplusplus.png)

- [CMake](https://cmake.org/download/)

- [Git](https://git-scm.com/) (Leave all options to their defaults)

### Getting the source

Create a folder where you want the source to be ( I will be using `C:\ror-server`)

While in the folder, do `SHIFT + Right click -> Open command prompt window here`.

A Command Prompt window should now be open.

Depending on what RoR version you are using, the clone command will be different.

### 0.4.7.0

If you want to run a server for 0.4.7.0, run this command:

`git clone https://github.com/Michael10055/ror-server-rornet238.git`

### Latest GitHub commit/AppVeyor builds

To run a server for the latest `rigs-of-rods` repo commit/AppVeyor builds, run this command:

`git clone https://github.com/RigsOfRods/ror-server.git`

### 0.38.67 to 0.4.6RC3

If you want to run a server for versions 0.38.67 to 0.4.6RC3, run this command:

`git clone https://github.com/Michael10055/ror-server-rornet237.git`

After running the correct command, you should now have a folder named `ror-server` inside of the folder you created earlier.

### Running CMake
Open CMake, input the source and build paths:

![cmake1](/images/cmake-1-server.png)

Click `Configure` and select your compiler: (Don't confuse Visual Studio 14 2015 with Visual Studio 15)

![cmake2](/images/cmake-2-server.png)

Click `Finish`.

(**Optional**) Change build options - It is highly recommended to enable Angelscript support.

![cmake3](/images/cmake-3-server.png)

It is highly recommended to enable Angelscript support.

Click `Configure` again till all fields are white then press `Generate`.

You should now have a `build` folder with `rorserver.sln` inside of it.

### Compiling

Open `rorserver.sln`

Set the build to `Release`

![vs2](/images/VS-server-release.png)

Click `Build -> Build Solution

![vs3](/images/VS-server-build.png)

Wait for it to compile. Your build should be successful.

![vs4](/images/VS-server-finish.png)

You should now have `rorserver.exe` inside of the `bin` directory.

### Configuration
Copy the example `auth`/`cfg`/`motd`/`rules` files from the `contrib` directory to the `bin` directory:

![f1](/images/server-config-1.png)

Rename the files: (example: `tutorial-`):

![f2](/images/server-config-2.png)


Open each file in a text editor and fill it out with your server's info. You will need to port forward your servers port in your router settings. See the `Port Forwarding` part of this page. If you're running your server on a VPS, you most likely can skip this step.

If you're running a RoRNet 2.38/2.37 server (UserAuth support for 2.40 will come in the future), see the [Setting up admins/moderators](#userauth-setup) section.

### Running the server
In the `bin` directory,
`SHIFT + Right click -> Open command prompt window here`

To start the server:

`rorserver.exe -c your-config.cfg`

Your server should now be running and registered on the server list!

To stop the server, press `CTRL+C` or close the command prompt.

## Linux
(requires a `terminal` and `sudo` access)

#### Required tools:
(Debian/Ubuntu)

- `sudo apt-get install build-essential`
- `sudo apt-get install nano`
- `sudo apt-get install cmake`
- `sudo apt-get install git`

(CentOS)

- `sudo yum groupinstall 'Development Tools'`
- `sudo yum install nano`
- `sudo yum install cmake`
- `sudo yum install git`

### Getting the source

Create rorserver user with no login rights:

`useradd rorserver -s /bin/false`

Make a directory where you want your source to be:

`mkdir ror-server`

Change into the created directory:

`cd ror-server`

Depending on what RoR version you are using, the clone command will be different.

#### 0.4.7.0

If you want to run a server for 0.4.7.0, run this command:

`git clone https://github.com/Michael10055/ror-server-rornet238.git`

#### Latest GitHub commit/AppVeyor builds

To run a server for the latest `rigs-of-rods` repo commit/AppVeyor builds, run this command:

`git clone https://github.com/RigsOfRods/ror-server.git`

#### 0.38.67 to 0.4.6RC3

If you want to run a server for versions 0.38.67 to 0.4.6RC3, run this command:

`git clone https://github.com/Michael10055/ror-server-rornet237.git`

After running the correct command, you should now have a folder named `ror-server` inside of the folder you created earlier.

Change into the source folder (The folder name might be different depending on which `git clone` command you used):

`cd ror-server`

### Running CMake

(**Optional**) Change build options - It is highly recommended to enable Angelscript support.

```

cmake -DCMAKE_INSTALL_PREFIX:STRING=/usr \
-DRORSERVER_NO_STACKLOG:BOOL=ON \
-DRORSERVER_CRASHHANDLER:BOOL=OFF \
-DRORSERVER_GUI:BOOL=OFF \
-DRORSERVER_WITH_ANGELSCRIPT:BOOL=ON \
-DRORSERVER_WITH_WEBSERVER:BOOL=OFF \
.

```



### Compiling

`make -j2`

Your build should be successful:

![linux1](/images/server-linux-finish.png)

You should now have a `rorserver` binary in the `/bin` directory.

### Configuration


Copy the example `auth`/`cfg`/`motd`/`rules` files from the `contrib` directory to the `bin` directory:

```

cd contrib
cp example-auth.auth ../bin
cp example-motd.motd ../bin
cp example-config.cfg ../bin
cp example-rules.rules ../bin

```



Change into the `bin` directory:

`cd ../bin`

Rename the files (example: `tutorial-`):

```

mv example-auth.auth tutorial-auth.auth
mv example-motd.motd tutorial-motd.motd
mv example-config.cfg tutorial-config.cfg
mv example-rules.rules tutorial-rules.rules

```

Edit the files using `nano`:

```
nano tutorial-motd.motd
nano tutorial-config.cfg
nano tutorial-rules.rules

```
Use the arrow keys to navigate. After you fill out the file, press `CTRL+O` to write the changes and `CTRL+X` to exit.
You will need to port forward your servers port in your router settings. See the `Port Forwarding` part of this page. If you're running your server on a VPS, you most likely can skip this step.

If you're running a RoRNet 2.38/2.37 server (UserAuth support for 2.40 will come in the future), see the [Setting up admins/moderators](#userauth-setup) section.

### Running the server

To start the server:

`./rorserver -c your-config.cfg`

If you get permission denied:

`sudo chmod +x rorserver`


Your server should now be running and registered on the server list!

To stop the server, use the kill command with the `pid`:

`sudo kill pid`

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

2.  Problems while connecting to your server
    1.  **Network fatal error: server uses a different protocol version**
        *You need to download the correct game version to match your server version. 0.4.7.0+ supports RoRNet 2.38, the latest server protocol.*

If you come across a problem, please post in the appropriate [help/support forum](https://forum.rigsofrods.org/forum-15.html).
If you have a solution for your problem, please add the problem and solution to this list.

# UserAuth setup

If you're running a RoRNet 2.38/2.37 server (UserAuth support for 2.40 will come in the future) and have your server working, this section will teach you how to set up the `.auth` file.

Open the `.auth` file in a text editor. It should look like this:


```
; This files defines who is an admin, moderator etc on your server
; the syntax is as follows: <authorization> <token> <username (optional)>
;  - where authorization is a number between 1 and 13:
;		1: administrator (red name, has access to all admin functions)
;		4: moderator (red name, has access to all admin functions)
;		8: bot, robot (blue name, no special privileges)
;  - token is the user token of the user. It's the token that uniquely identifies the user, not the username.
;		This is not the normal token, but an encoded version of it.
;		You can get this token by starting your server, filling in your token
;		in your configurator and then look in the logfile for your encoded token.
;		A typical encoded token is exactly 40 characters long.
;  - username is the username that will be shown to other players
;		The username that the user fills in into their configurator will be overridden by this username.
;		If you do not specify a username, the username from the client's configurator will be used.
;
; note: You need to restart server after every edit to this file.
; note: Do not use spaces in the usernames
; note: Empty lines and lines starting with a ";" will be ignored.

; EXAMPLE ADMIN (replace these with your username and encoded token)
1 9b3c463506f128319a0f16ef08d39d876ca25c68 admin_user
```

Open RoRConfig and set your unhashed token `Gameplay tab -> User Token` box. It's kind of like a password, so make it unique.

Now join your server and check your server's log. You should see a line similar to this:

`INFO| New client: example_user (en_US), using RoR 0.4.7.0-dev-0ab5bca-dirty, with token 0EBB5A8B28053AB3CF63D4C59F0C1E04F28F01C9`

This is the hashed token for the user.

If you want the user to be a admin, set the number in the `.auth` file to `1`, or `4` if you want the user to be a moderator.

```
;example admin
1 0EBB5A8B28053AB3CF63D4C59F0C1E04F28F01C9 example_user
;example moderator
4 0EBB5A8B28053AB3CF63D4C59F0C1E04F28F01C9 example_user
```

Save the file and restart your server. If the server read the auth file correctly, it should log this:

` INFO| found X auth overrides in the authorizations file!`

The next time you join your server you should now have a red flag next to your name if you're a admin or a blue flag if you're a moderator.

Admin/moderator commands:
```
!list - Lists all users on a server with their UID

!kick/!ban - Kicks or bans a user. Note that server bans will be removed when the server restarts.

Usage: !kick UID reason or !ban UID reason

!say - Sends a message to a user or the entire server.

Usage: !say 10 message or !say -1 message

```

