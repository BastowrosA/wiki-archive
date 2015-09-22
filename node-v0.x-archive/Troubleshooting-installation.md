**NOTE:** Out of date.

If you encounter the following error on linux:

    error: could not configure a cxx compiler!

Run:

    sudo aptitude install build-essential

To permanently add node to the path in RHEL/Fedora, add it to your .bashrc by running:

    echo 'export PATH=$HOME/local/node/bin:$PATH' >> ~/.bashrc

If you have trouble building with the directions given try this (mac & maybe linux/bsd)  

in the root directory of the source code:  

    ./configure  
    make  
    sudo make install  

`configure` is currently broken for some versions of MacOS; for more details, see [How to compile Node.js v0.4.2 on MacOS 10.5.8](http://canonical.org/~kragen/compiling-node-on-macos.html). The working approach cited there is as follows:

    export PATH=/Developer/usr/bin:$PATH
    ISYSROOT="-isysroot /Developer/SDKs/MacOSX10.5.sdk"
    export LINKFLAGS=$ISYSROOT CXXFLAGS=$ISYSROOT CFLAGS=$ISYSROOT
    ./configure --prefix=$HOME --without-ssl
    make

Something in the libv8 build process seems to fail erratically when using ccache (on OS X with gcc4, anyway), so if you see errors building accessors.o, try removing ccache from your path.




    git clone --depth 1 https://github.com/joyent/node.git

returns this error:

    fatal: https://github.com/joyent/node.git/info/refs download error - The requested URL returned error: 403

got this working instead with

    git clone --depth 1 git://github.com/joyent/node.git



if you have bug:



    task failed (err #2):  	
    {task: uv uv.h -> uv.a}

use the stable version:



    git clone git://github.com/joyent/node.git
    cd node
    git checkout v0.4.11