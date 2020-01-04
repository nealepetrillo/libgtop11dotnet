# libgtop11dotnet (aka PKCS11dotNetV2)

This repository contains the source code for the libgtop11dotnet library. It is a [PKCS #11](https://en.wikipedia.org/wiki/PKCS_11) module for [Gemalto IDPrime .NET](http://www.gemalto.com/products/dotnet_card/index.html) smart cards.

This repository was forked from https://github.com/AbigailBuccaneer/libgtop11dotnet which was, in turn, created by importing the SVN repository from [smartcardservices.macosforge.org](https://svn.macosforge.org/repository/smartcardservices).

This fork includes updates to correct warnings for CentOS 7 targets as well as certain errors encourntered with building the software with GCC compilers greater than 4.8.5. The updates were inspired due to the discontinuation of the IDPrime .NET product (more information on which can be found [here](https://github.com/AbigailBuccaneer/libgtop11dotnet)) but the requiment to support the legacy cards in a Linux enviornment.

## Building

This information is based on [this invaluable guide](https://stomp.colorado.edu/blog/blog/2014/06/02/on-building-the-gemalto-net-pkcs-11-module-for-linux/):

### CentOS 7 / RHEL 7
```
sudo yum install git automake autoconf zlib-devel pcsclite-devel boost-devel
git clone https://github.com/nealepetrillo/libgtop11dotnet.git
cd libgtop11dotnet
./autogen.sh
./configure --enable-system-boost
make
sudo make install
```

### Debian 10 / Ubuntu 18
```
sudo apt install git automake autoconf pkg-config zlib1g-dev libpcsclite1 libpcsclite-dev libboost-all-dev 
git clone https://github.com/nealepetrillo/libgtop11dotnet.git
cd libgtop11dotnet
./autogen.sh
./configure --enable-system-boost
make
sudo make install
```

## Using

```
sudo apt install opensc-tool
# list the contents of the card:
pkcs11-tool --module=/usr/local/lib/libgtop11dotnet.so -O
# view the contents of an x509 certificate on the card
pkcs11-tool --module=/usr/local/lib/libgtop11dotnet.so -y cert -r \
  --id ${certificate_ID_from_previous_command} | openssl x509 -inform der -text -noout
```

## License

This source code is available under the GNU Lesser General Public License.
See the file `LGPL-2.1` for more information.
The source code contains the notice:

```
PKCS#11 library for .Net smart cards
Copyright (C) 2007-2009 Gemalto <support@gemalto.com>

This library is free software; you can redistribute it and/or
modify it under the terms of the GNU Lesser General Public
License as published by the Free Software Foundation; either
version 2.1 of the License, or (at your option) any later version.

This library is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
Lesser General Public License for more details.

You should have received a copy of the GNU Lesser General Public
License along with this library; if not, write to the Free Software
Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA  02110-1301  USA
```
