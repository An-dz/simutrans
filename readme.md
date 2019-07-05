# Simutrans

Simutrans is a transportation business simulator where the player can a
transport passengers, mails and goods by many different transportation
options.

Simutrans started in 1997. You can find more information about the game
on our [official site](https://www.simutrans.com/).

## Makeobj

Makeobj is a command line tool to create new objects for Simutrans. It
joins image and data files into a single optimised pak-file that can be
used on Simutrans.

# How to compile

The instructions below expect that you at least know what the tools are
and what they do, as well as how to obtain the source code. They also
only point to a minimum easy compiling and not the bare-minimum.

## Dependencies

### Required

To compile you will need the following libraries:
- libz <https://www.zlib.net/>
- libbz2 <https://sourceware.org/bzip2/>
- libpng <http://www.libpng.org/pub/png/libpng.html>  
  Only required to compile makeobj, the tool that creates pak files
  for the game.

### Back-ends

If you want to compile Simutrans as a command line tool, for a server,
you don't need to install any back-end library.

On Windows you can compile with GDI back-end and it does not require
any library to be installed as it comes with any compilation system.

For the recommended SDL2 back-end you need:
- libSDL2 <http://www.libsdl.org/>
- libSDL2_mixer (link from the same page)  
  This is if you want sound support.

SDL1 can also be used but it is deprecated.

Allegro support is also available but it lacks maintenance:
- liballeg <https://liballeg.org/>  
  Not compatible with Allegro 5

### Optional

- libfreetype <http://www.freetype.org/>  
  For scalable font support. (Recommended for High DPI screens)
- libminiupnpc <http://miniupnp.free.fr/>  
  For easily creating new servers with a single click.

## Linux

On Linux you should be able to install all dependencies with your
distro package manager (Ubuntu apt-get, Arch pacman, Fedora yum, etc).
On some distros the packages with the development files have a -dev or
-devel in their names so install them as well.

Make sure you have GNU make, GCC, autoconf and pkg-config installed as
well and you can get it compiling with:

```sh
autoconf
./configure
make
```

## Windows

### Visual Studio

Microsoft offers a free version of Visual Studio called Community for
open-source, academic and one-man development that can be downloaded
[here](https://visualstudio.microsoft.com/vs/community/).

For the bare-minimum you need to install these individual components:
- Any C++ build tools for MSVC  
  You can choose the latest version
- Any Windows 10 SDK  
  Works on Windows 7 and 8
- Main C++ Resources

Or you can choose the _Game Development with C++_ workload, though it
will install some unnecessary packages.

Along with the dependencies already listed Visual Studio builds also
requires the Windows version of pthread which is available at
<https://sourceforge.net/projects/pthreads4w/>.

A package with all dependencies pre-compiled can be downloaded from our
[forum](). You can also compile them by yourself.

The _Simutrans.sln_ file compiles for the GDI back-end, while the
_Simutrans-SDL2.sln_ file compiles, obviously, for the SDL2 back-end.
By default both have _miniupnpc_ and _freetype_ enabled, change the
pre-processor directives if you don't want them.

### Visual Studio Build Tools

The [build tools](https://visualstudio.microsoft.com/downloads/) only
installs the needed components for compiling with the command line.
This option, like the MSYS2 option, can be used to work with Visual
Studio Code or SublimeText.

Follow the instruction from [Visual Studio](#visual-studio). They can
differ in some small points though.

### MSYS2 + MinGW

[MSYS2](https://www.msys2.org/) is a very small and easy to set-up
system for compiling on Windows with GCC. It's entirely used on the
command line.

You can install the [Dependencies](#dependencies) with _pacman_, these
are the name of the packages:
- mingw-w64-i686-zlib
- mingw-w64-i686-bzip2
- mingw-w64-i686-SDL
- mingw-w64-i686-SDL_mixer
- mingw-w64-i686-SDL2
- mingw-w64-i686-SDL2_mixer
- mingw-w64-i686-freetype
- mingw-w64-i686-miniupnpc
- mingw-w64-i686-libpng

You'll also need the following installed:
- make
- autoconf
- mingw-w64-i686-gcc
- mingw-w64-i686-pkg-config

Once everything is installed you just compile as any GCC/make code with
MSYS2 MinGW 32bits:

```sh
autoconf
./configure
make
```

## MacOS

It's not recommended to compile with the GCC bundled with Xcode as it's
too outdated and possibly Simutrans can't be compiled with it. Instead
use Clang for compiling.

The easiest option is to use [Homebrew](https://brew.sh/), a package
manager for MacOS. The package names of the dependencies are:
- sdl2
- sdl2_mixer
- freetype
- miniupnpc
- libpng

zlib and bzip2 are already installed so installing the brew version is only for using a more up-to-date version. You'll have to manually edit
the build to use these newer versions of the lib.

Other packages you'll need are:
- autoconf
- pkg-config

Then you can just call these to start compiling:

```sh
autoconf
./configure
make
```

## FreeBSD

You can install all [Dependencies](#dependencies) with FreeBSD package
manager _pkg_. The name of the packages are:
- lzlib
- bzip2
- sdl2
- sdl2_mixer
- freetype2
- miniupnpc
- png

Along with the dependencies listed above you'll also need:
- gcc
- gmake
- autoconf
- pkgconf

Here are the commands to run from inside the Simutrans directory:

```sh
autoconf
./configure
gmake
```

## Server

If you want to compile Simutrans as a command line tool, for hosting a
server without graphical back-end, with GCC just call `configure` with
`--enable-server`. For Visual Studio use the _Simutrans-server.sln_ file.


Congratulations, you checked out the simutrans source. To compile it,
you have many options, either using Microsoft Visual C++ Express (which
is free in Version 7.0 or up) or some GCC variant including clang.


To make life easier, you can follow the instructions to compile OpenTTD:
http://wiki.openttd.org/Category:Compiling_OpenTTD
A system set up for OpenTTD will also compile simutrans (except for
bzlib2, see below sections).

If you are on a MS Windows machine, download either MS VC Express or
MSYS2. MSVC is easy for debugging, MSYS2 is easy to set up (but it has to 


To built on Haiku you must use GCC4 (type "setarch x86" in the current
nightlies). To incorporate bz2lib, download make bz2lib and add them
manually (via FLAGS = -I/dwonloadeddir -L/downloadeddir). However, simutrans
has a Haikuporter package, which may built the lastest version.

A subversion will be also a good idea. You can find some of them on:
http://subversion.tigris.org/
or you some other client.

Check out the latest source from the SVN or check out a certain revision.
I recommend always to use the latest source, since it does not make any
sense to work with buggy code.

The address is:
svn://servers.simutrans.org/simutrans

A commandline would look like this:
svn checkout svn://servers.simutrans.org/simutrans

If everything is set up, you can run configure inside trunk. This should 
create a config.default file with all the needed settings. Try to compile 
using make. You can manually fine edit config.default to enable other 
settings.

Typical you type into a command window:
./configure
make

The executable compiled by this is located in the directory "build/default", 
i.e. "./build/default/sim" You can start it by this
cd simutrans
../build/default/sim -use_workdir
but you will need to add at least one pak to the simutrans directory.

You can run ./distribute which will give you a zip file that contains 
everything (minus a pak) needed to run simutrans.


IMPORTANT:
----------

If you want to contribute, read the coding guidelines in
trunk/coding_styles.txt


The following instructions are manual setup for GCC systems:
------------------------------------------------------------

Finally type make. If you want a smaller program and do not care about error
messages, you can comment out #DEBUG=1 and run strip sim resp. strip sim.exe
after compile and linking.


The following instructions are for MS Visual C Express:
-------------------------------------------------------

For debugging, you have to set the correct working directory, i.e. the
directory where the pak/ folders are located and use the -use_workdir
command line option.
