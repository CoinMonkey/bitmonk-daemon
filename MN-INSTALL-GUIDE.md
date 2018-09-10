# For install with link to windows wallet:

## 1. Register new VPS

We recommend you to register a new VPS (droplet) at DigitOcean [cloud.digitalocean.com](https://m.do.co/c/9ba9ece23196o). 

  - Press green "Create" button (top right)
  - Choose Ubuntu 16.04.4 x64 (pay attention to the version, it's important)
  - Choose 1-2GB RAM and 25+GB of space
  - Create it
  - Check login and password for server at e-mail. Save IP address, this is your *{IPLinuxServer}*

## 2. Generate keys

  - Open windows wallet
  - Make new transaction with 250000 BMO amount (this is transaction to yourself or from another wallet)
  - Wait 15 minutes
  - Go to the console tab and type 2 commands:
  
  ```
  masternode genkey
  ```
  Save returned string, this is your *{genkey}* (for example, 69Y2Rqpr7ugWTdVJV1pklYgRofa6b10oX5rSCpMYRcRlD8qDk21).

  ```
  masternode outputs
  ```
  Save returned strins, this is your *{output1}* and *{output2}* (one long, one short, for example "41b130b7ec3d318e6cacba13f8c3148d627f9446a78885f387d45aef6313012c" : "1")

## 3. Install MN node at Linux

 - Download Putty SSH https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html
 - Connect to server via IP address, login (root) and password
 - Download and launch the installer script. On 3rd step give your correct {genkey} to script. Just type in terminal, after press Enter:
 
 ```
 wget https://raw.githubusercontent.com/CoinMonkey/bitmonk-daemon/master/bmo-mn-installer.sh && chmod 755 bmo-mn-installer.sh && ./bmo-mn-installer.sh
 ```
 
## 4. Start your MN

 - Go to "Wallet" tab in windows wallet and click on the link "My MN: 0"
 - Click on Edit button (right side of window), it will open folder with config for you
 - Open Bitmonk.conf and replace config with:
```
rpcuser=p1
rpcpassword=p2
staking=0
```

 - Open masternode.conf and instert this line:
 ```
mn1 {IPLinuxServer}:37770 {genkey} {output1} {output2}
```

Where:

 - IPLinuxServer - is the IP address of your Ubuntu server
 - {genkey} - generated string from step 2
 - {output1} - generated string from step 2 (long)
 - {output2} - generated string from step 2 (short)
 
 Example of this file:
 
 ```
 mn1 111.11.232.111:37770 6PPSfjicR3p7ccdRtGzPLTxTmbXefiVNfv1iV8DAR4Jw9yMaPLK 41b130b7ec3d318e6cacba14f8c3248d627f9446a71115f387d45aef6313012c 1
 ```
 
 Save both files and relaunch the wallet. Now open link "My MN: 0" again and press "Start All" button. Your MN will start within 2 hours.

# For install on linux:

The easiest way to launch your MN without windows wallet:

## 1.  Register new VPS with Ubuntu 16.04 on board
## 2.  Connect to VPS via SSH
## 3. Run command and follow all steps of installator

 ```
wget https://raw.githubusercontent.com/CoinMonkey/bitmonk-daemon/master/bmo-node-installer.sh && chmod 755 bmo-node-installer.sh && ./bmo-node-installer.sh
 ```

## 4. Get new address:

bitmonkd getnewaddress

## 5. Send 250k coins to generated address
## 6. Wait when node will be synced (check balance: bitmonkd getbalance)
## 7. Wait 15 confirmations of this transaction
## 8. Run commands:

```
bitmonkd genkey
bitmonkd outputs
```
 
Write down returned strings

## 9. Open config and change "masternode" and "masternodeprivkey" settings, add nodes (nano /root/.Bitmonk/Bitmonk.conf):
```
masternode=1
masternodeprivkey={genkey}
```

Add these nodes to the end of file:

```
addnode=178.128.111.124
addnode=138.68.81.193
addnode=185.204.3.101
addnode=199.247.7.103
addnode=95.213.184.109
addnode=178.128.111.124
addnode=185.204.3.173
addnode=64.59.94.130
addnode=142.93.169.148
addnode=207.154.210.39
addnode=5.149.252.184
addnode=79.141.160.49
addnode=185.81.115.16
```

And save it (ctrl+x + Y + enter)

## 10. Open MN config (nano /root/.Bitmonk/masternode.conf) and add one line:

mn1 {IPLinuxServer}:37770 {genkey} {output1} {output2}

Save it (ctrl+x + Y + enter)

## 11. Relaunch daemon:

```
bitmonkd stop
bitmonkd -daemon -reindex
```

Done. Wait 1 hour and your node will start processing, you will receive rewards on your linux wallet.

This command should return you "successfully started masternode":

```
bitmonkd masternode debug
```
