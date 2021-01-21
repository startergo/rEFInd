# NextLoader-UDK
## Overview
UDK2018 Environment for Building the NextLoader Boot Manager.

Build instructions:
# Building NextLoader on Mac OS
These are step-by-step instructions for setting up a bespoke Tianocore EDK II build environment for buidling NextLoader on Mac OS.

These steps have been verified on Mac OS v10.12 (Sierra) and Mac OS v10.14 (Mojave) and should also work on Mac OS v10.13 (High Sierra) and Mac OS v10.15 (Catalina).


## Activate Mac OS Development Tools

### Xcode
Download [Xcode](https://developer.apple.com/xcode) from the Mac App Store and install.
**NB:** Tested on Xcode v9.4.1 and v11.3 but should also work on v10.x and v12.x

### Xcode Commandline Tools
After installing Xcode, you will additionally need to install commandline tools.  To do this, at a Terminal prompt, enter:

```
$ xcode-select --install
```

### HomeBrew

#### Installing HomeBrew

While Xcode provides a full development environment as well as a suite of different utilities, it does not provide all tools required for Tianocore EDK II development.  These tools can be provided in a number of ways, but the two most popular ways come from HomeBrew and MacPorts.  This guide focuses on `HomeBrew` but equivalent steps can be taken in MacPorts.

If you do not have HomeBrew already installed, go to the [HomeBrew Home Page](https://brew.sh) and follow the instructions. Installation involves copying and pasting a one-line code string into Terminal and pressing `Enter`.

#### Update the PATH Environment Variable

Tools installed using HomeBrew are placed in `/usr/local/bin` which is non-standard to avoid conflicts with pre-installed tools.  The `PATH` environment variable must therefore be updated so newly installed tools are found.

```
$ export PATH=/usr/local/bin:$PATH
```

### Install the MTOC Utility with HomeBrew

The mtoc utility is required to convert the Mac OS Mach-O image format to the PE/COFF format required by the UEFI specifications.

```
$ brew install mtoc
$ brew upgrade mtoc
```

### Install the Netwide Assembler (NASM) with HomeBrew

The assembler used for Tianocore EDK II builds is the Netwide Assembler (NASM).

```
$ brew install nasm
$ brew upgrade nasm
```

### Install the ACPI Compiler with HomeBrew

The ASL compiler is required to build code in ACPI Source Language for Tianocore EDK II firmware builds.

```
$ brew install acpica
$ brew upgrade acpica
```

### Install the QEMU Emulator with HomeBrew (Optional)

The QEMU emulator from http://www.qemu.org/ is required to enable UEFI support on virtual machines.

```
$ brew install qemu
$ brew upgrade qemu
```

## Prepare the Bespoke TianoCore EDK II (UDK2018) Environment
### Fork the NextLoader-UDK Repository

Navigate to `https://github.com/startergo/NextLoader-UDK` and fork the repository

### Clone the Forked NextLoader-UDK Repository
In Terminal, create a `NextLoader` folder under your `Documents` folder, `cd` to that directory and clone the "NextLoader Ready" TianoCore EDK II (UDK2018) repository into an `edk2` folder:

```
$ mkdir ~/Documents/NextLoader
$ cd ~/Documents/NextLoader
$ git clone https://github.com/YOUR_GITHUB_USERNAME/NextLoader-UDK.git edk2
$ cd ~/Documents/NextLoader/edk2
$ git checkout main
$ git remote add upstream https://github.com/startergo/NextLoader-UDK.git
```

**NB:** Replace `YOUR_GITHUB_USERNAME` above with your actual GitHub User Name.

Your local `NextLoader-UDK` repository will be under `Documents/NextLoader/edk2`

### Build Required BaseTools C Tool Binaries

```
$ cd ~/Documents/NextLoader/edk2
$ make -C BaseTools/Source/C
```


## Prepare the NextLoader Environment
### Fork the NextLoader Repository

Navigate to `https://github.com/startergo/NextLoader` and fork the repository

### Clone the Forked NextLoader Repository

In Terminal, clone the forked `NextLoader` repository into a `Working` folder under your `NextLoader` folder:

```
$ cd ~/Documents/NextLoader
$ git clone https://github.com/YOUR_GITHUB_USERNAME/NextLoader.git Working
$ cd ~/Documents/NextLoader/Working
$ git checkout NextLoader
$ git remote add upstream https://github.com/startergo/NextLoader.git
```

**NB:** Replace `YOUR_GITHUB_USERNAME` above with your actual GitHub User Name.

Your local `NextLoader` repository will be under `Documents/NextLoader/Working`


## Build NextLoader
- Navigate to your `/Documents/NextLoader/edk2/000-BuildScript` folder in Finder
- Drag the `NextLoaderBuilder.sh` file into Terminal
  - Enter a space and `MyEdits`, or any other branch name, to the end of the line if you want to build on that branch
  - If nothing is entered, the script will build on the default `NextLoader` branch
- Press `Enter`


## Syncing Your Repositories with Upstream Repositories
### Sync with the RepoUpdater Script (Recommended)
- Navigate to your `/Documents/NextLoader/edk2/000-BuildScript` folder in Finder
- Drag the `RepoUpdater.sh` file into Terminal
- Press `Enter`

### Sync Manually
#### NextLoader-UDK
In Terminal, run the following commands:

```
$ cd ~/Documents/NextLoader/edk2
$ git checkout main
$ git pull upstream main
$ git push
```

#### NextLoader

In Terminal, run the following commands:

```
$ cd ~/Documents/NextLoader/Working
$ git checkout master
$ git pull origin master
$ git push
```
