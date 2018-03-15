# Create a Zoinode on Linux

## Disclaimer

Zoin team is not in any way responsible if you don't provide a necessary hardening level to your VPS/Servers. We try to make everything simple and super easy, but if you fail to implement some basic and/or Advanced Security Level in your Zoinodes we are not responsible if disasters happen.

If you not feel confident in setting up, running and mantain your Zoinodes, you can contact a Trusted 3rd-party service as [Zednodes](http://zednode.com/) and let them do everything for you.

## Prerequisites

1. **Zoin Core Wallet v0.13.1.4 or later: **See [Github](https://github.com/zoinofficial/zoin/releases) for the latest release and release notes.

2. **25,000 Zoin**

3. **A Virtual Private Server \(VPS\):** A VPS is recommend as a Zoinode requires dedicated resources and 24x7 availability for proper operation.  Although it is possible, in theory, to run a Zoinode from your desktop, this guide will not walk through those steps.  The VPS must have:  
   1. At least 2 GB of RAM  
   2. At least 20 GB of storage space  
   3. A static public IP address

4. **Secure the Wallet:** This is optional but **highly recommended**.  See [Wallet / Securing the Zoin Wallet](/wallet/securing-the-wallet.md) for details.

5. **Review the Release Notes: **See the Release Notes in the [Documentation](/introduction/release-notes.md) or on [Github](https://github.com/zoinofficial/zoin/releases) that corresponds with the version of the wallet you are using.

## Generating a Zoinode Key

This section describes how to generate a Zoinode key from a desktop wallet.  You can associate a desktop wallet address with a Zoinode on a separate server, which this section describes.

First, launch your desktop wallet and navigate to **Help --&gt; Debug Window --&gt; Console **as shown in the screenshot below:  
![](/assets/wallet-console.png)

In the console, enter the following command.  This generates the Zoinode key.  Be sure to save it to a safe location.

```
zoinode genkey
```

Next, enter the following command to generate a Zoinode deposit address for the 25,000 Zoin collateral.  ZN1 will be the label assigned to the new deposit address and can be changed if desired.

```
getaccountaddress ZN1
```

After generating the Zoinode key and Zoinode wallet address, transfer the collateral deposit of 25,000 Zoin.  Be aware that you must send **exactly 25,000 Zoin in a single transaction**.  Also consider that a transaction fee will be deducted.

Once you have sent the 25,000 Zoin to the address generated from `getaccountaddress`, you will need to obtain the transaction ID and index.  Do this by navigating to **Help --&gt; Debug Window --&gt; Console** as shown in the screenshot above.

Type the following into the Console to obtain your **Transaction ID** and **Index**:

```
zoinode outputs
```

You should see the something similar to the example below:

```
{ "d8ff88888bb6d9998d22c5155437f009c72dfd55dd2222f87fd55e22c0f89ddc" : "1", }
```

From the example, we get the **Transaction ID** and **Index**:

* **Transaction ID: **d8ff88888bb6d9998d22c5155437f009c72dfd55dd2222f87fd55e22c0f89ddc
* **Index: **1

Next, you will need to create a text file on the computer with the desktop wallet.  Depending on your operating system, create a file called `zoinode.conf`and place it in the appropriate directory:

* **Windows:**`%APPDATA%`
* **OS X:** `~/Library/Application Support/zoin`
* **Linux:** `$HOME/.zoin`

In the file, add a line that matches the following syntax.  If you are running multiple Zoinodes, you will add one line for each node with the appropriate values:

`LABEL IP:82255 ZOINODEPRIVATEKEY TXID INDEX`

Where:

* **LABEL:** The label of the node used for `getaccountaddress` command above.
* **IP:** Your VPS public IP address.
* **ZOINODEPRIVATEKEY:** Zoinode key previously generated with the `zoinode genkey`command.
* **TXID:** The Transaction ID obtained using the `zoinode outputs` command above.
* **INDEX:** The Index obtained using the `zoinode outputs` command above.

Your file should look like this, except the first line which is there for visual reference.  The file will only have one line.

![](/assets/zoinode-conf.png)

Save the file and restart your wallet.  The wallet is now configured for Zoinode and next we will setup and link the Zoinode server.

## Server Configuration

### Install Necessary Packages

The following packages are mandatory to successfully setup a Zoinode:

```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install build-essential libtool autotools-dev automake pkg-config \
                     libssl-dev libevent-dev bsdmainutils libboost-all-dev \
                     software-properties-common

sudo add-apt-repository ppa:bitcoin/bitcoin
sudo apt-get update

sudo apt-get install libdb4.8-dev libdb4.8++-dev libminiupnpc-dev libzmq3-dev \
             libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools \
             libprotobuf-dev protobuf-compiler libqrencode-dev unzip screen
```

Next, we will install and configure UFW, a firewall for Linux:

```bash
sudo apt-get install uwf
ufw allow ssh/tcp
ufw limit ssh/tcp
ufw allow 8255/tcp
ufw logging on
ufw enable
```

It is also recommended that you further harden your server with [AppArmor](https://wiki.ubuntu.com/AppArmor) or [SELinux](https://wiki.debian.org/SELinux), [Fail2Ban](https://www.fail2ban.org/wiki/index.php/Main_Page), and other common best practices as suggested [here](https://www.cisecurity.org/cis-benchmarks/).

## Download, Build & Configure the Zoin Wallet

First, download the latest version of the Zoin wallet into your home directory, extract, and rename for clarity:

```bash
cd ~
wget https://github.com/zoinoicial/zoin/archive/v0.13.1.4.tar.gz
tar -xzvf v0.13.1.4.tar.gz
mv v0.13.1.4.tar.gz zoin-0.13.1.4
```

Next, we will build the wallet.  These steps will take some time to complete, so please be patient:

```bash
cd zoin-0.13.1.4
./autogen.sh
./configure –without-gui –enable-wallet
make
make install
```

Once the installation is complete, we need to set up the Zoin configuration files:

```bash
mkdir ~/.zoin
nano ~/.zoin/zoin.conf
```

Next, enter the following configuration.  Be sure to update the following fields in &lt;brackets&gt;:

* **&lt;username&gt;**: For example, zoinuser
* **&lt;password&gt;:** Any secure password, although the `rpcallow=127.0.0.1` configuration prevents access outside the server itself.
* **&lt;zoinode-ip-address&gt;: **The public IP address assigned to your server.  Refer to your VPS provider documentation for details on how to assign and obtain your public IP address.
* **&lt;zoinode-private-key&gt;:** The private key of the wallet address that will be associated with your Zoinode as documented above.

```
rpcuser=<username>
rpcpassword=<password>
rpcallowip=127.0.0.1
port=8255
rpcport=8822
listen=0
server=1
daemon=1
logtimestamps=1
maxconnections=64
txindex=1
zoinode=1
externalip=<zoinode-ip-address>:8255
zoinodeprivkey=<zoinode-private-key>
```

Press **Ctrl+X** to save and **y** to confirm.

# Zoinode Payments

A single Zoinode gets paid for every block, so if there are 150 active nodes you will receive your payment once every 150 blocks, or roughly every 375 min \(6.25 hours\) to your Zoinode address \(the one containing 25,000 ZOI\).  Note that every time your Zoinode goes offline or if it is restarted, it resets to the last place in the payout queue.  Therefore it is critical that your VPS is stable with a decent network connection to ensure consistent payments.

