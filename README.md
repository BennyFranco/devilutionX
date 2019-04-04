<<<<<<< HEAD
[![Downloads](https://img.shields.io/github/downloads/diasurgical/devilutionX/total.svg)](https://github.com/diasurgical/devilutionX/releases)
[![github stars](https://img.shields.io/github/stars/diasurgical/devilutionX.svg)](https://github.com/diasurgical/devilutionX/stargazers)

Status | Platform
---:| ---
[![CircleCI](https://circleci.com/gh/diasurgical/devilutionX.svg?style=svg)](https://circleci.com/gh/diasurgical/devilutionX) | Linux 32bit & 64bit, Windows 32bit
[![Build Status](https://travis-ci.org/diasurgical/devilutionX.svg?branch=master)](https://travis-ci.org/diasurgical/devilutionX) | macOS 32bit & 64bit

[Discord Channel](https://discord.gg/aQBQdDe)

# DevilutionX
Diablo build for modern operating systems

# How To Play:
 - Copy diabdat.mpq from your CD, or GoG install folder, to the DevilutionX game directory ; Make sure it is all lowercase.
 - [Download DevilutionX](https://github.com/diasurgical/devilutionX/releases), or build from source
 - Install SDL2 (including SDL2_mixer and SDL2_ttf) make sure to get the appropriate 32bit or 64bit version.
 - Run `./devilutionx`

### Building devilutionX (native Linux build)
Note: Since 64-bit builds are currently not in a playable state, it is advised to build in a 32-bit environment. Another possibility is a 32-bit build on a multilib system (see below).

Install the dependencies on your machine:
```
sudo apt-get install cmake g++ libsdl2-dev libsdl2-mixer-dev libsdl2-ttf-dev libsodium-dev
```

Now run the following commands:
```
mkdir build
cd build
cmake ..
make -j$(nproc)
```

*Arguments to cmake:*

The default build type is `Debug`. This can be changed with `-DBINARY_RELEASE=ON`. Independently of this, the debug mode of the Diablo engine is always enabled by default. It can be disabled with `-DDEBUG=OFF`. Finally, in debug builds the address sanitizer is enabled by default. This can be disabled with `-DASAN=OFF`.

*To run the game:*

 - Copy the compiled devilution executable to your Diablo directory.
 - Copy the "diablodat.mpq" from your Diablo CD to the Diablo directory and make sure it is LOWERCASE.
 - Run `./devilution`

Please keep in mind that this is still being worked on and is missing parts of UI and SoundEffects are not properly playing now.

### Building deviltuionX 32-bit on 64-bit Linux (multilib) platforms
Install the dependencies on your machine:
```
sudo apt-get install cmake g++-multilib libsdl2-dev:i386 libsdl2-mixer-dev:i386 libsdl2-ttf-dev:i386 libsodium-dev libsodium-dev:i386
```

Now run the following commands:
```
mkdir build
cd build
linux32 cmake -DCMAKE_TOOLCHAIN_FILE=../CMake/32bit.cmake ..
linux32 make -j$(nproc)
```

### Cross-compiling for Windows via MinGW
Install the dependencies on your machine:

Download and place the 32bit MinGW Development Libraries of [SDL2](https://www.libsdl.org/download-2.0.php), [SDL2_mixer](https://www.libsdl.org/projects/SDL_mixer/), [SDL2_ttf](https://www.libsdl.org/projects/SDL_ttf/) and [Libsodium](https://github.com/jedisct1/libsodium/releases) in `/user/i686-w64-mingw32`.

```
sudo apt-get install cmake gcc-mingw-w64-i686 g++-mingw-w64-i686
```
Use `-DCROSS_PREFIX=/path/to/prefix` if the `i686-w64-mingw32` directory is not in `/usr`.

Now run the following commands:
```
mkdir build
cd build
cmake -DASAN=OFF -DCMAKE_TOOLCHAIN_FILE=../CMake/mingwcc.cmake ..
make -j$(nproc)
```

### Building devilutionX on macOS

#### Building with Xcode Build (x86 only)

Install Xcode 9.4.1 and Xcode Command Line tools, this is the last version with support for **32 bits**

Note: Be sure that your to select the command line Xcode if you have two or more installed, for example:

```
$ sudo xcode-select --switch /Applications/Xcode.app
```

Install the some tools using [Homebrew](https://brew.sh/):
```
brew install automake autoconf libtool
```

Get and build the dependencies
```
$ ./xcode-build.sh --get-libs --build-libs
```

Build the devilutionX project
```
$ ./xcode-build.sh --build-project
```

The result bundle should be in the **build** folder

To create a **dmg** execute
```
$ ./xcode-build.sh --package
```

If you want use Xcode to build and debug, you can find the project inside Xcode folder

#### Building for x64 with CMake
Note: macOS is 64-bit only so this is not fully playable at this point.

Install the dependencies using [Homebrew](https://brew.sh/):
```
brew install cmake sdl2_mixer sdl2_ttf libsodium pkg-config
```

Now run the following commands:
```
mkdir build
cd build
cmake ..
make -j$(sysctl -n hw.physicalcpu)
```

# Installing
Once compiled, the devilutionx binary will serve as a replacement for `Diablo.exe`. The following files from the original game patched to 1.09(b) need to be present: `diabdat.mpq`. If `COPYPROT` was defined when compiling, the Diablo CD will also be required.

# Multiplayer
 - TCP/IP only requires the host to expose port 6112
 - UPD/IP requires that all players expose port 6112

All games are encrypted and password protected.

# Contributing
[Guidelines](docs/CONTRIBUTING.md)

# Modding
Here are some screenshots of a few things I tinkered around with, to demonstrate the relative ease of improving the game:

![Screenshot 1: Monster lifebar+items](https://s33.postimg.cc/6xnnhhlmn/diabuimon.png "Monster lifebar+items")

![Screenshot 2: New trade screen](https://s22.postimg.cc/5i5k91vht/diabstore.png "New trade screen, items that couldn't spawn")

# F.A.Q.
> Wow, does this mean I can download and play Diablo for free now?

No, you'll need access to the data from the original game. To get a legitimate copy of the game assets, please refer to the [GoG release of Diablo 1](https://www.gog.com/game/diablo).
> Ok, so I'm playing DevilutionX now and all the sudden it crashed. NOW WHAT??

Open an issue and provide as much information as possible (OS version, etc.) including any crash logs.
> I thought I'd fix the crash myself, but after looking at the code its a disaster. Do you speak v2-34-v8?

That is the result of decompiled code. Whenever a program is compiled, much of the source is optimized and stripped away, so it's nearly impossible to decompile it back. Have patience. Everything will be cleaned up eventually. :)

# Credits
- [sanctuary](https://github.com/sanctuary) - extensively documenting Diablo's game engine
- [BWAPI Team](https://github.com/bwapi) - providing library API to work with Storm
- [Ladislav Zezula](https://github.com/ladislav-zezula) - reversing PKWARE library, further documenting Storm
- [fearedbliss](https://github.com/fearedbliss) - being awe-inspiring
- Climax Studios & Sony - secretly helping with their undercover QA :P
- Blizzard North - wait, this was a typo!
- Depression - reason to waste four months of my life doing this ;)

# Legal
This software is being released to the Public Domain. No assets of Diablo are being provided. You must own a copy of Diablo and have access to the assets beforehand in order to use this software.

Battle.net(R) - Copyright (C) 1996 Blizzard Entertainment, Inc. All rights reserved. Battle.net and Blizzard Entertainment are trademarks or registered trademarks of Blizzard Entertainment, Inc. in the U.S. and/or other countries.

Diablo(R) - Copyright (C) 1996 Blizzard Entertainment, Inc. All rights reserved. Diablo and Blizzard Entertainment are trademarks or registered trademarks of Blizzard Entertainment, Inc. in the U.S. and/or other countries.

This software is in no way associated with or endorsed by Blizzard Entertainment(R).
=======
[![Downloads](https://img.shields.io/github/downloads/diasurgical/devilutionX/total.svg)](https://github.com/diasurgical/devilutionX/releases)
[![github stars](https://img.shields.io/github/stars/diasurgical/devilutionX.svg)](https://github.com/diasurgical/devilutionX/stargazers)

Status | Platform
---:| ---
[![CircleCI](https://circleci.com/gh/diasurgical/devilutionX.svg?style=svg)](https://circleci.com/gh/diasurgical/devilutionX) | Linux 32bit & 64bit, Windows 32bit
[![Build Status](https://travis-ci.org/diasurgical/devilutionX.svg?branch=master)](https://travis-ci.org/diasurgical/devilutionX) | macOS 32bit & 64bit

![Discord Channel](https://avatars3.githubusercontent.com/u/1965106?s=16&v=4) [Discord Chat Channel](https://discord.gg/aQBQdDe)

# How To Play:
 - Copy diabdat.mpq from your CD, or GoG install folder, to the DevilutionX game directory ; Make sure it is all lowercase.
 - [Download DevilutionX](https://github.com/diasurgical/devilutionX/releases), or build from source
 - Install SDL2 (including SDL2_mixer and SDL2_ttf) make sure to get the appropriate 32bit or 64bit version.
 - Run `./devilutionx`

Please keep in mind that this is still being worked on and is missing parts of UI and some minor bugs, see [milestone 1](https://github.com/diasurgical/devilutionX/milestone/1) for a full list of known issues.

# Building from Source
## 32-bit building on 64-bit platforms
<details><summary>Linux</summary>

### Installing dependencies on Debian and Ubuntu
```
sudo apt-get install cmake g++-multilib libsdl2-dev:i386 libsdl2-mixer-dev:i386 libsdl2-ttf-dev:i386 libsodium-dev libsodium-dev:i386
```
### Installing dependencies on Fedora
```
sudo dnf install cmake glibc-devel.i686 SDL2-devel.i686 SDL2_ttf-devel.i686 SDL2_mixer-devel.i686 libsodium-devel.i686 libasan.i686
```
### Compiling
```
mkdir build
cd build
linux32 cmake -DCMAKE_TOOLCHAIN_FILE=../CMake/32bit.cmake ..
linux32 make -j$(nproc)
```
</details>
<details><summary>macOS</summary>

### Installing dependencies
Install [Xcode 9.4.1 and Xcode Command Line tools](https://developer.apple.com/download/more/?=xcode%209.4.1), this is the last version with **32 bits** support.

Note: Be sure that your to select the command line Xcode if you have more then one installed:
```
$ sudo xcode-select --switch /Applications/Xcode.app
```
Install the build tools using [Homebrew](https://brew.sh/):
```
brew install automake autoconf libtool
```
Get SDL2, SDL2_mixer, SDL2_ttf and Libsodium:
```
./xcode-build.sh --get-libs
```
### Compiling
```
./xcode-build.sh --build-libs
./xcode-build.sh --build-project
./xcode-build.sh --package
```
</details>
<details><summary>Windows via MinGW</summary>

### Installing dependencies on Debian and Ubuntu

Download and place the 32bit MinGW Development Libraries of [SDL2](https://www.libsdl.org/download-2.0.php), [SDL2_mixer](https://www.libsdl.org/projects/SDL_mixer/), [SDL2_ttf](https://www.libsdl.org/projects/SDL_ttf/) and [Libsodium](https://github.com/jedisct1/libsodium/releases) in `/user/i686-w64-mingw32`.

```
sudo apt-get install cmake gcc-mingw-w64-i686 g++-mingw-w64-i686
```
### Compiling
```
mkdir build
cd build
cmake -DASAN=OFF -DCMAKE_TOOLCHAIN_FILE=../CMake/mingwcc.cmake ..
make -j$(nproc)
```
</details>

## Building for the native platform
*Note: Since 64-bit builds are currently not in a playable state, it is advised to build in a 32-bit environment. Another possibility is a 32-bit build on a 64-bit system (see above).*
<details><summary>Linux</summary>

### Installing dependencies on Debian and Ubuntu
```
sudo apt-get install cmake g++ libsdl2-dev libsdl2-mixer-dev libsdl2-ttf-dev libsodium-dev
```
### Compiling
```
mkdir build
cd build
cmake ..
make -j$(nproc)
```
</details>
<details><summary>macOS</summary>

Install the dependencies using [Homebrew](https://brew.sh/):
```
brew install cmake sdl2_mixer sdl2_ttf libsodium pkg-config
```
### Compiling
```
mkdir build
cd build
cmake ..
make -j$(sysctl -n hw.physicalcpu)
```
</details>

## CMake arguments
### General
The default build type is `Debug`. This can be changed with `-DBINARY_RELEASE=ON`. Independently of this, the debug mode of the Diablo engine is always enabled by default. It can be disabled with `-DDEBUG=OFF`. Finally, in debug builds the address sanitizer is enabled by default. This can be disabled with `-DASAN=OFF`.
### mingw32
Use `-DCROSS_PREFIX=/path/to/prefix` if the `i686-w64-mingw32` directory is not in `/usr`.


# Multiplayer
 - TCP/IP only requires the host to expose port 6112
 - UPD/IP requires that all players expose port 6112

All games are encrypted and password protected.

# Contributing
[Guidelines](docs/CONTRIBUTING.md)

# Modding
Below are a few examples of some simple improvements made to the game. It is planned in the future to create tools for designing dungeons and graphics.

![Screenshot 1: Monster lifebar+items](https://github.com/diasurgical/scalpel/blob/master/screens/mod1.png)

![Screenshot 2: New trade screen](https://github.com/diasurgical/scalpel/blob/master/screens/mod2.png)

# F.A.Q.
<details><summary>Click to reveal</summary>

> Wow, does this mean I can download and play Diablo for free now?

No, you'll need access to the data from the original game. If you don't have an original CD then you can [buy Diablo from GoG.com](https://www.gog.com/game/diablo).
> Cool, so I fired your mod up, but there's no 1080p or new features?

We're working on it.
> After looking at the code some of it is a disaster

That is the result of decompiled code. Whenever a program is compiled, much of the source is optimized and stripped away, so it's nearly impossible to decompile it back. Have patience. Everything will be cleaned up eventually. :)
> What about Hellfire?

Hellfire was a bit of a flop on the developer's part. Support may come in the future once the base game is finished.
</details>

# Credits
- Reverse engineered by GalaXyHaXz in 2018
- [sanctuary](https://github.com/sanctuary) - extensively documenting Diablo's game engine
- [BWAPI Team](https://github.com/bwapi) - providing library API to work with Storm
- [Ladislav Zezula](https://github.com/ladislav-zezula) - reversing PKWARE library, further documenting Storm
- [fearedbliss](https://github.com/fearedbliss) - being awe-inspiring
- Climax Studios & Sony - secretly helping with their undercover QA :P
- Blizzard North - wait, this was a typo!
- Depression - reason to waste four months of my life doing this ;)

And a special thanks to all the support and people who work on Devilution to make it possible! <3

# Legal
Devilution is released to the Public Domain. The documentation and function provided by Devilution may only be utilized with assets provided by ownership of Diablo.

Battle.net(R) - Copyright (C) 1996 Blizzard Entertainment, Inc. All rights reserved. Battle.net and Blizzard Entertainment are trademarks or registered trademarks of Blizzard Entertainment, Inc. in the U.S. and/or other countries.

Diablo(R) - Copyright (C) 1996 Blizzard Entertainment, Inc. All rights reserved. Diablo and Blizzard Entertainment are trademarks or registered trademarks of Blizzard Entertainment, Inc. in the U.S. and/or other countries.

Devilution and any of its' maintainers are in no way associated with or endorsed by Blizzard Entertainment(R).
>>>>>>> fc9cb19ca4d831cc514e5c037cc0acb073603aed
