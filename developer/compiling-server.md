---
layout: page
title:  "Compiling server"
categories: [developer]
---

<div class="toc" markdown="1">
  * TOC
  {:toc}
</div>

# Introduction

This tutorial will guide you through the process of building a Rigs of Rods multiplayer server from source.

**Please read thoroughly and do not skip any steps.**

The steps below only apply to the latest source, use a [pre-built package](/gameplay/multiplayer-server-setup/#downloads) instead if you want to host a server for older RoR versions.

# Windows

### Required programs

The programs listed below are required to build the server, restart your computer after installing all the below tools!

- [Visual Studio 2017 Community](https://visualstudio.microsoft.com/downloads/)

- [CMake](https://cmake.org/download/)

- [Git](https://git-scm.com/) (Leave all options to their defaults)

### Getting the source

Create a folder where you want the source to be ( I will be using `C:\Users\%username%\Documents\GitHub\ror-server`)

While in the folder, press `SHIFT + Right click -> Open command prompt window here`. 
If you are running Windows 10, click `Open PowerShell window here`.

Then run this command to download the source:

`git clone https://github.com/RigsOfRods/ror-server.git .`

![gitclone](/images/powershell-server-gitclone.png)

The directory should now be populated with the source:

![serversource](/images/server-source.png)


### Running CMake
Open CMake, input the source and build paths:

![cmake1](/images/cmake-1-server.png)

Click `Configure` and set the generator to Visual Studio 2017:

![cmake2](/images/cmake-2-server.png)

Click `Finish` and let it generate. Once it's done, it should display some build options highlighted in red:

![cmake3](/images/cmake-3-server.png)

**(Optional)** Enable Angelscript support if you plan on using scripts.

Now click `Configure` again until all options turn white:

![cmake4](/images/cmake-4-server.png)

And finally, click `Generate` to create the Visual Studio project.

### Compiling

Click `Open Project` to open Visual Studio.

Once open, set the build to `Release`

![vs2](/images/VS-server-release.png)

Click `Build` then `Build Solution`

![vs3](/images/VS-server-build.png)

Wait for it to compile. Your build should be successful:

![vs4](/images/VS-server-finish.png)

Congratulations! You should now have a `rorserver.exe` inside of the `bin` directory:

![compiled-bin](/images/server-compiled-bin.png)

You can now follow these steps on [running the server](/gameplay/multiplayer-server-setup/).

# Linux
(requires a terminal and `sudo` access)

#### Required tools
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

Download the source:

`git clone https://github.com/RigsOfRods/ror-server.git .`


The folder should now be populated with the source.

### Running CMake

```
cmake -DCMAKE_INSTALL_PREFIX:STRING=/usr \
-DRORSERVER_NO_STACKLOG:BOOL=ON \
-DRORSERVER_CRASHHANDLER:BOOL=OFF \
-DRORSERVER_GUI:BOOL=OFF \
-DRORSERVER_WITH_ANGELSCRIPT:BOOL=OFF \
-DRORSERVER_WITH_WEBSERVER:BOOL=OFF \
.
```

**Note:** Do not forget the ending period! It is required to exit the CMake options.

**(Optional)** Enable Angelscript support if you plan on using scripts.

### Compiling

`make -j2`

Your build should be successful:

![linux1](/images/server-linux-finish.png)

Congratulations! You should now have a `rorserver` binary inside the `/bin` directory.

You can now follow these steps on [running the server](/gameplay/multiplayer-server-setup/).