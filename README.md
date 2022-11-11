# Asterisk Source for AllStarLink

This is the Asterisk source package for AllStarLink and the files to build the ASL 2.0.0+ distribution. This repo contains patches
for building AllStarLink on recent editions of Debian. Currently tested on Debian 11 Bullseye.

Debian 12 Bookworm is not supported for now because the kernel is too new and there is a missing dependency (libvpb-dev). Feel free to make a pull request if you have the solution :)

---------------------------------------------------------------------------------------------------------------------------------

AllStarLink Wiki: https://wiki.allstarlink.org

AllStarLink Community Forum: https://community.allstarlink.org/

AllStarLink Portal:  https://www.allstarlink.org

AllStarLink Node Stats:  https://stats.allstarlink.org

---------------------------------------------------------------------------------------------------------------------------------

## Prerequisites

#### Debian 11 Bullseye

* Install the ASL Repo

<pre>
sudo su
apt update
apt install -y curl gnupg
echo "deb http://apt.allstarlink.org/repos/asl_builds buster main" > /etc/apt/sources.list.d/allstar.list
curl -s http://apt.allstarlink.org/repos/repo_signing.key | apt-key add -
apt update
exit</pre>
</pre>

* Install apt dependencies
```
apt -y install quilt libreadline-dev libgsm1-dev libssl-dev libasound2-dev libpq-dev \
  unixodbc-dev libpri-dev libvpb-dev libnewt-dev libsqlite3-dev libspeex-dev \
  libspeexdsp-dev libcurl4-openssl-dev libpopt-dev libiksemel-dev freetds-dev libvorbis-dev \
  libsnmp-dev libcap-dev libi2c-dev libjansson-dev build-essential libtonezone-dev \
  git cmake g++ libboost-all-dev libgmp-dev swig python3-numpy asl-dahdi-source libusb-dev \
  libmxml-dev graphviz doxygen gsfonts devscripts
```

## Compiling
Packaging (.deb)

This will compile and package AllStar into .deb files. You do not need to run configure or make before doing this.

```
git clone https://github.com/F4HWD/ASL-Asterisk.git
cd ASL-Asterisk/asterisk
debuild -b -us -uc
```

.debs will appear in the repository root folder after compiling and packaging

If all goes well, you will have cloned, configured, compiled and installed the Astersisk 1.4.23pre and app_rpt suite of programs that comprise the ASL 2.0.0+ release onto your system.

## Install
You can now install all generated .deb files. Assuming you're still in asterisk folder

```
cd ..
sudo dpkg -i asl-asterisk*.deb
```

To install various scripts useful for AllStarLink, like the famous asl-menu. Assuming you're in the root of the repository

```
cd allstar
sudo make install
```

If you want a .deb package for these scripts, you can type the following command

```
debuild -b -us -uc
```

It will create an allstar-helpers***.deb in the root directory of the repository


## Dependencies
You will need DAHDI modules for your kernel. For the moment, there is no known method to succeed the compilation. You can use a pre-compiled package instead
For the linux-headers, I will use classic Debian. If you have a Raspberry Pi or if the command fails, please refer to the documentation of your distribution.

``` 
sudo apt install linux-headers-$(dpkg --print-architecture)
cd ~/
wget http://dvswitch.org/buster
chmod +x buster
sudo ./buster
rm buster
sudo apt remove -y asl-dahdi-linux asl-dahdi-source
sudo apt install -y allstar-dahdi-linux-dkms
```

Normally, the nodes list updates on its own. If not (impossible to connect to a node after a while), you can either compile the following repository ... : https://github.com/AllStarLink/ASL-Nodes-Diff

... or type the following commands to install it directly

```
wget https://github.com/AllStarLink/ASL-Nodes-Diff/releases/download/2.0.0-beta.5/asl-update-node-list_2.0.0-beta.5-1_all.deb
sudo dpkg -i asl-update-node-list_2.0.0-beta.5-1_all.deb
```

## Configuration
You can now configure your node

```
sudo asl-menu
```



---------------------------------------------------------------------------------------------------------------------------------

## Help

Community Forum: https://community.allstarlink.org/

AllStarLink Wiki: http://wiki.allstarlink.org

E-Mail: developers@allstarlink.org

---------------------------------------------------------------------------------------------------------------------------------

## Contributing

Please refer to the [Contributing](https://wiki.allstarlink.org/wiki/Contributing) page on the AllStarLink Wiki.

## Copyright

Asterisk 1.4.23pre is copyright Digium (https://www.digium.com)

app_rpt and associated programs (app_rpt suite) are copyright Jim Dixon, WB6NIL; 2018-2021 AllStarLink, Inc., and contributors

_(Refer to each individual's file source code for full copyright information)_

## License

Asterisk, app_rpt, and all associated code/files are licensed, released, and distributed under the GNU General Public License v2 and cannot be relicensed without written permission of Digium and the copyright holders of the app_rpt suite of programs.
