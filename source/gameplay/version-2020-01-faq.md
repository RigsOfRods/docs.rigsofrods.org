Version 2020.01 FAQ
============



Rigs of Rods version 2020.01 brings some important changes to how players interact with the game. This page should answer any questions you have about these changes.

## Version format change

Until now, Rigs of Rods has used the [semver release format](https://semver.org/) (0.38.x, 0.39.x, 0.4.x). 
Starting with version 2020.01, we now use date-based versioning.  All future versions will now start with `<year>.<month>`

### Why?

In 2016, we (the RoR developers) released version 0.4.7.0. During the following years, lots of bugfixes and new features were added. We wanted to include them all with the next release, 0.4.8.0, but [new bugs and technical issues](https://forum.rigsofrods.org/threads/developer-suffering-a-release-block.147/) prevented us from doing so. 

So on January 2019, the first release candidate, [0.4.8 RC1](https://forum.rigsofrods.org/threads/test-build-version-0-4-8-rc1.939/), was released as a test build. As with all test builds, bugs were found and the next release candidates (RC2, RC3, RC4) followed.

But as we made more changes and bugfixes, mods became dependent on the [development builds](https://forum.rigsofrods.org/threads/ror-development-builds-for-0-4-8-for-windows-and-linux.696/) to function properly. The current stable release (0.4.7.0) became too old to support them. However, the game still had some major glitches holding back an official 0.4.8.0 release. As a solution, we decided to release [0.4.8 RC4](https://forum.rigsofrods.org/threads/updated-installer-end-of-support-for-0-4-7-0.1613/) as a replacement to 0.4.7.0, followed by [RC5](https://forum.rigsofrods.org/threads/test-build-version-0-4-8-rc5.1900/) a few months later.

With RoR now considered 'stable enough' to do another stable release, we wanted to break away from release candidates. The original plan was to finally officially release 0.4.8.0, however compatibility issues with the Documents user folder (explained below) made it nearly impossible to correctly handle upgrades. After long discussions on Discord and GitHub([1](https://github.com/RigsOfRods/rigs-of-rods/issues/2415) / [2](https://github.com/RigsOfRods/rigs-of-rods/pull/2422)) we ultimately decided to change the version format.

### How does this affect me?

With the new version format, new releases will happen much more frequently.  Nearly every month, you'll be able to download a new version. These versions may be packed with new features or just have some minor bugfixes. Official releases will be more 'in-line' with our [development repository](https://github.com/RigsOfRods/rigs-of-rods/).

## User folder location change 

Since 0.38, the user directory, where mods and configuration files are stored, was named after the version number (`Rigs of Rods 0.38/0.39/0.4`). All 0.4 versions have used the same `Documents\Rigs of Rods 0.4` directory. Over time, the config file format has received major updates, making it increasingly difficult to be backwards compatible. In most cases, attempting to upgrade from older versions caused RoR to either outright crash or have other major glitches.

Starting with version 2020.01, the user directory has been moved to `Documents\My Games\Rigs of Rods`. The `My Games` folder is used by a large amount of modern Windows games to store configuration files, so it is fitting for RoR to use it as well. 

The user directory on Linux will remain in `~/.rigsofrods` for now.

### Mods

On first run, players with the old directory will receieve a notice about the directory change. To continue using your mods, you will have to move your mod directories (`mods` on recent RCs, or `packs`,`terrains`, and `vehicles` on older versions) to the new `My Games\Rigs of Rods` directory. RoR itself will not move the folders to prevent data loss. The [Installing content](/gameplay/installing-content/) page has been updated for the new directory. 

### Settings and input mappings

At the moment, players who already use 0.4.8 RC5 can move the `config` and `savegames` folders from `Documents\Rigs of Rods 0.4` to the new directory without issues. 

For those running older versions, **DO NOT** move the `config` or `savegames` folders. Version 2020.01 is not compatible with anything older than 0.4.8 RC5.

If you have input maps for controllers ([separate controller `.map` files](/images/controller-inputmaps.png), not an edited `input.map`!!) you will have to move those to the new `config` folder to continue using your input devices.

## End of 32 bit support 

Beginning with version 2020.01, Rigs of Rods will be for 64-bit systems only due to unfixable bugs with 32 bit builds. We're sorry for any inconvenience this may cause.
