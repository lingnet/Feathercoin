Feathercoin 0.9.3.2 
===================

Copyright (c) 2009-2016 Feathercoin Developers


Setup
-----------

[Feathercoin Core] is the original Feathercoin client and it builds the backbone of the network. However, it downloads and stores the entire history of Feathercoin transactions (which is currently several GBs); depending on the speed of your computer and network connection, the synchronization process can take anywhere from a few hours to a day or more. Thankfully you only have to do this once. 

Example UNIX Build from source
------------------------------

The Feathercoin wallet contains a number of features which require additional libraries to the Bitcoin build instructions.

### Quick build example for Ubuntu 16.04  

    sudo apt-get update ; sudo apt-get upgrade

    sudo apt-get install git  

    sudo apt-get install autoconf automake  debhelper dh-autoreconf  

    sudo apt-get install libssl-dev libdb++-dev libminiupnpc-dev binutils  

    sudo apt-get install autotools-dev  build-essential

    
### You need the Qt5 run-time libraries to build Feathercoin-Qt.  

    sudo apt-get install qtbase5-dev qttools5-dev-tools  

    sudo apt-get install libqt5printsupport5 libqt5opengl5-dev  

    sudo apt-get install libqjson-dev  

    sudo apt-get install libqt5gui5 libqt5core5a libqt5dbus5  

    sudo apt-get install libssl-dev debhelper

    sudo apt-get install libqrencode-dev pkg-config libprotobuf-dev  protobuf-compiler  

    sudo apt-get install libzxing  

    
### Download the .deb file or install the zxing binaries available after installing the Feathercoin PPA  


(http://forum.feathercoin.com/topic/8327/guide-feathercoin-wallet-ppa-and-binaries-on-ubuntu-and-debian-linux)  

As Super user (or sudo) create a file named **opensuse.list** in the directory 

    /etc/apt/sources.list.d 

For your OS, copy the command into /etc/apt/sources.list.d and save it.  
    
    deb http://download.opensuse.org/repositories/home:/wellenreiter01/xUbuntu_16.04 ./

download the repository key:
    wget http://download.opensuse.org/repositories/home:/wellenreiter01/Debian_7.0/Release.key    
   
Then add the key to your system:

    sudo apt-key add Release.key
    
    sudo apt-get update  
    sudo apt-get install libzxing  
 
 
### If PPA or .deb does not work, compile the zxing libraries yourself, download the sources from github.com.

Search for zxing-cpp to get the c++ version of the code.   

https://github.com/glassechidna/zxing-cpp

Build command for libzxing :  

sudo apt-get install cmake

cd zxing-cpp

mkdir build
cd build

export CXXFLAGS="-fPIC"
cmake -G "Unix Makefiles" .. -D_GLIBCXX_USE_CXX11_ABI=0 -DCMAKE_BUILD_TYPE=Release
make  
sudo make install   

   
### For Ununtu 16.04 - Edit : the zxing files source.  

sudo nano /usr/local/include/zxing/LuminanceSource.h

check Line 30 : is set to public 

### Install boost Libraries

    sudo apt-get install libboost-all-dev  

    sudo apt-get install libmessaging-menu-dev  

    cd Feathercoin  
    make clean
    rm configure
     ./autogen.sh
    ./configure --with-gui=qt5 --enable-tests=no  --with-incompatible-bdb --enable-upnp-default --with-qrcode=yes
    make  

    
Possible issues  
---------------- 

### Enable uPNP.   

--enable-upnp-default 


### Dependency issues with qr codes and zxing.  

--with-qrcode=no


### Use alternate database, 4.8 is still most portable.  

sudo apt-get install libdb5.3-dev  

--with-incompatible-bdb
   
### Build Berkley database version 4.8 from source.     

wget http://download.oracle.com/berkeley-db/db-4.8.30.NC.tar.gz
tar -xzvf db-4.8.30.NC.tar.gz
cd db-4.8.30.NC/build_unix/
…/dist/configure --enable-cxx
make
sudo make install

Example config usage :

./configure --disable-upnp-default --disable-tests --with-boost-libdir=/usr/lib/arm-linux-gnueabihf CPPFLAGS="-I/usr/local/BerkeleyDB.4.8/include -O2" LDFLAGS="-L/usr/local/BerkeleyDB.4.8/lib"

     
Running Feathercoin
---------------------
The following are some helpful notes on how to run Feathercoin on your native platform. 

### Unix

cd Feathercoin  
./feathercoin-qt  

### Windows

Unpack the files into a directory, and then run feathercoin-qt.exe.

### OSX

Drag Feathercoin-Qt to your applications folder, and then run Feathercoin-Qt.

### Need Help?

* Ask for support in the support section of https://forum.feathercoin.com
* If you find a bug, you also may raise an issue at: http://www.github.com/Feathercoin/Feathercoin/issues

Building
---------------------
The developer documentation can be found on http://www.github.com/Feathercoin/Feathercoin/tree/0.9.3/doc 

check for 

- [OSX Build Notes](build-osx.md)
- [Unix Build Notes](build-unix.md)
- [Windows Build Notes](build-msw.md)

Development
---------------------
The Feathercoin repo's [root README](https://github.com/Feathercoin/Feathercoin/tree/0.9.3/README.md) contains relevant information on the development process and automated testing.

- [Coding Guidelines](coding.md)
- [Multiwallet Qt Development](multiwallet-qt.md)
- [Release Notes](release-notes.md)
- [Release Process](release-process.md)
- [Source Code Documentation (External Link)](https://dev.visucore.com/feathercoin/doxygen/)
- [Translation Process](translation_process.md)
- [Unit Tests](unit-tests.md)

### Resources
- forum.feathercoin.com
- chat: forum.feathercoin.com/shoutbox


License
---------------------
Distributed under the [MIT/X11 software license](http://www.opensource.org/licenses/mit-license.php).
This product includes software developed by the OpenSSL Project for use in the [OpenSSL Toolkit](http://www.openssl.org/). This product includes
cryptographic software written by Eric Young ([eay@cryptsoft.com](mailto:eay@cryptsoft.com)), and UPnP software written by Thomas Bernard.
