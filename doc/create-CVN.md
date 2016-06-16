# How to create a CVN
## 1 Compile and install the OpenSC smart card framework
First we need a recent version of the OpenSC framework. Most linux distributions use old versions that do not support the SmarCardHSM smart card.

In the HOWTO we suppose that you are going to install into the folder /opt/faircoin.
```
sudo apt-get install -y build-essential libtool autotools-dev autoconf pkg-config libssl-dev libboost-all-dev git libdb5.3-dev libdb5.3++-dev libqt4-core libqt4-gui libqt4-dev libqrencode-dev libprotobuf-dev protobuf-compiler libevent-dev libpcsclite-dev
mkdir /opt/faircoin && cd /opt/faircoin
git clone https://github.com/OpenSC/OpenSC.git
cd OpenSC
git checkout 0.16.0
./bootstrap
./configure --prefix=/opt/faircoin/OpenSC/target --sysconfdir=/opt/faircoin/OpenSC/target/etc
make -j`nproc`
make install
```
## 2 Compile the FairCoin2 wallet
```
cd /opt/faircoin
git clone https://github.com/FairCoinTeam/faircoin2
cd faircoin2
./autogen.sh
./configure --disable-tests --disable-bench --with-incompatible-bdb --with-gui=qt4 --with-opensc=/opt/faircoin/OpenSC
make -j`nproc`
```
## 3 Run the FairCoin2 wallet in CVN mode
There are two ways to run a CVN.
1. By using a smart card which contains all the information required
2. By using an x509 Key/certificate pair which containls all the information required (for testing only)

### 3.1 Using a smart card
The smart card is provided by the FairCoin development team. Once you have received the card & reader plug it into a USB port and start the wallet using the parameters
```-cvn=card -gen=1```
### 3.2 Using an x509 Key/certificate pair
The wallet searches for a file named cvn.pem in the FairCoin data directory (in Linux ~/.faircoin2)

Start the wallet with the arguments: ```-cvn=file -gen=1```
