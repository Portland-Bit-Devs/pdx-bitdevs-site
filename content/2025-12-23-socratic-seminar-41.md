+++
title = "PDX BitDevs Socratic Seminar #42"
template = "post.html"
[extra]
meetup_id = "307472941"
+++
## Announcements

Please join us for our next Socratic Seminar. A special thank you to our host <a href="https://dicksprimalburger.com/" data-no-summary>Primal Burger</a>, for the event space. Please support them by buying their delicious food or a beverage.

If you can't make it to the main event please join us at Lutz Tavern around 9PM **<a href="https://www.lutztavern.com/" data-no-summary>here</a>.**

### Special Thanks | Mentions

- Libbitcoin Presentation - [PortlandHODL](https://github.com/portlandhodl)

### Rules

- Respect people's privacy
  - No Photos / Sequenced Photos
  - No Audio Recording
  - No Phones in your shirt front pocket camera out.
- [Chatham House Rules](https://www.chathamhouse.org/about-us/chatham-house-rule)
- Interaction and asking questions are encouraged!

### Requests

- A guest speaker for January 27th 2025

### Schedule

- **6:00pm - 6:30pm:** Arrive, socialize, and grab some food.
- **6:30pm - 7:30pm:** Libbitcoin Presentation
- **7:30pm - 8:00pm:** Bitcoin Development Discussions

## Bitcoin Dev news

- [New Mempool.space precise fee rates endpoint](https://x.com/OrangeSurfBTC/status/1995331334655586322)
- [Use slightly over integer fees](https://x.com/OrangeSurfBTC/status/1995340887921176785)
- [RDTS (BIP110) Impact over time](https://x.com/mononautical/status/1988449182462660964/photo/1)
- [The Cat - Non-Monetary UTXO Cleanup](https://github.com/bitcoin/bips/pull/2048)
- [Jade Firmware PWN'd Again](https://x.com/darosior/status/2001269835305496835)
- [Human Bitcoin Addresses](https://spiralbtc.substack.com/p/making-bitcoin-speak-human)
 - [Possible mockups](https://x.com/OrangeSurfBTC/status/1999531873207205924) 
- [Libsecp256k1 Performance vs. OpenSSL](https://delvingbitcoin.org/t/comparing-the-performance-of-ecdsa-signature-validation-in-openssl-vs-libsecp256k1-over-the-last-decade/2087)
- [Quantum FUD is back](https://x.com/nic_carter/status/2001653606328487975)
- [BIP 360 Update](https://delvingbitcoin.org/t/major-bip-360-update/2170)
- [LUA based  policy](https://github.com/jasonfoura/bitcoin/pull/1)
- [Ledger Bitcoin App Updater](https://x.com/Rob1Ham/status/2003137941619564683)
- [Cluster Mempool (v31?)](https://github.com/bitcoin/bitcoin/pull/33629)
  - [Thread](https://x.com/murchandamus/status/1854678133896626293)  
- [RDTS Softfork Proposal](https://github.com/bitcoin/bips/pull/2017)
- [Proposed Limit to ScriptPubkey Size](https://groups.google.com/g/bitcoindev/c/YO8ZwnG_ISs)
  - [Abandoned](https://x.com/PortlandHODL/status/1988459825903399058)
  - [OP_TECH](https://bitcoinops.org/en/newsletters/2025/11/07/#multiple-discussions-about-restricting-data)
- [MARA Pool Empty Block](https://x.com/mononautical/status/1991110957968265699)
- [Ordiknots](https://github.com/taproot-wizards/ordiknots)
- [C Bitcoin Kernel Header API](https://github.com/bitcoin/bitcoin/pull/30595)
- [Sync Performance Improvement](https://github.com/bitcoin/bitcoin/pull/31645)
- [Chaincode Delegationin](https://block.xyz/inside/chain-code-delegation-improving-privacy-in-collaborative-multisig)
- [Onchain RDTS (444) Softfork Contract](https://x.com/Rob1Ham/status/1987284298144399683)

## Bitcoin General News

- [Naka Rugged 6MM payout](https://x.com/HodlMagoo/status/1991679031625040183)
- [Samuori Devs Jailed](https://www.justice.gov/usao-sdny/pr/founders-samourai-wallet-cryptocurrency-mixing-service-sentenced-five-and-four-years)
- [Start9 Selling Treasury](https://x.com/start9labs/status/1985797112265654559)

## Tech news

- [DDR 4/5 Prices go Parabolic](https://pcpartpicker.com/trends/price/memory/)
- [Raspberry pi5 Price Hikes](https://www.pcmag.com/news/facing-memory-shortage-raspberry-pi-hikes-prices-introduces-1gb-option)

## Libbitcoin Server

### Why?

The primary reason would be to not be dependent on another Bitcoin Core based client implementation.

There are also many built in protocols

- Stratum v2
- Electrs
- bitcoind
- Web
- ZMQ
- Explorer

### Prep

- Host (Computer)
- Internet
- Time (1 hour+)

### Installation

You will need a host that acts like a server, this would be something ideally running Linux, but could be Windows or MacOS.
Libbitcoin does require boost >= 1.86.0. This needs to be installed before building and configuring. The install.sh file
that is included did not fetch/build/install boost.

This required me to run the following shell commands

```
cd ~
wget https://archives.boost.io/release/1.86.0/source/boost_1_86_0.tar.gz
tar -xzf boost_1_86_0.tar.gz
cd boost_1_86_0
./bootstrap.sh --prefix=/usr/local
sudo ./b2 -j$(nproc) install
sudo ldconfig
```

But wait there is more! Time to ensure that we have [libsecp256k1](https://github.com/bitcoin-core/secp256k1) installed too.

```
cd ~
git clone https://github.com/bitcoin-core/secp256k1.git
cd secp256k1
./autogen.sh
./configure --prefix=/usr
make -j$(nproc)
sudo make install
sudo ldconfig
```

Now run this. ([Install Script](https://github.com/libbitcoin/libbitcoin-system/blob/master/install.sh))

```
./install.sh --prefix=/home/<username>/<libbitcoin prefix> --disable-shared
```

Building on an 8 core machine Xeon E5-2620 takes about 20 minutes. Now we can build and install Libbitcoin server.
This build process failed on GCC with a segmentation fault. Clang 18.x seems to work just fine.

### Installation [Libbitcoin Node](https://github.com/libbitcoin/libbitcoin-node)

After doing the above steps we are able to run this command on Ubuntu

```
./install.sh --prefix=/home/<user>/development/libbitcoin/build/release_static/ --build-secp256k1 --build-boost --disable-shared
```

### Running

Out of the box most things don't seem to work overall. The first is the suggested config file is out of date use [Config for v4.0](https://github.com/libbitcoin/libbitcoin-node/blob/105388e012f0d87ea670c56f748619bb532aa6f3/src/parser.cpp#L697).

You can start libbitcoin with `./bn` or add your config file with `./bn --config ./bn.cfg` where bn.cfg is your configuration file.

### Problems

1. Just stops syncing ...
2. Fresh Ubuntu 24.04 will not build without Segfault
3. Config isn't properly documented
4. All connections are broken on startup?
5. Disk full error on Ubuntu startup
