# Linux Mining Guide

The purpose of this guide is to get you started with mining Zoin on Linux. This guide is intended for Ubuntu 16.04 but similar steps should work with other Debian distributions.

Please let us know if you experience issues following this guide. A helpful community is always available to assist on [Discord](https://discord.gg/mE3KemF). Alternatively, feel free to contribute to it! Zoin is a community coin and we are always welcoming contributions that help Zoin grow.

## Building the Miner

The steps in this section explain how to properly obtain and build cpuminer-opt, which is the recommended miner on Linux.

First, update the apt package manger to obtain the latest packages and install the necessary miner dependences:

```
sudo apt-get update

sudo apt-get install automake autoconf pkg-config libcurl4-openssl-dev libjansson-dev \
                     libssl-dev libgmp-dev autotools-dev automake make \ 
                     libcurl4-openssl-dev g++ libssl-dev libgmp3-dev build-essential \
                     screen automake m4 openssl libssl-dev git libjson0 libjson0-dev \
                     libcurl4-openssl-dev autoconf python-software-properties -y

```



Once the dependencies are done installing, clone cpuminer from the Github repository and run the build script.

```
cd ~
git clone https://github.com/JayDDee/cpuminer-opt
cd cpuminer-opt
./build.sh
```

## Running the Miner

If you haven't already registered for a mining pool, do so now. The example below uses the [Zoin Official Pool](https://zoin.netabuse.net/), but other pools can be found towards the bottom of the [Zoin Website](https://zoinofficial.com/).

Next, enter the following command, ensuring to update the following fields in &lt;brackets&gt;:

* **&lt;username&gt;**: Your username you used to register with on the pool.
* **&lt;worker name&gt;**: The name of a worker you registered on the pool.  See your pool's Getting Started guide for assistance with this.
* **&lt;password&gt;**: The password you assigned to your worker.  This is _not_ the login password for your pool account.
* **&lt;threads&gt;**: The `-t `flag and threads is optional.  This indicates the number of threads to mine with.  Depending on your hardware specifications, tweaking this number can help improve performance.  If this is left off, the default will use the number of cores for your processor.

```bash
./cpuminer -a lyra2zoin -o stratum+tcp://zoin.netabuse.net:3000 -u <username>.<worker name> -p <password> -t <threads>
```

## Running the Miner on Startup

Optionally, you can run the miner on startup.  There are multiple ways to do this, and one approach is outlined below.  Run the following commands and upon reboot of your machine you should see the miner running in the background.

First, create a shell script using your favorite Linux text editor:

```bash
cd ~
vi runMiner.sh
```

Next, enter the following command in the file.  This assumes you cloned the miner in your home directory, so if you put it elsewhere you will need to update the paths.  Be sure to update the **&lt;username&gt;**, **&lt;worker name&gt;**, **&lt;password&gt;**, and **&lt;threads&gt;** parameters as described in **Running the Miner **above.  

```bash
#! /bin/bash
cd ~/cpuminer-opt
./cpuminer -a lyra2zoin -o stratum+tcp://zoin.netabuse.net:3000 -u <username>.<worker name> -p <password> -t <threads>
```



Next, make your script executable and verify you entered everything correctly by running it.  If everything is configured correctly, you should see accepted shares after a few minutes.

```
sudo chmod a+x ~/runMiner.sh
./runMiner.sh
```



If everything above is running correctly, terminate the script with **Ctrl+C**.  Next, move the script to the `bin` directory:

```
sudo mv ~/runMiner.sh /usr/local/bin
```



Next, we will switch to the root user and remove `exit 0` from `/etc/rc.local` if it exists:

```bash
sudo su - # Switch to root
sed -i s/'exit 0'//g /etc/rc.local
```



Next, we will add the miner script to `/etc/rc.local` and add back the `exit 0` using the `echo` command and `>>` for redirection of output to a file.  Be sure to replace **&lt;username&gt;** with your user account on Linux.

```
echo "su - <username> -c runMiner.sh
exit 0" >> /etc/rc.local
```



Finally, exit from the root user and restart:

```
exit
sudo shutdown -r now
```



Upon startup, run `ps` or `top` and you should see `cpuminer` running in the background:

```
ps -ef | grep cpuminer
```



