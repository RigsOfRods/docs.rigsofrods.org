---
layout: page
title:  "Multiplayer server setup"
categories: [gameplay]
---

<div class="toc" markdown="1">
  * TOC
  {:toc}
</div>

# Introduction

This tutorial will guide you through the process of setting up a Rigs of Rods multiplayer server.

## Port forwarding

**THIS STEP IS EXTREMELY IMPORTANT - FAILURE TO PORT FORWARD WILL RESULT IN YOUR SERVER TO NOT APPEAR ON THE SERVER LIST AND OTHER PLAYERS WILL NOT BE ABLE TO JOIN!**

Before we begin, you **MUST** be able to forward the server port (TCP `12000` by default). This requires accessing your router's firewall settings. 

<div style="background-color:#FFFFCC; border: 1px solid #FFCC00; padding:0.2em; margin:1em; display: table;">
    <div style="float:left;"><a href="/images/NoticeIcon.png" class="image"><img alt="NoticeIcon.png" src="/images/NoticeIcon.png" width="32" height="32" /></a></div>
    <div style="margin-left:40px"><strong>Notice</strong><br />All routers/ISPs are different, so just search for a tutorial for your router. A general port forwarding guide can be found <a href="https://www.noip.com/support/knowledgebase/general-port-forwarding-guide/">here</a>. If you're unable to figure it out, don't bother trying to host a server. </div>
</div>

