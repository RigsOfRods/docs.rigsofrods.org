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

## Downloads

Download a pre-built package that matches your RoR version and operating system from the links below:

| Server version                 | Link                                                                                                        | Supported OS(s) | Included build options   |
|--------------------------------|-------------------------------------------------------------------------------------------------------------|-----------------|--------------------------|
| 0.4.8.0 (RoRNet 2.41 - WIP)    | [Download](https://sourceforge.net/projects/rigs-of-rods/files/ror-server/CI-build/)                        | Windows         | Angelscript & Webserver  |
| 0.4.8.0 (RoRNet 2.41 - WIP)    | [Download](http://forum.rigsofrods.org/resources/rigs-of-rods-multiplayer-server-for-0-4-8-0-linux.208/)    | Linux           | Angelscript & Webserver  |
| 0.4.7.0 (RoRNet 2.38)          | [Download](https://forum.rigsofrods.org/resources/rigs-of-rods-multiplayer-server-for-0-4-7-0.206/)         | Windows & Linux | Angelscript              |
| 0.38.67-0.4.6RC3 (RoRNet 2.37) | [Download](http://forum.rigsofrods.org/resources/rigs-of-rods-multiplayer-server-for-0-38-67-0-4-6rc3.207/) | Windows & Linux | Angelscript              |

# Windows

## Setting up

After you've downloaded a pre-built package, extract it into a folder. 

While in the folder, press `SHIFT + Right click -> Open command prompt window here`. 
If you are running Windows 10, click `Open PowerShell window here`, then type `cmd` once the PowerShell window appears:

![powershell](/images/powershell-win10.png)

**Make sure you've forwarded the port you wish to use. There are many tutorials online on how to do this.**

## Running the server using CLI arguments

The easiest way to get a server running is by using the CLI arguments.

List of arguments used by RoRNet 2.41/2.38:

| Argument        | Description                                                                          | Example                          |
|-----------------|--------------------------------------------------------------------------------------|----------------------------------|
| -name           | The server name. Use underscores instead of spaces.                                  | -name Private_Server             |
| -config (-c)    | Path to a configuration file                                                         | -config /path/to/server.cfg      |
| -terrain        | Map name (defaults to 'any')                                                         | -terrain a1da0UID-nhelens.terrn2 |
| -inet           | Registers the server on the [server list](https://forum.rigsofrods.org/multiplayer/) | -inet                            |
| -lan            | Will not register the server on the server list                                      | -lan                             |
| -password       | Private server password                                                              | -password secret                 |
| -ip             | Public IP address to register with                                                   | -ip 127.0.0.1                    |
| -port           | Port to use (defaults to random 12000-12500)                                         | -port 12000                      |
| -verbosity      | Sets displayed verbosity in foreground                                               | -verbosity 1                     |
| -log-verbosity  | Sets verbosity of the log                                                            | -log-verbosity 1                 |
| -log-file       | Sets the filename of the log                                                         | -log-file myserver.log           |
| -script-file    | Server script to execute                                                             | -script-file scripts\Main.as     |
| -use-webserver  | Enables the built-in webserver                                                       | -use-webserver                   |
| -webserver-port | Sets the port for the webserver, default is game port + 100                          | -webserver-port 12100            |
| -version        | Prints the server version number                                                     | -version                         |
| -fg             | Starts the server in the foreground (background by default)                          | -fg                              |
| -resource-dir   | Sets the path to the resource directory                                              | -resource-dir /path/to/resources |
| -auth-file      | Sets the filename of the file that contains authorization info                       | -auth-file server.auth           |
| -motd-file      | Sets the filename of the file that contains the message of the day                   | -motd-file server.motd           |
| -rules-file     | Sets the filename of the file that contains rules for this server                    | -rules-file server.rules         |
| -vehicle-limit  | Sets the maximum number of vehicles that a user is allowed to have                   | -vehicle-limit 6                 |
| -owner          | Sets the owner of this server (for the !owner command)                               | -owner Name                      |
| -website        | Sets the website of this server (for the !website command)                           | -website example.com             |
| -irc            | Sets the IRC url for this server (for the !irc command)                              | -irc chat.freenode.net           |
| -voip           | Sets the voip url for this server (for the !voip command)                            | -voip voice.teamspeak.com        |
| -help           | Displays this list                                                                   | -help                            |

The arguments in RoRNet 2.37 are slightly different:

| Argument        | Description                                                                          | Example                          |
|-----------------|--------------------------------------------------------------------------------------|----------------------------------|
| -name           | The server name. Use underscores instead of spaces.                                  | -name Private_Server             |
| -config (-c)    | Path to a configuration file                                                         | -config /path/to/server.cfg      |
| -terrain        | Map name (defaults to 'any')                                                         | -terrain a1da0UID-nhelens.terrn2 |
| -inet           | Not working on RoRNet 2.37. Use -lan instead. 										 | -inet                            |
| -lan            | Will not register the server on the server list                                      | -lan                             |
| -password       | Private server password                                                              | -password secret                 |
| -ip             | Public IP address to register with                                                   | -ip 127.0.0.1                    |
| -port           | Port to use (defaults to random 12000-12500)                                         | -port 12000                      |
| -verbosity      | Sets displayed verbosity in foreground                                               | -verbosity 1                     |
| -logverbosity   | Sets verbosity of the log                                                            | -logverbosity 1                  |
| -logfilename    | Sets the filename of the log                                                         | -logfilename myserver.log        |
| -script    	  | Server script to execute                                                             | -script scripts\Main.as          |
| -webserver      | Enables the built-in webserver                                                       | -use-webserver                   |
| -webserverport  | Sets the port for the webserver, default is game port + 100                          | -webserver-port 12100            |
| -version        | Prints the server version number                                                     | -version                         |
| -fg             | Starts the server in the foreground (background by default)                          | -fg                              |
| -resdir   	  | Sets the path to the resource directory                                              | -resdir /path/to/resources 		|
| -authfile       | Sets the filename of the file that contains authorization info                       | -authfile server.auth            |
| -motdfile       | Sets the filename of the file that contains the message of the day                   | -motdfile server.motd            |
| -rulesfile      | Sets the filename of the file that contains rules for this server                    | -rulesfile server.rules          |
| -vehiclelimit   | Sets the maximum number of vehicles that a user is allowed to have                   | -vehiclelimit 6                  |
| -owner          | Sets the owner of this server (for the !owner command)                               | -owner Name                      |
| -website        | Sets the website of this server (for the !website command)                           | -website example.com             |
| -irc            | Sets the IRC url for this server (for the !irc command)                              | -irc chat.freenode.net           |
| -voip           | Sets the voip url for this server (for the !voip command)                            | -voip voice.teamspeak.com        |
| -help           | Displays this list                                                                   | -help                            |

Here are a few examples:

A basic password-protected server:

`rorserver.exe -name Private_Server -port 12000 -password secret`

Public server with the terrain set to North St. Helens and a client limit of 4:

`rorserver.exe -name Public_Server -port 12000 -terrain a1da0UID-nhelens.terrn2 -max-clients 4`

**Note**: If you're running a RoRNet 2.37 server, you must set the `-lan` argument otherwise the server will crash!

If the server launched successfully, it should be now displayed on the server list (if allowed) and your log should look similar to this:

![rorserver-launch](/images/rorserver-launch.png)

## Running the server using a config file

If you plan on running a server for extended periods of time, it is recoomended that you set up a config file.

**Note: If you downloaded a RoRNet 2.41 Windows package, you will have to [download](/download/rorserver-example-configs.zip) the config files separately.**

First rename the included files: (example: `tutorial-`):

![f2](/images/server-config-2.png)

Open each file in a text editor and fill it out with your server's info.

To set up the `.auth` file, see the [Setting up admins/moderators](#userauth-setup) section.

Once you're done, use this command to start the server:

`rorserver.exe -c tutorial-config.cfg`

Your server should now be running and (if allowed) registered on the server list!

To stop the server, press `CTRL+C`.

# Linux

## Setting up

I will assume that you are running the server on a VPS and that you have `nano` installed.

First download the correct package and upload it to your server.

Then extract the zip file (Name will be different depending on which package you downloaded)

`unzip rorserver-rornet241-linux.zip -d rorserver-241`

Change to the extracted directory:

`cd rorserver-241`

Copy `libmysocketw.so` to the `/lib` directory (requires superuser access):

`sudo cp libmysocketw.so /lib`

## Running the server using CLI arguments

The easiest way to get a server running is by using the CLI arguments.

For a list of available arguments, see the above tables.

Here are a few examples:

A basic password-protected server:

`./rorserver -name Private_Server -port 12000 -password secret`

Public server with the terrain set to North St. Helens and a client limit of 4:

`./rorserver -name Public_Server -port 12000 -terrain a1da0UID-nhelens.terrn2 -max-clients 4`

If you get permission denied:

`sudo chmod +x rorserver`

To run the server in the foreground, set the `-fg` argument.

**Note**: If you're running a RoRNet 2.37 server, you must set the `-lan` argument otherwise the server will crash!

If the server launched successfully, it should be now displayed on the server list (if allowed) and your log should look similar to this:

![rorserver-launch](/images/rorserver-launch-linux.png)

## Running the server using a config file

If you plan on running a server for extended periods of time, it is recoomended that you set up a config file.

First rename the included files: (example: `tutorial-`):
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

Use the arrow keys to navigate. After you fill out the file(s), press `CTRL+O` to write the changes and `CTRL+X` to exit.

To set up the `.auth` file, see the [Setting up admins/moderators](#userauth-setup) section.

Once you're done, use this command to start the server:

`./rorserver -c tutorial-config.cfg`

Your server should now be running and (if allowed) registered on the server list!

To stop the server, press `CTRL+C` or kill the server if launched in the background:

`sudo kill pid`

# Troubleshooting

Many things can go wrong with your server, here's a small selection of problems that may occur:

Common error messages:

-  **Error upon registration: error: cannot connect from the master server. Please check your Firewall or leave it as it is now to create a local only server. Your server is NOT advertised on the Master server.**
 
This usually means that you didn't forward your port. Another cause may be that you specified the wrong IP address. If you don't know the correct IP address, then don't specify one. The server will search the correct IP address itself.

-  **FATAL Listerer: SWInetSocket::bind() error: Address already in use**
	
The port that you filled in is already in use by another program. Please use another port number.
  
- **error opening admin configuration file '/admins.txt**'
  
This means that you didn't specify an authorizations file. You can safely ignore this error message.

Problems while connecting to your server:

- **Network fatal error: server uses a different protocol version**

You need to download the correct game version to match your server version. 0.4.8RC4 supports RoRNet 2.41, the latest server protocol.


If you've come across a problem not listed here, please post in the appropriate [support forum](https://forum.rigsofrods.org/forums/game-support.8/).

# UserAuth setup

This section will teach you how to set up the `.auth` file.

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

`INFO| found X auth overrides in the authorizations file!`

The next time you join your server you should now have a red flag next to your name if you're a admin or a blue flag if you're a moderator.

![userauth-ingame](/images/userauth-ingame.png)

Admin/moderator commands:

```
!list - Lists all users on a server with their UID

!kick/!ban - Kicks or bans a user. Note that server bans will be removed when the server restarts.

Usage: !kick UID reason or !ban UID reason

!say - Sends a message to a user or the entire server.

Usage: !say 10 message or !say -1 message

```

