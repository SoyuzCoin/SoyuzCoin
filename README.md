
Soyuz3 Core

Quick installation of the Soyuz3 daemon under linux.

Installation of libraries (using root user):

add-apt-repository ppa:bitcoin/bitcoin -y
apt-get update
apt-get install -y build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils
apt-get install -y libboost-system-dev libboost-filesystem-dev libboost-chrono-dev libboost-program-options-dev libboost-test-dev libboost-thread-dev
apt-get install -y libdb4.8-dev libdb4.8++-dev

Cloning the repository and compiling (use any user with the sudo group):

cd
git clone https://github.com/SoyuzCoin/SoyuzCoin.git
cd SoyuzCoin
./autogen.sh
./configure
sudo make install
cd src
sudo strip soyuz3d
sudo strip soyuz3-cli
sudo strip soyuz3-tx
cd ..

Running the daemon:

soyuz3d 

Stopping the daemon:

soyuz3-cli stop

Demon status:

soyuz3-cli getinfo
soyuz3-cli mnsync status

All binaries for different operating systems, you can download in the releases repository:

https://github.com/SoyuzCoin/SoyuzCoin/releases

P2P port: 31917, RPC port: 31918
