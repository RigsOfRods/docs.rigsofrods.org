# Multiplayer Server Setup

Rigs of Rods multiplayer uses a relay-type server architecture, where the server acts as an intermediary between connected clients by forwarding synchronized physics, vehicle, chat, and gameplay data rather than simulating the world authoritatively itself.

Because of this, the server software is very lightweight and can run on modest hardware while still supporting multiple concurrent players.

This guide covers downloading, configuring, and running a dedicated multiplayer server for Rigs of Rods on Linux and Windows.

Running and maintaining a multiplayer server requires some familiarity with system administration, networking, security, and ongoing maintenance. If you would prefer not to manage the infrastructure yourself, several community-vetted hosting providers offer preconfigured Rigs of Rods server hosting options.

- [PingPerfect $4.99/mo (w/free trial), last checked May 2026](https://pingperfect.com/gameservers/rigs-of-rods-server-hosting)


!!! note
	These providers are listed for convenience only and are not officially affiliated with or endorsed by the Rigs of Rods project. Always review pricing, support quality, uptime guarantees, and terms of service before purchasing hosting services.

## Requirements

As mentioned earlier, the server software is very lightweight, but the relay-type architecture inherently requires significant bandwidth.

- 512 MB (less is ok) of memory for up to 16 players
- 1 vCPU (modern single-core performance is sufficient for small servers)
- 1 GB of disk space for the server binaries and logs (could be more, depending on how active the server is)
- 100 MiB up, 10 MiB down internet speeds (at least, one should plan for up to 100-50 GiB in outbound traffic per month)

In practice, this may look like the e2-micro from Google Public Cloud, the t2.nano from Amazon Web Services, or the smallest droplet from [DigitalOcean](https://m.do.co/c/8d2c25d20a60).

For Windows Server, the above still applies with the additional operating system overhead.

### Port Forwarding

If you decide to self-host (as in, hosted on your own computer and/or home internet), it may be necessary to to [port forward](https://en.wikipedia.org/wiki/Port_forwarding). Without port forwarding, no one else outside your home/local network will be able to join your server.

!!! warning "Continue at your own risk"
	Port forwarding exposes your local network to incoming traffic from the internet. Only proceed if you understand the security implications and are comfortable configuring your router. If done incorrectly, it may result in connectivity issues or unintended exposure of your system.

Because router interfaces vary, choose your specific router model or ISP gateway and follow its port forwarding instructions accordingly.

The suggested port to forward is `12000`, or anything in that range.

## Download

The latest server release is published on the [Repository](https://forum.rigsofrods.org/resources/rigs-of-rods-multiplayer-server.208/) for both Linux and Windows.

=== "Linux"

	This guide assumes basic familiarity with Linux system administration and that you are connecting to the server remotely over SSH.

	You will need the `unzip` utility, which is available through virtually every Linux distribution package manager (e.g. `apt`, `dnf`, or `yum`).

    Transfer the server archive to your machine using `scp`, `rsync`, or an SFTP client such as WinSCP or FileZilla. Once connected over SSH, extract the archive:

    ```bash
    unzip rorserver-*-linux.zip -d rorserver
    cd rorserver
    ```

=== "Windows"

    This guide assumes you're either using a home PC (with direct monitor access) or remotely connected through [Remote Desktop Connection](https://support.microsoft.com/en-us/windows/how-to-use-remote-desktop-5fe128d5-8fb1-7a23-3b8a-41e636865e8c).

    Install the [Visual C++ 2015–2022 Redistributable (x64)](https://aka.ms/vs/17/release/vc_redist.x64.exe) if you don't already have it.

    Extract the downloaded zip into a new folder:

    ![server-filelist-win](../images/server-filelist-win.png)

    !!! tip "Enable file extensions"
        Turn on file extensions in File Explorer so you can tell the config files apart at a glance. In Windows 10 and 11, open File Explorer and toggle **View -> Show -> File name extensions**.

## Configuration

The server ships with four plain-text configuration files. Any text editor will do — the examples below just show one common choice per platform.

=== "Linux"

    From inside the `rorserver` directory:

    ```bash
    nano server.cfg
    ```

    ![server-config-nano](../images/server-config-nano.png)

    Save with ++ctrl+o++, exit with ++ctrl+x++.

=== "Windows"

    Right-click `server.cfg` and open it with Notepad (or your preferred editor).

    ![server-config-notepad](../images/server-config-notepad.png)

### server.cfg

The main server configuration. Every option has an inline comment explaining what it does.

At minimum, set:

| Field | Purpose |
| --- | --- |
| `name` | Display name shown in the public server list |
| `terrain` | Terrain filename players will load |
| `port` | TCP port the server listens on (default is random, but suggested port is `12000`) |
| `password` | Optional join password — leave blank for a public server |

If you want a private server that doesn't register with the master server list, set `mode = lan` instead of `mode = inet`. Players will then join via the **Direct IP** tab in-game.

### server.motd

The Message of the Day, displayed to players on join.

![server-motd](../images/server-motd.png)

### server.rules

The rules text, shown to players when they type `!rules` in chat.

### server.auth

Defines admins, moderators, and bots. See [UserAuth setup](#userauth-setup) below — you can leave this file untouched for now and come back once the server is running.

## Running the server

=== "Linux"

    From inside the `rorserver` directory:

    ```bash
    chmod +x rorserver
    ./RunRoR.sh
    ```

    `chmod +x` only needs to be run once.

    ![server-linux-start](../images/server-linux-start.png)

    !!! tip "Keep it running after you log out"
        Running `./RunRoR.sh` directly will stop the server when your SSH session ends. For a persistent server, run it inside `tmux` or `screen`, or wrap it in a `systemd` service.

=== "Windows"

    Double-click `run.bat`.

    ![server-win-start](../images/server-win-start.png)

If the server starts cleanly, it's now live and — assuming `mode = inet` — registered on the public server list. If you see an error instead, jump to [Troubleshooting](#troubleshooting).

## UserAuth setup

`server.auth` defines who has staff privileges on your server. Stop the server before editing it — changes are only loaded at startup.

Authorization levels:

| Level | Role | Notes |
| --- | --- | --- |
| `1` | Administrator | Red name, full access to admin commands |
| `4` | Moderator | Red name, full access to admin commands |
| `8` | Bot | Blue name, no special privileges |

### Get your user token

In the game settings, set a personal user token following [this tutorial](https://forum.rigsofrods.org/account/user-token). The server stores a hashed version of it, not the token itself.

### Edit server.auth

Open `server.auth`. The default contents look like this:

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

To find a player's hashed token, start the server, have them join, then open `config/server.log`. Look for a line like:

```
INFO| New client: example_user (en_US), using RoR 0.4.7.0-dev-0ab5bca-dirty, with token 0EBB5A8B28053AB3CF63D4C59F0C1E04F28F01C9
```

The 40-character string at the end is the hashed token. Add an entry to `server.auth` using the format `<level> <hashed_token> <username>`:

```
; example admin
1 0EBB5A8B28053AB3CF63D4C59F0C1E04F28F01C9 example_user
; example moderator
4 0EBB5A8B28053AB3CF63D4C59F0C1E04F28F01C9 example_user
```

Remove the leading `;` to activate the line. Save and restart the server. On successful load you'll see:

```
INFO| found X auth overrides in the authorizations file!
```

The player will then appear with a red flag (admin) or blue flag (moderator) next to their name:

![userauth-ingame](../images/userauth-ingame.png)

### Moderation commands

| Command | Usage | Description |
| --- | --- | --- |
| `!list` | `!list` | List all connected players and their UIDs |
| `!kick` | `!kick <UID> <reason>` | Kick a player |
| `!ban` | `!ban <UID> <reason>` | Ban a player — stored in `banned-players.json` and loaded on startup |
| `!say` | `!say <UID> <message>` | Send a private message to a UID; use `-1` to message everyone |

## Troubleshooting

### Cannot connect to master server

```
Registration failed, response code: HTTP 503
Could not connect to your server and verify it's version.
Your server is NOT advertised on the master server!
```

The master server couldn't reach yours to verify it. Common causes:

- The port isn't forwarded on your router (see [Port Forwarding](#port-forwarding)).
- A firewall (host or network) is blocking inbound traffic on the configured port.
- The `ip` setting in `server.cfg` points to the wrong address — leave it blank and the server will auto-detect.

If you only want a LAN/Direct-IP server, set `mode = lan` and ignore this error.

### Address already in use

```
FATAL Listener: SWInetSocket::bind() error: Address already in use
```

Another process is already bound to the port you configured. Pick a different `port` value in `server.cfg`, or stop the process holding it.

=== "Linux"

    ```bash
    ss -lntup | grep <port>
    ```

=== "Windows"

    ```powershell
    netstat -ano | findstr :<port>
    ```

### Failed to open authorization file

```
Couldn't open the local authorizations file ('...simple.auth'). No authorizations were loaded.
```

The server couldn't find the auth file referenced in `server.cfg`. Check that the filename matches what's on disk and revisit [UserAuth setup](#userauth-setup). If you aren't using auth, this warning is harmless.

### Server uses a different protocol version

```
Network fatal error: server uses a different protocol version
```

The client and server are built against incompatible RoRNet protocol versions. Update the game to match the server (or vice versa) from the [Rigs of Rods homepage](https://www.rigsofrods.org/).

---

Run into something not covered here? Post in the [Webservices support forum](https://forum.rigsofrods.org/forums/webservices-support.9/).