If you fail to port forward, the [Cannot connect to master server](#cannot-connect-to-master-server) error will appear on startup.

On Windows, you also may have to allow `rorserver.exe` through the firewall. 

Got that? Great! Let's begin. 

# Windows

## Requirements 

- [VS 2015 Redistributable x86](https://www.microsoft.com/en-us/download/details.aspx?id=48145)
- Text editor (such as Notepad)
- Router access (for port forwarding)
- Good internet connection speed
- A brain, basic computer knowledge, and patience

## Download

First, download `rorserver-2020.01-windows.zip` from [here](https://forum.rigsofrods.org/resources/rigs-of-rods-multiplayer-server.208/).

Extract the zip into a new folder:
![server-filelist-win](/images/server-filelist-win.png)

## server.cfg

Browse to the `config` folder and open `server.cfg` with Notepad. 

![server-config-notepad](/images/server-config-notepad.png)

This is the main configuration file for your server.

Each section contains a comment explaining what it does, pretty self-explanatory.

For simplicity's sake, you only need to change the `name`, `terrain`, `port`, and `password` lines.

Save and close the file once you're done. 

## server.motd 

This file sets your server's Message of the Day (MOTD), shown on server join:

![server-motd](/images/server-motd.png)

Fill it out with whatever you'd like. 

## server.rules

This file contains the rules for your server, shown by typing `!rules`.

Just as before, fill it out with rules you want players to follow. 

## server.auth 

This file configures who is staff on your server. Please see the [UserAuth setup](#userauth-setup) section for more information. 

## Running

Once you're finished configuring your server, double-click `StartServer.bat` to launch the server:

![server-win-start](/images/server-win-start.png)

If successful, your server should now be running and registered on the server list!

Please see the [troubleshooting](#troubleshooting) section if you receive an error.

# Linux

## Download

I will assume you're running the server on a 64-bit VPS with SSH/FTP access and have `unzip` and `nano` installed.

First, download `rorserver-2020.01-linux.zip` from [here](https://forum.rigsofrods.org/resources/rigs-of-rods-multiplayer-server.208/).

Upload the file to your VPS using an FTP client such as WinSCP or FileZilla.

Now SSH into your VPS and change to the directory where you uploaded the zip file. 

Extract the zip with the following command:

`unzip rorserver-2020.01-linux.zip -d rorserver`

The server files should now be located in the `rorserver` folder:

![server-filelist-linux](/images/server-filelist-linux.png)

## server.cfg

In SSH, Change to the `config` directory and type `nano server.cfg`.

![server-config-nano](/images/server-config-nano.png)

This is the main configuration file for your server.

Each section contains a comment explaining what it does, pretty self-explanatory.

For simplicity's sake, you only need to change the `name`, `terrain`, `port`, and `password` lines.

Once you're done, press `CTRL+O` to save the file and `CTRL+X` to exit.

## server.motd 

This file sets your server's Message of the Day (MOTD), shown on server join:

![server-motd](/images/server-motd.png)

Fill it out with whatever you'd like. 

## server.rules

This file contains the rules for your server, shown by typing `!rules`.

Just as before, fill it out with rules you want players to follow. 

## server.auth 

This file configures who is staff on your server. Please see the [UserAuth setup](#userauth-setup) section for more information. 

## Running

Once you're finished configuring your server, change back to the `rorserver` directory and run the following:

```
chmod +x rorserver
sh StartServer.sh
```

`chmod +x rorserver` only needs to be run once to set permissions.

![server-linux-start](/images/server-linux-start.png)

If successful, your server should now be running and registered on the server list!

Please see the [troubleshooting](#troubleshooting) section if you receive an error.

# UserAuth setup

This section will teach you how to set up the `server.auth` file. This is used to define who is staff on your server.

Shut down your server before following these steps.

## User token

First, you need to set a user token in your game's settings. To do this, please follow [this tutorial](https://forum.rigsofrods.org/account/user-token).

## server.auth

Open the `server.auth` file in a text editor. The contents should look like this:

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
;1 9b3c463506f128319a0f16ef08d39d876ca25c68 admin_user
```

Start your server, join it and open the log file located at `config/server.log`. You should see a line similar to this:

`INFO| New client: example_user (en_US), using RoR 0.4.7.0-dev-0ab5bca-dirty, with token 0EBB5A8B28053AB3CF63D4C59F0C1E04F28F01C9`

`0EBB5A8B28053AB3CF63D4C59F0C1E04F28F01C9` is the hashed token for the user, which is what you will set in your auth file. 

If you want the user to be a admin, set the number to `1`, or `4` if you want the user to be a moderator.

```
;example admin
1 0EBB5A8B28053AB3CF63D4C59F0C1E04F28F01C9 example_user
;example moderator
4 0EBB5A8B28053AB3CF63D4C59F0C1E04F28F01C9 example_user
```

Make sure to remove the comment (`;`) before the line. 

Save the file and restart your server. If the server read the auth file correctly, it should log this:

`INFO| found X auth overrides in the authorizations file!`

The next time you join your server you should now have a red flag next to your name if you're a admin or a blue flag if you're a moderator.

![userauth-ingame](/images/userauth-ingame.png)

Admin/moderator commands:

```
!list - Lists all users on a server with their UID

!kick/!ban - Kicks or bans a user. Note that server bans are currently removed when the server restarts.

Usage: !kick UID reason or !ban UID reason

!say - Sends a message to a user or the entire server.

Usage: !say 10 message or !say -1 message

```

# Troubleshooting

Many things can go wrong with your server, here's a small selection of problems that may occur:

## Common error messages

### Cannot connect to master server

`Registration failed, response code: HTTP 503, body: {"result":false,"message":"Could not connect to your server and verify it's version. Please check your Firewall or leave it as it is now to create a local only server. Your server is NOT advertised on the master server!`
 
This usually means that you didn't forward your port. Another cause may be that you specified the wrong IP address. If you don't know the correct IP address, then don't specify one. The server will search the correct IP address itself.

### Address already in use

`FATAL Listerer: SWInetSocket::bind() error: Address already in use`
	
The port that you filled in is already in use by another program. Please use another port number.

### Failed to open authorization file
  
`Couldn't open the local authorizations file ('/etc/rorserver/simple.auth'). No authorizations were loaded.`
  
This means that the server failed to read your authorization file. Make sure your filename matches the one you specified and refer back to the [UserAuth setup](#userauth-setup) section.

If you didn't setup an authorization file, you can safely ignore this error message.

## Connection issues

### Server uses a different protocol version

`Network fatal error: server uses a different protocol version`

You need to download the correct game version to match your server version. Version 2020.01 supports RoRNet 2.42, the latest server protocol.

The latest version may be downloaded from the [homepage](https://www.rigsofrods.org/).

If you've come across a problem not listed here, please post in the appropriate [support forum](https://forum.rigsofrods.org/forums/webservices-support.9/)

