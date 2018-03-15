# Release Notes

## v0.13.1.4 \(2018-03-12\)

**MANDATORY UPGRADE BEFORE BLOCK 261500 \(ZOINODES ENABLED\) 0.13.1.3 WILL NOT WORK**

**Changelog**

* Enable Zoinodes at block 261500, payouts start at 262100
* Zoinode GUI
* Heavily reduced reindex time
* Upgraded Zerocoin wallet storage
* Zerocoin performance upgrade
* One touch TOR network reroute on overview GUI
* OBFS4 support
* Fixed minor bugs and tweaks.
* Fixed reindex issue for some users

**Instructions**

* Backup wallet.dat
* Run Zoin Core 13.1.4, it will trigger a required reindex \(if upgrading from 13.0.2 and less\) making your wallet.dat not compatible with older versions
* Done

**Known Issues/Bugs**

* Windows scaling issue with higher than 100% scaling set

**Credits **to Dash for the masternode implementation structure, and to Zcoin for their zerocoin library revamp.

## v0.13.1.3 \(2018-03-11\)

**MANDATORY UPGRADE BEFORE BLOCK 261500 \(ZOINODES ENABLED\)**

**Changelog**

* Enable Zoinodes at block 261500, payouts start at 262100
* Zoinode GUI
* Heavily reduced reindex time
* Upgraded Zerocoin wallet storage
* Zerocoin performance upgrade
* One touch TOR network reroute on overview GUI
* OBFS4 support
* Fixed minor bugs and tweaks.

**Instructions**

* Backup wallet.dat
* Run Zoin Core 13.1.3, it will trigger a required reindex making your wallet.dat not compatible with older versions
* Done

**Known Issues/Bugs**

* Windows scaling issue with higher than 100% scaling set

**Credits **to Dash for the masternode implementation structure, and to Zcoin for their zerocoin library revamp.

## v0.13.0.2 \(2018-02-01\)

**Changelog**

* Upgrade to GUI V2
* Paper wallet generator
* Added EUR portfolio price option in settings/preferences.
* Added custom change address.
* Fix wrong transaction display.
* Windows/Linux font distortion fix.
* Many minor bugs and tweaks.

If you are stuck when upgrading to this version from version 0.13.0.0 or before and the wallet did not ask for a reindex on initial bootup, make sure to go into your Zoin data directory and delete peers.dat and banlist.dat then do a reindex.

**Known Issues/Bugs**

* Windows scaling issue with higher than 100% scaling set

## v0.13.0.1 \(2018-01-22\)

**Changelog**

* Fix for reindex popup everytime wallet is booted.
* Correct display of price ticker and indicators.
* Fix for mac wallet crash.

**How To Install**

1. Backup your wallet.dat to a new location or do so by going to File &gt; Backup.

2. Go into your Zoin data directory and delete peers.dat and banlist.dat

   * Linux ~/.zoin
   * Mac ~/Library/Application Support/zoin/
   * Windows %appdata%\zoin

3. FOR MAC USERS:

   * If Homebrew is not installed, open a terminal and paste this command:
     `/usr/bin/ruby -e "$(curl -fsSL `[`https://raw.githubusercontent.com/Homebrew/install/master/install`](https://raw.githubusercontent.com/Homebrew/install/master/install)`)"`
   * Open a terminal and paste this command:
     `brew install automake berkeley-db4 libtool boost --c++11 miniupnpc openssl pkg-config homebrew/versions/protobuf260 --c++11 qt5 libevent`

4. Run wallet, the wallet will ask to reindex, say "ok".

5. Wait for reindex to finish.

6. Done.

If you are stuck when upgrading to this version and the wallet did not ask for a reindex on initial bootup, make sure to go into your Zoin data directory and delete peers.dat and banlist.dat then do a reindex.

**Known Issues/Bugs**

* Windows scaling issue with higher than 100% scaling set
* Windows/Linux Font distortion on some builds \(Will need YU GOTHIC UI Font on your system, comes standard with windows 10\)

## v0.13.0.0 \(2018-01-17\)

**What's New**

* BTC Core 0.13 implementation
* HD Wallet support
* Fulltime Zerocoin protocol to V2
* Pruned nodes
* Multiple BIP implementations -
  [https://github.com/zoinofficial/zoin/blob/master/doc/bips.md](https://github.com/zoinofficial/zoin/blob/master/doc/bips.md)
* Atomic Swap compatibility
* Fixed recurring sync issues
* Faster sync from scratch \(~5 hours @ 230k blocks\)
* TOR stream isolation
* Addition to transaction fee editor in GUI
* GUI cleanup
* Peer table in GUI
* Network traffic monitor in GUI

Before upgrading to this version:

* Backup your wallet.dat to a new location or do so by going to File &gt; Backup
* Browse to your Zoin directory
  * Linux `~/.zoin`
  * Mac `~/Library/Application Support/zoin/`
  * Windows `%appdata%\zoin`
* Delete all files and directories except for wallet.dat
* Run Zoin Core 0.13

**Development Fund**  
With these additions, the Development Reward Fund, which was voted on by 95% of the community 2 months ago in November 2017, has been instated and will initiate at block 230250 until block 255250 increasing block rewards to 50 and allocation 37.5 Zoin per block to the fund. This will not affect miner rewards, once block 255250 is reached, block rewards will go back to 12.5, again not affecting miners.

**Credits**to Tim Ruffing for his contribution on improving security of the Zerocoin Protocol, as well as to the Zcoin development team for their continuous additions to the Zerocoin Protocol.

**Known Issues/Bugs**

* Windows scaling issue with higher than 100% scaling set
* Mac build not fetching Zoin price info
* Portfilio value in USD stays 0.00 USD

## v0.9.0.2 \(2017-12-25\)

Fix sync issues from scratch pertaining to older Zerocoin spends. Fix blurry font issues on windows and linux GUI.

## v0.9.0.1 \(2017-12-08\)

Fixed halted blockchain. Temporarily removed DevRewards.



