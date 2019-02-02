---
layout: page
title:  "General FAQ"
categories: [gameplay]
---

<div class="toc" markdown="1">
  * TOC
  {:toc}
</div>

Welcome to the General FAQ! Here you'll find answers to common questions and errors.
It is organized into sections to make finding answers easier.

# Downloading Rigs of Rods
 
## **Q:**Where do I download the latest Rigs of Rods version?

**A:**You can find the latest version on [GitHub](https://github.com/RigsOfRods/rigs-of-rods/releases) 

[Direct link](https://github.com/RigsOfRods/rigs-of-rods/releases/download/0.4.7.0/RoR_0.4.7.0_Setup.exe)

## **Q:**Where do I find old RoR versions?

**A:**You can find old RoR versions on [SourceForge](https://sourceforge.net/projects/rigsofrods/files/rigsofrods/).

## **Q:**I run Linux/MacOS, where can I download RoR?

**A:**On Linux, You can either download a [prebuilt package](https://archives.rigsofrods.net/old-forum-mybb/thread-68.html) or [compile from source using these shell scripts on apt-based systems.](https://forum.rigsofrods.org/development-discussion/101-shell-scripts-build-rigs-rods-git-debian-ubuntu-mint.html) (Recommended)

Due to the lack of MacOS developers, the last MacOS supported version is [0.37](http://archives.rigsofrods.net/repo/files/repofiles-4th-batch/RoR-Mac-0.37-beta.zip). 

It has been confirmed that the latest version does work in [WINE](https://www.winehq.org/).

# Website/Forum

## **Q:**What happened to the old websites? 

**A:**Quote from @Hiradur on [GitHub](https://github.com/RigsOfRods/rigs-of-rods/issues/795#issuecomment-227970587):


`The website was handed over from tdev to only_a_ptr, the new project leader.` 
`Because the old website had security flaws, it's been reworked from scratch which is why it took so long.`


A blog post explaining everything that happened with the old rigsofrods.org website may be found [here](https://forum.rigsofrods.org/members/michael10055/2-website-changes.html).


## **Q:**Why did the domain switch to rigsofrods.org?

**A:**Simply put, the *.org domain makes sense as RoR is open source.

## **Q:**What happened to my old forum account?

**A:**All user data was removed before transferring the website ownership to @only_a_ptr.

# Archive links

## **Q:**Where can I find the wiki/repository archive?

**A:**You can find links to the archives [here.](https://archives.rigsofrods.net)

## **Q:**Where can I get vehicles/terrains?

**A:**You can find mods on the [Repository](hhttps://forum.rigsofrods.org/downloads.php?tabid=38), [Content](https://forum.rigsofrods.org/content/) section of the forum, the [old Repository archive](https://archives.rigsofrods.net/repo), and the [vB forum archive](https://archives.rigsofrods.net/old-forum/). 

0.4+ terrains may be found on the [Repository](https://forum.rigsofrods.org/downloads.php?tabid=38).

# Multiplayer

## **Q:**What happened to the servers/Why does clicking 'Update' in the Configurator show "Outdated game used!"?


**A:**An "Outdated game used!" page was added for old versions that do not support the [new master server API.](https://github.com/only-a-ptr/multiplayer.rigsofrods.org]

You can still connect to the old RoR servers if you know the IP/Port, a list of the current official legacy servers can be found [here](https://forum.rigsofrods.org/members/michael10055/4-official-multiplayer-servers.html).



## **Q:**I get a "wrong server version" error when trying to join an MP server!

**A:**This means you're trying to join a server that is running an earlier/later RoRNet version than what your current RoR version supports.

[0.4.6.0 RC3](http://archives.rigsofrods.net/old-forum-mybb/thread-3.html) is the last version to support RoRNet 2.37. The new version, RoRNet 2.38, is available in [0.4.7.0](https://github.com/RigsOfRods/rigs-of-rods/releases/tag/0.4.7.0).

To check which RoRNet version your RoR version uses, head over to the `About` tab in the Configurator:

![1](/images/network-about-rorconfig.png)


# AppVeyor/Development builds

## **Q:**How do I download an AppVeyor build?

**A:**First, make sure you have the [VS 2017 x86 Redistributable](https://aka.ms/vs/15/release/vc_redist.x86.exe) installed.

Then go to the [RoR AppVeyor project](https://ci.appveyor.com/project/AnotherFoxGuy/rigs-of-rods/history) page, select a build from the list marked in green (A build marked in red means the build failed) click the `Artifacts` tab, then click `bin\Build.zip` to start the download. After downloading, extract the zip into a new folder (Do not extract into your current RoR install folder!) and run `RoRConfig.exe`. 

To update, just redownload the zip from a newer build.

Builds marked as `0.4.x.0-NB-xx` is from the upstream (master branch-Recommended builds), and `0.4.x.0-NB-xx-yy` builds are pull requests.

# Errors

## **Q:**I get a MSVCP140.dll/MSVCP110.dll/MSVCP100.dll error when starting RoR!
**A:** You're missing the required Visual C++ x86 Redistributable:

Install the correct version that matches the `.dll` name in the error then restart your PC.

- [MSVCP140.dll](https://www.microsoft.com/en-us/download/details.aspx?id=48145)

- [MSVCP110.dll](https://www.microsoft.com/en-us/download/details.aspx?id=30679)

- [MSVCP100.dll](https://www.microsoft.com/en-us/download/details.aspx?id=26999)


## **Q:**A terrain freezes RoR while loading with an InvalidStateException error in the RoR.log!

**A:**Delete all `*.mapbin` files in the cache folder. This error is fixed in [0.4.7.0+](https://github.com/RigsOfRods/rigs-of-rods/releases/tag/0.4.7.0)

## **Q:** Clicking single player results in a `Bad UTF-8 continuation byte` error!

**A:**This is caused by special characters in your Windows username. Currently the only fix is to create a new Windows account without any special characters.

# Miscellaneous

## **Q:**I found a bug, Where do I report it at?

**A:**You can report bugs and other issues on RoR's [GitHub repo issue tracker.](https://github.com/RigsOfRods/rigs-of-rods/issues) 

Make sure your issue hasn't already been reported.

GitHub is only for issues relating to the latest development build, if you're using 0.4.7.0 please post on the [correct support forum](https://forum.rigsofrods.org/support/) instead. 

## **Q:**Does RoR support Windows XP?

**A:**The latest RoR version does not support any Windows version older than Vista.

