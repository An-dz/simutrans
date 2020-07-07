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

A Makefile and a Visual Studio solution are available in its directory.

# Contributing

The files `about-the-code.txt` and `coding_styles.txt` can give you a
head start on some quirks about the code and how you should style your
code.

Simutrans can accept any contribution as long as the core of the game,
being transportation simulation, is not reduced.

When sending pull requests we ask for small patches doing small things
at a time, even if it's part of a large project. The chances of your
code being merged are heavily boosted if you do so.

It's very common for long discussions about your patch to happen and
many change requests to follow, and even if you follow everything it
might still be denied. But don't take this harshly, we try to keep the
gameplay simple and intuitive for any player and the complexity of your
patch can be one of the reasons it did not make into the master branch.
Consensus is also another big factor on the future of a patch.

# How to compile

The instructions below expect that you at least know what the tools are
and what they do, as well as how to obtain the source code. They also
only point to a minimum easy compiling and not the bare-minimum.

The compiling will only generate the Simutrans executable, you still
need to have a [pakset](https://www.simutrans.com/paksets) and the
files that are available in the `simutrans` directory to actually run
the game.

You can use the `-use_workdir <path>` flag to let the executable know
where the `simutrans` directory is located so it can load the pakset
and the other needed files.

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

For the SDL2 back-end you need:
- libSDL2 <https://www.libsdl.org/>
- libSDL2_mixer (link from the same page)  
  This is if you want sound support.

SDL1 can also be used but it is deprecated.

Allegro support is also available but it lacks maintenance:
- liballeg <https://liballeg.org/>  
  Not compatible with Allegro 5

### Optional

- libfreetype <https://www.freetype.org/>  
  For scalable font support. (Recommended for High DPI screens)
- libminiupnpc <https://miniupnp.tuxfamily.org/>  
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

Our solution and project files are fully compatible with any version of
Visual Studio 2013 Update 2 or newer. Visual Studio 2012 can also open
it after accepting the conversion dialogue that opens when you load it
for the first time. Older versions will not work.

For the bare-minimum you need to install these individual components:
- Any VC++ build tools for MSVC  
  You can choose the latest version
- Any Windows 10 SDK  
  Works on Windows 7 and 8
- C++ Core Features  
  May also be named as C++ Main Resources depending on your language
- Re-distributable package  
  Needed to run but not required if you already have it installed

Or you can choose the _Game Development with C++_ workload, though it
will install some unnecessary packages as well.

Along with the dependencies already listed Visual Studio builds also
requires the Windows version of pthread which is available at
<https://sourceforge.net/projects/pthreads4w/>.

A package with all dependencies pre-compiled can be downloaded from our
[forum](https://forum.simutrans.com/index.php?topic=14226.0). You can
also compile them by yourself, the same link has important information
about compiling the dependencies.

The _Simutrans.sln_ file contains the projects for compiling with GDI
and SDL2 back-ends as well as a Server configuration for running on the
command line. By default GDI and SDL2 have _miniupnpc_ and _freetype_
enabled, change the pre-processor directives and linked libraries if
you don't want them.

Once you have the dependencies in place open the _Simutrans.sln_ file.
There are three compiling configurations:
- **Debug** is for development, it generates a non-optimised code with
debugging capabilities;
- **Stable** generates a stable build, you should only use this with
the sources of the stable release;
- **Release** is just like Stable but it adds commit information for
servers that don't want to run stable.

Once you choose your option, right-click over one of the projects, like
_Simutrans GDI_, and open the _Properties_. Make sure you are editing
the configuration you want and under **VC++ Directories** you should
add the _Include_ and _Library_ paths where the dependencies are
located so VS can use them.

Under **C/C++ -> Preprocessor** you can edit upnp and freetype support.
For removing them from being linked remove them under **Linker ->
Input**.

### Visual Studio Build Tools

The [build tools](https://visualstudio.microsoft.com/downloads/) only
installs the needed components for compiling with the command line.

Read the instruction from [Visual Studio](#visual-studio), they explain
the basics about the configurations, options and dependencies.

Once you have the build tools installed check your Start Menu for an
item titled **Developer Command Prompt** this will open the Command
Prompt with all paths already set up. Navigate to the Simutrans folder
and pass the project you want to build. Passing the _Simutrans.sln_
file to MSBuild will compile all three versions (GDI, SDL2, Server), to
compile only one version pass the _.vcxproj_ file instead.

For passing extra include and library paths, needed to tell where the
required libraries are located, use parameters _SimIncludePath_ and
_SimLibraryPath_.

The following will compile a _Stable_ version telling the libraries
headers are available in `<CurrentDir>\include\` and the lib files are
in `<CurrentDir>\lib\`.

```powershell
MSBuild Simutrans-GDI.vcxproj /c:Stable /p:SimIncludePath=include /p:SimLibraryPath=lib
```

### MSYS2 + MinGW

[MSYS2](https://www.msys2.org/) is a very small and easy to set-up
system for compiling on Windows with GCC. It's entirely used on the
command line.

You can install the [dependencies](#dependencies) with _pacman_, these
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

zlib and bzip2 are already installed so installing the brew version is
only for using a more up-to-date version. You'll have to manually edit
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

On MacOS Simutrans uses AVFoundation for media capabilities. This comes
by default with XCode (Homebrew installs it) on MacOS 10.7+ (Lion). For
older systems Simutrans will use QuickTime (also comes with Xcode), but
this back-end is deprecated.

## FreeBSD

You can install all [dependencies](#dependencies) with FreeBSD package
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

### Other BSD

Simutrans configure script is set up to offer Haiku support and is
known to compile without problems on it. You may need to install
_libtool_ to compile with static linking.

Other BSD systems, like OpenBSD, should fallback to using the FreeBSD
settings and should compile without problems as well.

## Server

If you want to compile Simutrans as a command line tool, for hosting a
server without graphical back-end, with GCC just call `configure` with
`--enable-server`. For Visual Studio compile the **Simutrans Server**
project inside the _Simutrans.sln_ file.
