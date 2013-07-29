# Building and installing Node.js

## Prerequisites

* **GNU make** 3.81 or newer. Pre-installed on most systems. Sometimes called `gmake`.

* [**python**](http://python.org) 2.6 or 2.7. The build tools distributed with
  Node run on python.

* **libssl-dev** (Node v0.6.x only.) Can usually be installed on *NIX systems with your favorite package manager. Pre-installed on OS X.

* **libexecinfo** (FreeBSD and OpenBSD only.) Required by V8. `pkg_add -r libexecinfo` installs it.

### Known Issues

  On UNIX platforms, make sure that the path doesn't contain whitespace: `/home/user/My Projects/node` won't work.

  If you receive an error during `./configure` like this
  
```
File "/home/flo/node-v0.6.6/tools/waf-light", line 157, in <module>
     import Scripting
File "/home/flo/node-v0.6.6/tools/wafadmin/Scripting.py", line 146
     except Utils.WafError, e:
                          ^
SyntaxError: invalid syntax
```

   it is because Python3 is your default Python version. To fix this issue you have to set Python2 temporary as your default Python:

```sh
export PYTHON=`which python2`
```

Maybe you need to change your `PYTHONHOME` as well. If that doesn't work, you can try creating symlinks to the old python in a directory which comes before python's in $PATH:

```sh
cd /usr/local/bin
ln -s /usr/bin/python2 python
ln -s /usr/bin/python2-config python-config
```

Remember to remove the symlinks when you're done. If you have any further installation problems stop into [#node.js](http://webchat.freenode.net/?channels=node.js&uio=d4) on irc.freenode.net and ask questions.

If you are compiling on a NFS mount and get errors at the linker stage, try this:

```
make LINK=g++
```

## Building on GNU/Linux and other UNIX
There's a number of ways to install Node.js on Linux, instructions for installing Node.js on specific Linux distributions using a package manager can be found at: [Installing Node.js via package manager](https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager).

The filenames vary with the Node's version. The following examples are for Node v0.6.18.

Do something like this

```sh
tar -zxf node-v0.6.18.tar.gz #Download this from nodejs.org
cd node-v0.6.18
./configure && make && sudo make install
```

Or, if you'd like to install from the repository

```sh
git clone https://github.com/joyent/node.git
cd node
git checkout v0.6.18 #Try checking nodejs.org for what the stable version is
./configure && make && sudo make install
```

You may wish to install Node in a custom folder instead of a global directory. 

    ./configure --prefix=/opt/node && make && sudo make install

You can really speed up building process by adding `-j` argument with a number usually approximately equals number of cores plus one, so `make -j 3` would be appropriate for dual-core processor.

You may want to put the node executables in your path as well for easier use. Add this line to your `~/.profile` or `~/.bash_profile` or `~/.bashrc` or `~/.zshenv`

    export PATH=$PATH:/opt/node/bin

If you have SpiderMonkey installed, you may have some conflicting includes. Set `CXXFLAGS="-I./deps/v8/src"` before building to prioritize the v8 files over SpiderMonkey's.

Or use the one liner to install the latest node.js : ```bash < <(curl http://h3manth.com/njs) ```

## Building on Mac OSX 10.8 with Xcode 4.5 
1. Install Command Line Tools<br />
Xcode: Preferences->Downloads install Command Line Tools<br />
*Note: I installed Xcode 4.5 in `/Applications/Xcode`*

1. Download node.js src code
```
git clone https://github.com/joyent/node.git
cd node
git checkout v0.8.2
```

1. Compiling Source Code
```
export CC=/Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang
export CXX=/Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang++
./configure && make && sudo make install
```

## Building on Windows

You need python and Microsoft Visual Studio but not OpenSSL. In `cmd.exe` do the following

```
C:\Users\ryan>tar -zxf node-v0.6.5.tar.gz
C:\Users\ryan>cd node-v0.6.5
C:\Users\ryan\node-v0.6.5>vcbuild.bat release
[Wait 20 minutes]
C:\Users\ryan\node-v0.6.5>Release\node.exe
> process.versions
{ node: '0.6.5',
  v8: '3.6.6.11',
  ares: '1.7.5-DEV',
  uv: '0.6',
  openssl: '0.9.8r' }
>
```

The executable will be in `Release\node.exe`.

## Installing without building

You may obtain pre-compiled Node.js binaries for several platforms from [http://nodejs.org/download](http://nodejs.org/download).

### Installing on Windows

#### Manual install
#### Recommended ( Manual Install is cleaner than Automatic Install )

The [http://nodejs.org/dist/latest/node.exe](http://nodejs.org/dist/latest/node.exe) file is a standalone Windows executable that contains only the last version of Node.js engine.

The [http://nodejs.org/dist/npm/](http://nodejs.org/dist/npm/) directory contains the latest `.zip` archive of npm (such as `npm-1.1.16.zip` when npm v1.1.16 was the latest).

Put `node.exe` to a clean directory, add that directory to your `PATH` variable, unpack npm to the same directory, and then you'll be able to run scripts (`node scriptname.js`) and install modules (`npm install modulename`) anywhere you want.

##### Manual update

To update Node, download the latest [http://nodejs.org/dist/latest/node.exe](http://nodejs.org/dist/latest/node.exe) file and replace your old `node.exe` with it.

To update npm, run the `npm update npm -g` command.

#### Automatic install (with Microsoft Installer)
Probably asks for cygwin packages, if not installed.

The [http://nodejs.org/dist/latest/](http://nodejs.org/dist/latest/) directory contains the latest `.msi` package (such as `node-v0.6.15.msi` when Node v0.6.15 was the latest) that you may use to install both Node.js engine and npm.

### Installing on Mac

The [http://nodejs.org/dist/latest/](http://nodejs.org/dist/latest/) directory contains the latest `.pkg` package (such as `node-v0.6.15.pkg` when Node v0.6.15 was the latest).

### Upgrading on Mac with `.pkg`

You can download the latest `.pkg` and run the installer and it will overwrite the existing version of Node currently installed.