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

## Bitcoin Dev News

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

## Libbitcoin Server

### Why?

The primary reason would be to not be dependent on another Bitcoin Core based client implementation.

### Prep

- Host (Computer)
- Internet
- Time (10 minutes - 1 hour)

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

But wait there is more! Time to ensure that we have libsecp256k1 installed too.

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
