Bitmonk (BMO) daemons
==========

Bitmonk - it's the MN/POS/POW(scrypt) cryptocurrency, part of the decentralized exchange system Coinmonkey 2.0 and MonkTtadeX protocol. Repository contain the source of [Ubuntu 16.04](https://coinmonkey.io/donload/bitmonkd) and [Windows](https://coinmonkey.io/donload/bitmonkd.exe) daemons. You can download the wallet [here](https://github.com/coinmonkey/Bitmonk-wallet).

![coinmonkey](https://coinmonkey.io/images/logo.png)

[bitmonk.coinmonkey.io](http://bitmonk.coinmonkey.io) - for getting more information about cryptocurrency and project.

Compilation
==========

*git clone ...
*cd src
*change path to libs in makefile.mingw for Windows and makefile.unix for Linux

For Windows (in MINWG32 console):
*sd bitmonk/src/leveldb
*TARGET_OS=NATIVE_WINDOWS make libleveldb.a libmemenv.a

In CMD console:
*cd src
*mingw32-make -f makefile.mingw
*strip bitmonkd.exe
  
For Linux (Ubuntu 16.04)
*sudo apt-get update
*sudo apt-get upgrade -y
*sudo apt-get install build-essential libssl-dev libdb++-dev libboost-all-dev libqrencode-dev autoconf automake libgmp3-dev miniupnpc libminiupnpc-dev
*chmod -R 0755 src
*cd leveldb
*make clean
*make libleveldb.a libmemenv.a
*cd ..
*make -f makefile.unix
*strip bitmonkd

Launch
==========

bitmonkd[.exe] -reindex -daemon

Settings in /root/.Bitmonk/Bitmonk.conf

`rpcuser=p1
rpcpassword=p2
rpcallowip=127.0.0.1
staking=1
listen=1
server=1
txindex=1
daemon=1
addnode=138.68.81.193
addnode=46.101.102.37
addnode=207.154.210.39
`

For mining
==========
minerd --url=http://127.0.0.1:37771 --userpass=p1:p2 -t3 --coinbase-addr=Y6wdwsoC7WWR2R3HK49RkRNHU9cXVEcQpM

[More info](https://bitcointalk.org/index.php?topic=55038.0)

Masternode install
==========

You should send 250000 coins to the new address and wait 15 confirmations. In Windows wallet console:

*bitmonkd masternode genkey
*bitmonkd masternode outputs

Bitmonk.conf on Linux:
masternode=1
masternodeprivkey=getkey

masternode.conf on Windows:
mn1 IPLinuxServer:37770 genkey output1 output2

For check status: bitmonkd masternode status
For start one: bitmonkd.exe masternode start-alias mn1
For start all: bitmonkd.exe masternode start-many
For stop one: bitmonkd.exe masternode stop-alias mn1
For stop all: bitmonkd.exe masternode stop-many

Statuses:
MASTERNODE_NOT_PROCESSED: 0 
MASTERNODE_IS_CAPABLE: 1 
MASTERNODE_NOT_CAPABLE: 2 
MASTERNODE_STOPPED: 3
MASTERNODE_INPUT_TOO_NEW: 4
MASTERNODE_PORT_NOT_OPEN: 6
MASTERNODE_PORT_OPEN: 7
MASTERNODE_SYNC_IN_PROCESS: 8
MASTERNODE_REMOTELY_ENABLED: 9

Ports
==========
nDefaultPort: 37770
nRPCPort: 37771

RPC\Cli documentation almost same with Bitcoin. Check it out [here](https://en.bitcoin.it/wiki/Original_Bitcoin_client/API_calls_list).